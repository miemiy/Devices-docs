---
title: Enroll Surface Hub to MDM provider
description: Learn how to enroll Surface Hub in MDM via manual or auto methods, including Intune setup for streamlined management and compliance
manager: frankbu
ms.service: surface-hub
author: coveminer
ms.author: chauncel
ms.topic: how-to
ms.date: 11/13/2024
ms.localizationpriority: medium
appliesto:
- Surface Hub 2S
- Surface Hub
---


# Enroll Surface Hub into MDM management

Learn how to enroll Surface Hub into Microsoft Intune or other Mobile Device Management (MDM) providers using manual or automatic enrollment options.

## Manual enrollment

1. Open the **Settings** app, sign in as a local administrator, and go to **Surface Hub** > **Device management**. Select **+Device management**.
2. Sign in with the account to use with your MDM provider. After authentication, the device automatically enrolls with your MDM provider.

> [!TIP]  
> If you’re using Intune and the server address isn’t automatically detected, enter **manage.microsoft.com**.

> [!NOTE]  
> MDM enrollment uses the provided account for authentication. Ensure this account has permissions to enroll a Windows device and an Intune license or equivalent permissions in your third-party MDM provider.

<a name='auto-enrollment--azure-ad-affiliated'></a>

## Auto enrollment with Microsoft Entra affiliation

During the [initial setup process](/surface-hub/first-run-program-surface-hub#microsoft-azure-active-directory), if you affiliate Surface Hub with a Microsoft Entra tenant that has Intune auto enrollment enabled, the device automatically enrolls in Intune. For more information, see [Enroll Windows client devices in Microsoft Intune](/mem/intune/fundamentals/deployment-guide-enrollment-windows). Microsoft Entra affiliation and Intune auto enrollment are required for Surface Hub to be a "compliant device" in Intune.

## Manage Surface Hub via MDM

- For more management options, see [Manage Surface Hub with an MDM provider](manage-settings-with-mdm-for-surface-hub.md).