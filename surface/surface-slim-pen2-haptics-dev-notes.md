---
title: Surface Slim Pen (2nd Edition) haptics developer notes
description: Guidance for developers on implementing haptics in Windows 11 Ink apps with customizable inking and interaction feedback features.
ms.service: windows-11
ms.localizationpriority: medium
author: coveminer
ms.author: chauncel
ms.topic: how-to
ms.date: 10/30/2024
ms.reviewer: gusing
manager: frankbu
appliesto:
- Windows 11
---

# Surface Slim Pen (2nd Edition) haptics developer notes

This page provides implementation notes for developers building apps that extend the **Windows 11 Ink** capabilities of the [Surface Slim Pen (2nd Edition) for Business](https://www.microsoft.com/d/surface-slim-pen-2-for-business/8mjc4rmvltj0?). Customizable haptics features include:

- **Inking feedback:** Simulates the feel of different tools, such as pens, pencils, and brushes, during writing or drawing.
- **Interaction feedback:** Provides tactile responses to user actions, such as hovering over buttons, clicking, or completing tasks with the pen.

If you are customizing haptics for the Slim Pen (2nd Edition), begin by consulting the **Windows Ink guidelines** in [Pen interactions and haptic feedback](/windows/apps/design/input/pen-haptics), and then review the implementation notes below.

---

## Implementation notes

Surface Slim Pen (2nd Edition) aligns with the Windows Ink guidelines, with the following considerations and exceptions:

###  Interaction waveforms and interruptions
As explained in the [Send and stop interaction feedback](/windows/apps/design/input/pen-haptics#send-and-stop-interaction-feedback) section, interaction waveforms temporarily interrupt inking waveforms. However, in the Slim Pen (2nd Edition), the **inking waveform might not automatically resume** after an interaction feedback completes. 

- **Recommendation:** If continuous inking feedback is needed, re-enable the inking waveform immediately after the interaction feedback stops. There is no need to wait for the interaction feedback to finish before reactivating the inking waveform.

### Unsupported haptic feedback features
The following optional haptic features, described in the [Haptic feedback customizations](/windows/apps/design/input/pen-haptics#haptic-feedback-customizations) section, are **not supported** on the Slim Pen (2nd Edition):

- **Play Count:** The number of times a haptic effect plays.  
- **Replay Pause Interval:** The delay between replays of a haptic effect.  
- **Play Duration:** The total length of time the effect is active.

Although these features appear in the descriptor, the following functions will return incorrect values:

- `IsPlayCountSupported`
- `IsPlayDurationSupported`
- `IsReplayPauseIntervalSupported`

Developers should avoid relying on these functions when building apps with Slim Pen (2nd Edition) haptics.

---

## Learn more

- [Pen interactions and Windows Ink in Windows apps](/windows/apps/design/input/pen-and-stylus-interactions)  
- [Surface Slim Pen (2nd Edition) for Business](https://www.microsoft.com/d/surface-slim-pen-2-for-business/8mjc4rmvltj0?)  
- [Surface pen features and compatibility](https://support.microsoft.com/surface/identify-your-surface-pen-and-features-c82a0208-2e35-b347-dae0-d7f4922edc77)  
