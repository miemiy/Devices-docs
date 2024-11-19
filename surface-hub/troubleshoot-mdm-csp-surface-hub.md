---
title: Troubleshoot configuration service provider policy settings for Surface Hub
description: Learn how to troubleshoot configuration service provider (CSP) policy settings on Surface Hub, including MDM enrollment and deployment steps.
manager: frankbu
ms.service: surface-hub
author: coveminer
ms.author: chauncel
ms.topic: troubleshooting
ms.date: 02/03/2023
ms.localizationpriority: medium
---

# Troubleshoot configuration service provider policy settings for Surface Hub

[Configuration service providers](/surface-hub/manage-settings-with-mdm-for-surface-hub#manage-surface-hub-windows-10-team-settings-with-intune) (CSPs) offer a robust set of options for deploying policy settings to Surface Hub. If your CSP settings are not working, follow these troubleshooting steps to identify and resolve the issue.

---

## Verify Surface Hub enrollment in MDM

1. **Check MDM enrollment**  
   Ensure that Surface Hub is enrolled in a mobile device management (MDM) provider without errors and is syncing correctly:
   - Sign in to Surface Hub with an admin account.
   - Navigate to **Settings** > **Surface Hub** > **Device management**.  
   - Confirm that a tenant with an email address is displayed, indicating that the device is enrolled in MDM.

2. **Review sync status**  
   To verify the sync status or check for any errors:
   - Select the email address.
   - Choose **Info** to display the device's sync status.

---

## Troubleshoot MDM issues

### Step 1: Confirm CSP support on Surface Hub

Refer to the following documentation to verify whether your CSP is supported on Surface Hub:
- [SurfaceHub CSP](/windows/client-management/mdm/surfacehub-csp)
- [CSPs supported in Microsoft Surface Hub](/windows/client-management/mdm/configuration-service-provider-support#csps-supported-in-microsoft-surface-hub)
- [Policies in Policy CSP supported by Microsoft Surface Hub](/windows/client-management/mdm/policies-in-policy-csp-supported-by-surface-hub)

### Step 2: Validate configuration in Microsoft Intune

1. **Sign in to the Intune admin center**  
   Access the [**Microsoft Intune admin center**](https://intune.microsoft.com/), and navigate to **Devices** > **Configuration profiles**. Select the relevant CSP configuration profile.

2. **Confirm device group assignment**  
   On the CSP configuration profile page:
   - Ensure the profile is applied to a **Device group** (not a user group or device account).

3. **Verify deployment status**  
   Check whether the CSP is deployed to your Surface Hub:
   - In Intune, go to **Devices** > **All devices**.
   - Select your Surface Hub from the list.
   - Navigate to **Device configuration** to confirm that the CSP is deployed successfully.

### Step 3: Check network connectivity

Ensure that the appropriate [Intune URLs and IP ranges](/mem/intune/fundamentals/intune-endpoints) are allowed through your proxy or firewall. Blocked endpoints can interfere with the deployment of CSP settings to your Surface Hub.
