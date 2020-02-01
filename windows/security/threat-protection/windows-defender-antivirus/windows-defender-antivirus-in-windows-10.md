---
title: Next-generation protection in Windows 10 and Windows Server 2016
description: Learn how to manage, configure, and use Windows Defender AV, the built-in antimalware and antivirus product available in Windows 10 and Windows Server 2016
keywords: windows defender antivirus, windows defender, antimalware, scep, system center endpoint protection, system center configuration manager, virus, malware, threat, detection, protection, security
search.product: eADQiWindows 10XVcnh
ms.pagetype: security
ms.prod: w10
ms.mktglfcycl: manage
ms.sitesec: library
ms.pagetype: security
ms.localizationpriority: medium
author: denisebmsft
ms.author: deniseb
ms.date: 12/17/2019
ms.reviewer: 
manager: dansimp
ms.custom: nextgen
---

# Next-generation protection in Windows 10 and Windows Server 2016

**Applies to:**

- [Windows Defender Advanced Threat Protection (Windows Defender ATP)](https://go.microsoft.com/fwlink/p/?linkid=2069559)

Windows Defender Antivirus is the next-generation protection component of Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP). Next-generation protection brings together machine learning, big-data analysis, in-depth threat resistance research, and cloud infrastructure to protect devices in your enterprise organization. Next-generation protection services include:

- [Behavior-based, heuristic, and real-time antivirus protection](configure-protection-features-windows-defender-antivirus.md). This includes always-on scanning using file and process behavior monitoring and other heuristics (also known as "real-time protection"). It also includes detecting and blocking apps that are deemed unsafe, but may not be detected as malware.
- [Cloud-delivered protection](utilize-microsoft-cloud-protection-windows-defender-antivirus.md). This includes near-instant detection and blocking of new and emerging threats.
- [Dedicated protection and product updates](manage-updates-baselines-windows-defender-antivirus.md). This includes updates related to keeping Windows Defender Antivirus up to date.

>[!TIP]
>Visit the [Microsoft Defender ATP demo website](https://demo.wd.microsoft.com?ocid=cx-wddocs-testground) to confirm the following protection features are working and explore them using demo scenarios:
> - Cloud-delivered protection
> - Block at first sight (BAFS) protection
> - Potentially unwanted applications (PUA) protection

## Minimum system requirements

Windows Defender Antivirus is your main vehicle for next-generation protection, and it has the same hardware requirements as of Windows 10. For more information, see:

- [Minimum hardware requirements](https://docs.microsoft.com/windows-hardware/design/minimum/minimum-hardware-requirements-overview)
- [Hardware component guidelines](https://docs.microsoft.com/windows-hardware/design/component-guidelines/components)

## Configure next-generation protection services

For information on how to configure next-generation protection services, see [Configure Windows Defender Antivirus features](configure-windows-defender-antivirus-features.md).

> [!Note]  
> Configuration and management is largely the same in Windows Server 2016, while running Windows Defender Antivirus; however, there are some differences. To learn more, see [Windows Defender Antivirus on Windows Server 2016](windows-defender-antivirus-on-windows-server-2016.md).

## Related topics

- [Full version history for Microsoft Defender Advanced Threat Protection](../microsoft-defender-atp/whats-new-in-microsoft-defender-atp.md)
- [Windows Defender Antivirus management and configuration](configuration-management-reference-windows-defender-antivirus.md)
- [Evaluate Windows Defender Antivirus protection](evaluate-windows-defender-antivirus.md)
- [Enable cloud protection](enable-cloud-protection-windows-defender-antivirus.md)
- [Configure real-time protection](configure-real-time-protection-windows-defender-antivirus.md)
- [Enable block at first sight](configure-block-at-first-sight-windows-defender-antivirus.md)
- [Detect and block potentially unwanted applications](detect-block-potentially-unwanted-apps-windows-defender-antivirus.md)
- [Create and deploy cloud-protected antimalware policies](https://docs.microsoft.com/sccm/protect/deploy-use/endpoint-antimalware-policies#cloud-protection-service.md)
