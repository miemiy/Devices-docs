---
title: Conditional Access for Surface Hub
description: Understand how Conditional Access policies impact Surface Hub. Learn to configure policies, troubleshoot sign-in issues, and exclude device accounts. 
ms.assetid: 8BB80FA3-D364-4A90-B72B-65F0F0FC1F0D
ms.reviewer: 
manager: peterdem
ms.service: surface-hub
ms.sitesec: library
author: ryanbwold
ms.author: rwold
ms.topic: article
ms.date: 11/19/2024
ms.localizationpriority: medium
---

# Conditional Access for Surface Hub

## What is Conditional Access?

[Conditional Access](/azure/active-directory/conditional-access/overview) is a Microsoft Entra feature that allows organizations to configure policies to grant or block access to corporate resources. These policies use if-then statements based on [Assignments](/azure/active-directory/conditional-access/concept-conditional-access-policies#assignments) and [Access controls](/azure/active-directory/conditional-access/concept-conditional-access-policies#access-controls). Enforcing incompatible Conditional Access policies on a Surface Hub device account can lead to the following issues:

- Unable to add the device account to the Surface Hub
- Welcome Screen calendar fails to sync with Exchange
- Teams Rooms client not signing in

Follow the guidance on this page to understand how the Surface Hub device account interacts with Conditional Access and troubleshoot issues effectively.

---

## Device account and Conditional Access policies

The Surface Hub [device account](create-and-test-a-device-account-surface-hub.md) is used to receive meeting invitations and join Teams meetings. When creating Conditional Access policies, consider the following key assignments and access controls to prevent the device account from being blocked.

---

## Key assignments for Conditional Access

### Cloud apps

The Surface Hub device account uses the following [cloud apps](/azure/active-directory/conditional-access/concept-conditional-access-cloud-apps) when signing in. Make sure your Conditional Access policies allow sign-in to these resources to prevent interruptions:

- Office 365
- Office 365 Exchange Online
- Office 365 SharePoint Online (this includes OneDrive for Business)
- Graph Explorer
- Microsoft Teams

### Conditions

The Surface Hub is included in the following [conditions](/azure/active-directory/conditional-access/concept-conditional-access-conditions):

- Device platforms - Windows
- Client apps - Mobile apps and desktop

---

## Access controls incompatible with Surface Hub

The Surface Hub device account isn't compatible with Conditional Access policies that require the following Grant and Session Access controls. All Surface Hub device accounts must be [excluded](#exclude-device-account-from-unsupported-conditional-access-policies) from such policies.

### Grant

- Require multifactor authentication
- Require authentication strength (Preview)
- Require device to be marked as compliant
- Require Microsoft Entra hybrid joined device
- Require approved client app
- Require app protection policy
- Require password change

### Session

- Use app-enforced restrictions
- Use Conditional Access App Control

For more details on Assignments and Access controls, see the [building a Conditional Access policy](/azure/active-directory/conditional-access/concept-conditional-access-policies) article.

---

## Troubleshooting sign-in issues with Conditional Access policies

If your Surface Hub device account encounters sign-in errors, use the following tools and methods to diagnose and resolve Conditional Access policy conflicts.

1. **Azure sign-in logs**: Review the [Azure sign-in logs](troubleshoot-azure-sign-in-logs-for-surface-hub.md) to identify failures or interruptions. The details often reveal if a Conditional Access policy is blocking sign-in.
2. **What If tool**: Use the ["What If"](/azure/active-directory/conditional-access/what-if-tool) tool to determine which Conditional Access policies apply to the device account. Select the Surface Hub device account as the user and leave the default "Any cloud app" selected. Learn more at [Troubleshooting Conditional Access using the What If tool](/azure/active-directory/conditional-access/troubleshoot-conditional-access-what-if).

:::image type="content" source="images/what-if-tool.gif#lightbox" alt-text="Gif image showing how to select the Surface Hub device account and run the What If tool against it.":::

---

## Review Conditional Access policies

If the Azure sign-in logs and "What If" tool don't reveal any Conditional Access policies affecting the account, manually review every Conditional Access policy to ensure the Surface Hub device account isn't impacted.

### Step 1: Locate Conditional Access policies in Microsoft Intune

Navigate to your tenant's Conditional Access policies within Microsoft Intune. Ensure the user has the correct [role](/azure/active-directory/reports-monitoring/how-to-view-applied-conditional-access-policies#required-administrator-roles) assigned.

1. Sign into [Microsoft Intune admin center](https://intune.microsoft.com/)
2. Go to **Devices > Conditional Access**

:::image type="content" source="images/conditional-access-policies.png#lightbox" alt-text="Image showing where to locate a tenant's Conditional Access policies.":::

### Step 2: Review policy assignments and access controls

Select each Conditional Access policy and review its **Assignments** and **Access Controls**. Use the requirements listed above to determine if the policy is compatible with the Surface Hub. If not, the device account needs to be [excluded](#exclude-device-account-from-unsupported-conditional-access-policies) from such policies.

:::image type="content" source="images/conditional-access-review-policies.gif#lightbox" alt-text="Gif image showing how to review each Conditional Access policy for Surface Hub compatibility.":::

>[!NOTE]
>Policies in *On* or *Report Only* states can affect the Surface Hub device account.

---

## Exclude device account from unsupported Conditional Access policies

Due to the limited number of policies the Surface Hub device account supports, it often needs to be excluded from Conditional Access policies to allow sign-in. Follow these steps:

1. In the Conditional Access policy, navigate to **Assignments**, then select **Users > Exclude**.
2. Select **Users and groups**.
3. Choose each Surface Hub device account or group of device accounts.
4. Click **Save** at the bottom of the screen.

> [!IMPORTANT]  
> Ensure you select the Surface Hub device account **user** object, not the Surface Hub **device** object.

Watch this [video](https://www.youtube.com/watch?v=5DsW1hB3Jqs&ab_channel=MicrosoftSecurity) for step-by-step guidance on excluding user accounts from Conditional Access policies.

:::image type="content" source="images/conditional-access-exclude-device-account.png#lightbox" alt-text="Image showing how to exclude the Surface Hub device account from a Conditional Access policy.":::