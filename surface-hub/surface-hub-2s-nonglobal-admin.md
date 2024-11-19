---
title: Configure non-Global Admin accounts on Surface Hub
description: Learn how to configure non-Global Admin accounts on Surface Hub, limiting permissions for enhanced security while allowing admins to manage device settings via Microsoft Entra domain integration
ms.service: surface-hub
author: coveminer
ms.author: chauncel
manager: frankbu
ms.topic: how-to
ms.date: 10/28/2024
ms.localizationpriority: Medium
ms.custom: has-azure-ad-ps-ref
appliesto:
- Surface Hub
- Surface Hub 2S
---

# Configure non-Global Admin accounts on Surface Hub

The Windows 10 Team 2020 Update introduces support for configuring non-global admin accounts with limited permissions to manage only the Settings app on Surface Hub devices joined to a Microsoft Entra domain. This enables IT administrators to scope admin permissions specifically to Surface Hub, reducing the risk of unwanted access across the entire Microsoft Entra domain.

> [!IMPORTANT]
> Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

Windows 10 Team 2020 Update 2 introduces support for the [LocalUsersAndGroups CSP](/windows/client-management/mdm/policy-csp-localusersandgroups), now the recommended method. While the [RestrictedGroups CSP](/windows/client-management/mdm/policy-csp-restrictedgroups) remains supported, it is deprecated.

> [!NOTE]
> Before you begin, confirm that your Surface Hub is joined to Microsoft Entra and auto-enrolled in Intune. If not, reset the Surface Hub and complete the [out-of-the-box (OOBE) setup](first-run-program-surface-hub.md) with Microsoft Entra ID. Only accounts authenticated via Microsoft Entra ID can use non-global admin configurations.

## Summary

The process of creating non-Global Admin accounts involves these steps:

1. In Intune, create a security group containing designated Surface Hub admins.
2. Use PowerShell to obtain the Microsoft Entra group’s SID.
3. Create an XML file with the Microsoft Entra group SID.
4. Create a Security Group containing the Surface Hub devices that the non-Global admins Security group manages. 
5. Create a custom Configuration profile to target the security group that contains your Surface Hub devices.

<a name='create-azure-ad-security-groups'></a>

## Create Microsoft Entra security groups

First, create a security group containing the admin accounts. Then create another security group for Surface Hub devices.  

### Create security group for Admin accounts

1. Sign in to Intune via the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Groups** > **New Group** > and under Group type, select **Security.**
2. Enter a group name, such as **Surface Hub Local Admins**, and select **Create**.

     ![Create security group for Hub admins.](images/sh-create-sec-group.png)

3. Open the group, select **Members**, and choose **Add members** to add the designated admin accounts. To learn more about creating groups in Intune, see  [Add groups to organize users and devices](/mem/intune/fundamentals/groups-add).

### Create security group for Surface Hub devices

1. Repeat the previous procedure to create a separate security group for Hub devices, such as **Surface Hub devices**.

     ![Create security group for Hub devices.](images/sh-create-sec-group-devices.png)

<a name='obtain-azure-ad-group-sid-using-powershell'></a>

## Obtain Microsoft Entra group SID using PowerShell

1. Launch PowerShell with elevated account privileges (**Run as Administrator**) and ensure your system is configured to run PowerShell scripts. To learn more, refer to [About Execution Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies?).
2. [Install Azure PowerShell module](/powershell/azure/install-az-ps).
3. Sign in to your Microsoft Entra tenant.

    ```powershell
    Connect-AzureAD
    ```

    [!INCLUDE [Azure AD PowerShell deprecation note](includes/aad-powershell-deprecation-note.md)]

4. When you're signed in to your tenant, run the following commandlet. It prompts you to "Please type the Object ID of your Microsoft Entra group."

    ```powershell
    function Convert-ObjectIdToSid
    {    param([String] $ObjectId)   
         $d=[UInt32[]]::new(4);[Buffer]::BlockCopy([Guid]::Parse($ObjectId).ToByteArray(),0,$d,0,16);"S-1-12-1-$d".Replace(' ','-')
      
    }
    ```

5. In Intune, select the group you created earlier and copy the Object ID, as shown in the following figure.

     ![Copy Object id of security group.](images/sh-objectid.png)

6. Run the following commandlet to get the security group's SID:

    ```powershell
    $AADGroup = Read-Host "Please type the Object ID of your Azure AD Group"
    $Result = Convert-ObjectIdToSid $AADGroup
    Write-Host "Your Azure Ad Group SID is" -ForegroundColor Yellow $Result
    ```

7. Paste the Object ID into the PowerShell commandlet, press **Enter**, and copy the **Microsoft Entra group SID** into a text editor.

<a name='create-xml-file-containing-azure-ad-group-sid'></a>

## Create XML file containing Microsoft Entra group SID

1. Copy the following code into a text editor:

    ```xml
    <GroupConfiguration>
    <accessgroup desc = "S-1-5-32-544">
        <group action = "U" />
        <add member = "AzureAD\bob@contoso.com"/>
        <add member = "S-1-12-1-XXXXXXXXXX-XXXXXXXXXX-XXXXXXXXXX-XXXXXXXXXX"/>
    </accessgroup>
    </GroupConfiguration>
    ```
2. Replace the placeholder SID (beginning with S-1-12-1) with your **Microsoft Entra group SID** and then save the file as XML; for example, **Microsoft Entra ID-local-admin.xml**.

      > [!NOTE]
      > Users can also be added directly using their User Principal Names (UPNs):  
      > `<member name="AzureAD\user@contoso.com" />`

## Create Custom configuration profile

1. In Microsoft Intune, go to **Devices** > **Configuration profiles** > **Create profile**.
2. Select **Windows 10 and later** for the platform. For the profile, choose **Templates** > **Custom** > **Create**.
3. Provide a name and description, then select **Next**.
4. Under **Configuration settings** > **OMA-URI Settings**, select **Add**.
5. Add a name and use the following OMA-URI:

    ```OMA-URI
     ./Device/Vendor/MSFT/Policy/Config/LocalUsersAndGroups/Configure
    ```

   > [!NOTE]
   > The **RestrictedGroups/ConfigureGroupMembership** policy setting allows adding or replacing local group members. However, it cannot selectively add or remove members without replacing the entire group. For Windows 10 Team 2020 Update 2, **LocalUsersAndGroups** is the recommended setting. Applying both policy settings to Surface Hub is unsupported and may yield unpredictable results.

6. Under Data type, select **String XML** and browse to open the XML file you created in the previous step.

     ![upload local admin xml config file.](images/sh-local-admin-config.png)

7. Select **Save**.
8. Select **Select groups to include** and choose the [security group you created earlier](#create-security-group-for-surface-hub-devices) (**Surface Hub devices**). Select **Next.**
9. Under Applicability rules, add a Rule if desired. Otherwise, select **Next** and then select **Create**.

To learn more about custom configuration profiles using OMA-URI strings, see [Use custom settings for Windows 10 devices in Intune](/mem/intune/configuration/custom-settings-windows-10).

## Non Global admins managing Surface Hub

Members of the newly configured **Surface Hub Local Admins** Security group can now sign in to the Settings app on Surface Hub and manage settings.

> [!IMPORTANT]
> If the [LocalUsersAndGroups CSP](/windows/client-management/mdm/policy-csp-localusersandgroups) is applied, access to the Settings app by global admins is removed unless explicitly configured using the “U” action.
