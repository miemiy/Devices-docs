---
title: Install and manage Surface Hub 3 Compute Cartridge
description: Explains how to upgrade Surface Hub 2S to Surface Hub 3 by installing the Surface Hub 3 Compute Cartridge. 
ms.reviewer: dpandre
manager: frankbu
ms.service: surface-hub
author: coveminer
ms.author: chauncel
ms.topic: how-to
ms.date: 01/18/2024
ms.localizationpriority: medium
appliesto:
- Surface Hub 2S
- Surface Hub 3

---

# Install and manage Surface Hub 3 Compute Cartridge

Enjoy the first all-in-one Teams Rooms board running on Windows by seamlessly updating your Surface Hub 2S to Microsoft Teams Rooms with the Surface Hub 3 Compute Cartridge (formerly Surface Hub 3 Pack). To place an order, contact your [Surface device reseller](https://www.microsoft.com/surface/business/where-to-buy-microsoft-surface#DEVICESRESELLERS).

## Install Surface Hub 3 Compute Cartridge

### Prerequisites

- A Surface Hub 2S, fully updated with the latest Windows Updates. By default, updates are installed automatically during nightly maintenance. To verify, go to **All apps** > **Settings** > **Update and Security** > **Windows Update**, and install all updates.

> [!TIP]
> You may need to restart the device and continue to check for available updates. Ensure the Surface Hub 2S's update history shows **Microsoft Corporation - System Hardware Update - 5/24/2023** or a **System Hardware Update** with any newer date (for example, 3/1/2024).

- An account with admin privileges. You need to reset the device if you don't know your username or admin password. For more information, see [Reset and recovery for Surface Hub 2S](/surface-hub/surface-hub-2s-recover-reset).
- A resource account with a [supported Microsoft Teams Rooms license](/microsoftteams/rooms/rooms-licensing).

> [!NOTE]
> Surface Hub 3 Compute Cartridge runs Windows 11 IoT Enterprise and does not support downgrading to Windows 10 Team or Windows 10 Pro/Enterprise. (If needed, you can reinstall the old cartridge to resume using Surface Hub 2S). 

### Demo video

Review the following demo and follow the instructions on this page.

> [!video 814a852d-7e1f-4193-98b3-2e5400395cfd]

### Detailed instructions

1. Shut down Surface Hub 2S, unplug all cables, and slide the cover sideways.

  ![Screenshot that indicates how to slide the cover sideways.](images/remove-cartridge-fig1.png).

2. Use a Phillips-head screwdriver to remove the retaining screw to detach the cartridge from Surface Hub 2S.

  ![Screenshot that shows retaining screw to remove and allow you to pull out the old cartridge.](images/remove-cartridge-fig2.png).

3. Slide the compute cartridge out. You can use the return label in the Surface Hub 3 Compute Cartridge packaging to send your old cartridge to Microsoft for recycling if desired.

  ![Screenshot that shows how to slide the compute cartridge out of the unit](images/remove-cartridge-fig3.png)

4. Slide the Surface Hub 3 Compute Cartridge into your Surface Hub.
5. Fasten the locking screw and slide the cover into place. Power on your new Surface Hub 3.  
6. Complete your setup with guidance from the following articles:

- [First-time setup for Surface Hub running Microsoft Teams Rooms on Windows](first-run-program-surface-hub-3.md).
- [Security best practices for Surface Hubs running Microsoft Teams Rooms on Windows](surface-hub-3-security.md)

## Manage Surface Hub 3

This section provides guidance on initial management steps for Teams Admin Center and Microsoft Intune or mobile device management (MDM) provider.

### Manual removal of upgraded Surface Hub devices from Teams Admin Center (Surface Hubs Legacy tab)

After upgrading your Surface Hub 2S with the Surface Hub 3 Compute Cartridge, you need to manually remove the device listing from the "Surface Hubs (Legacy)" section of Teams Admin Center. This will thereafter enable the device to show up properly under the "Teams Rooms on Windows" section and enable accurate device management.

1. **Navigate to Teams Admin Center**:
   - Open your web browser and go to the [Teams Admin Center](https://admin.teams.microsoft.com).
   - Sign in with your admin credentials.
2. **Access the Surface Hubs (Legacy) Tab**:
   - In the Teams Admin Center, select  **Teams devices** > **Surface Hubs (Legacy)**.
3. **Manually remove the upgraded device**:
   - Locate the row corresponding to the upgraded Surface Hub device and select the device.
   - Select **Remove** to manually remove the device's row from the list.
4. **Verification**:
   - Refresh the page or navigate away and then back to the **Surface Hubs (Legacy)** tab to ensure that the device has been successfully removed.
   - Verify that the upgraded device is now correctly managed under the appropriate tab for Teams Rooms devices, if applicable. This may take up to 12 hours to happen, but will happen automatically.
  
### Manual cleanup of stale Intune device records for upgraded Surface Hub devices

If you registered a Surface Hub 2S with Intune or other MDM provider before upgrading it with a Surface Hub 3 Compute Cartridge, you might encounter a "stale" device record. This situation occurs when the original device object in Intune remains, even after a new record is created for the Teams Rooms platform.

Although this stale record doesn't interfere with Intune-based management of the upgraded Surface Hub device, we recommend removal of these outdated entries to maintain directory cleanliness.

1. **Access** [Microsoft Intune Admin Center](https://intune.microsoft.com/): Sign in with your admin credentials.
2. **Navigate to Devices**: Use the left-hand navigation pane and select the **Devices** tab.
3. **Locate All Devices**: Within the **Overview** section, select **All devices** to view the entire list of managed devices.
4. **Identify and select the stale device object**: Look for the device object that needs removal. You can identify the stale entry based on your established device naming conventions. Typically, the stale record displays an OS build number of 19045, indicative of the Windows 10 Team edition.

   > [!NOTE]
   > Pay close attention to the OS build numbers to accurately distinguish between pre-upgrade and post-upgrade device records.

5. **Delete the stale record**: On the selected device object’s page, navigate to the top menu and select **Delete** to remove the stale device record from Intune.

## Surface Hub 2S Recycle Program

The Surface Hub 3 Compute Cartridge packaging allows you to return your old Surface Hub 2S cartridge to Microsoft for recycling. To participate, [remove the hard drive](#required-removal-of-hard-drive--corporate-data) from the cartridge to protect your sensitive data and [request a prepaid shipping label](#request-a-prepaid-shipping-label). 

### Required removal of hard drive & corporate data

Before recycling your Surface Hub 2S cartridge, first remove the hard drive and delete any corporate data.

1. You need the compute cartridge and a screwdriver.

![Screenshot that shows compute cartridge and screwdriver.](images/surface-hub-2s-repack-7.png)

2. Remove the cover screw and the cover from the compute cartridge and then remove the solid state drive (SSD).

![Screenshot that shows removal of cover screw and cover from the compute cartridge and removal of solid state drive (SSD).](images/surface-hub-2s-repack-8.png)

### Request a prepaid shipping label

Select your country/region and follow the instructions to obtain a shipping label. If you upgraded to the Surface Hub 3 Compute Cartridge, you can use its original packaging to ship the Surface Hub 2S cartridge for recycling. 

- [Australia](https://microsoft-hub.tes-amm.com/_Content/en-AU/)
- [Austria](https://microsoft-hub.tes-amm.com/_Content/de-AT/)
- [Bahrain](https://microsoft-hub.tes-amm.com/_Content/ar-BH/)
- [Belgium](https://microsoft-hub.tes-amm.com/_Content/nl-BE/)
- [Bulgaria](https://microsoft-hub.tes-amm.com/_Content/bg-BG)
- [Canada](https://microsoft-hub.tes-amm.com/_Content/en-CA/)
- [China](https://microsoft-hub.tes-amm.com/_Content/zh-CN/)
- [Croatia](https://microsoft-hub.tes-amm.com/_Content/hr-HR/)
- [Czech Republic](https://microsoft-hub.tes-amm.com/_Content/cs-CZ/)
- [Denmark](https://microsoft-hub.tes-amm.com/_Content/da-DK/)
- [Estonia](https://microsoft-hub.tes-amm.com/_Content/et-EE/)
- [Finland](https://microsoft-hub.tes-amm.com/_Content/fi-FI/)
- [France](https://microsoft-hub.tes-amm.com/_Content/fr-FR/)
- [Germany](https://microsoft-hub.tes-amm.com/_Content/de-DE/)
- [Greece](https://microsoft-hub.tes-amm.com/_Content/el-GR/)
- [Hong Kong](https://microsoft-hub.tes-amm.com/_Content/en-HK/)
- [Hungary](https://microsoft-hub.tes-amm.com/_Content/hu-HU/)
- [India](https://microsoft-hub.tes-amm.com/_Content/en-IN/)
- [Japan](https://microsoft-hub.tes-amm.com/_Content/ja-JP/)
- [Kuwait](https://microsoft-hub.tes-amm.com/_Content/ar-KW/)
- [Latvia](https://microsoft-hub.tes-amm.com/_Content/lv-LV/)
- [Lichtenstein](https://microsoft-hub.tes-amm.com/_Content/de-LI/)
- [Luxembourg](https://microsoft-hub.tes-amm.com/_Content/fr-LU/)
- [Malaysia](https://microsoft-hub.tes-amm.com/_Content/ms-MY/)
- [Mexico](https://microsoft-hub.tes-amm.com/_Content/es-MX/)
- [Netherlands](https://microsoft-hub.tes-amm.com/_Content/nl-NL/)
- [New Zealand](https://microsoft-hub.tes-amm.com/_Content/en-NZ/)
- [Norway](https://microsoft-hub.tes-amm.com/_Content/no/)
- [Poland](https://microsoft-hub.tes-amm.com/_Content/pl-PL/)
- [Portugal](https://microsoft-hub.tes-amm.com/_Content/pt-PT/)
- [Qatar](https://microsoft-hub.tes-amm.com/_Content/ar-QA/)
- [Romania](https://microsoft-hub.tes-amm.com/_Content/ro-RO/)
- [Saudi Arabia](https://microsoft-hub.tes-amm.com/_Content/ar-SA/)
- [Singapore](https://microsoft-hub.tes-amm.com/_Content/en-SG/)
- [Slovakia](https://microsoft-hub.tes-amm.com/_Content/sk-SK/)
- [Slovenia](https://microsoft-hub.tes-amm.com/_Content/sl-SI/)
- [South Africa](https://microsoft-hub.tes-amm.com/_Content/af-ZA/)
- [South Korea](https://microsoft-hub.tes-amm.com/_Content/ko-KR/)
- [Spain](https://microsoft-hub.tes-amm.com/_Content/es-ES/)
- [Sweden](https://microsoft-hub.tes-amm.com/_Content/sv-SE/)
- [Switzerland](https://microsoft-hub.tes-amm.com/_Content/fr-CH/)
- [Taiwan](https://microsoft-hub.tes-amm.com/_Content/zh-TW/)
- [Thailand](https://microsoft-hub.tes-amm.com/_Content/th-TH/)
- [United Kingdom](https://microsoft-hub.tes-amm.com/_Content/en-GB/)
- [United States](https://microsoft-hub.tes-amm.com/_Content/en-US/)

> [!TIP]
> Since both cartridges appear almost identical, we added two bumps to the edge of the Surface Hub 3 Compute Cartridge cartridge. These bumps are located on the opposite side of the power socket, helping you differentiate between the two models.

## Wallpaper installation

The latest Windows Bloom wallpaper is available for your Surface Hub 3 device or Pack. To learn more, see [Install wallpaper on Surface Hub running Microsoft Teams Rooms on Windows](install-wallpaper-surface-hub.md).

### Learn more

- [Surface Hub 3 Compute Cartridge FAQ](surface-hub-3-compute-cartridge-faq.md)
