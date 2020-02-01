---
title: Configure and validate Windows Defender Antivirus network connections
description: Configure and test your connection to the Windows Defender Antivirus cloud protection service.
keywords: antivirus, windows defender antivirus, antimalware, security, defender, cloud, aggressiveness, protection level
search.product: eADQiWindows 10XVcnh
ms.pagetype: security
ms.prod: w10
ms.mktglfcycl: manage
ms.sitesec: library
ms.pagetype: security
ms.localizationpriority: medium
author: denisebmsft
ms.author: deniseb
ms.custom: nextgen
ms.date: 10/08/2018
ms.reviewer: 
manager: dansimp
---

# Configure and validate Windows Defender Antivirus network connections

**Applies to:**

- [Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP)](https://go.microsoft.com/fwlink/p/?linkid=2069559)

To ensure Windows Defender Antivirus cloud-delivered protection works properly, you need to configure your network to allow connections between your endpoints and certain Microsoft servers.

This article lists the connections that must be allowed, such as by using firewall rules, and provides instructions for validating your connection. Configuring your protection properly helps ensure that you receive the best value from your cloud-delivered protection services.

See the blog post [Important changes to Microsoft Active Protection Services endpoint](https://techcommunity.microsoft.com/t5/Configuration-Manager-Archive/Important-changes-to-Microsoft-Active-Protection-Service-MAPS/ba-p/274006) for some details about network connectivity.

>[!TIP]
>You can also visit the Microsoft Defender ATP demo website at [demo.wd.microsoft.com](https://demo.wd.microsoft.com?ocid=cx-wddocs-testground) to confirm the following features are working:
>
>- Cloud-delivered protection
>- Fast learning (including block at first sight)
>- Potentially unwanted application blocking

## Allow connections to the Windows Defender Antivirus cloud service

The Windows Defender Antivirus cloud service provides fast, strong protection for your endpoints. Enabling the cloud-delivered protection service is optional, however it is highly recommended because it provides important protection against malware on your endpoints and across your network.

>[!NOTE]
>The Windows Defender Antivirus cloud service is a mechanism for delivering updated protection to your network and endpoints. Although it is called a cloud service, it is not simply protection for files stored in the cloud, rather it uses distributed resources and machine learning to deliver protection to your endpoints at a rate that is far faster than traditional Security intelligence updates.

See [Enable cloud-delivered protection](enable-cloud-protection-windows-defender-antivirus.md) for details on enabling the service with Intune, System Center Configuration Manager, Group Policy, PowerShell cmdlets, or on individual clients in the Windows Security app.

After you've enabled the service, you may need to configure your network or firewall to allow connections between it and your endpoints.

Because your protection is a cloud service, computers must have access to the internet and reach the ATP machine learning services. Do not exclude the URL `*.blob.core.windows.net` from any kind of network inspection. The table below lists the services and their associated URLs. Make sure that there are no firewall or network filtering rules denying access to these URLs, or you may need to create an allow rule specifically for them (excluding the URL `*.blob.core.windows.net`). Below mention URLs are using port 443 for communication.


| **Service**| **Description** |**URL** |
| :--: | :-- | :-- |
| Windows Defender Antivirus cloud-delivered protection service, also referred to as Microsoft Active Protection Service (MAPS)|Used by Windows Defender Antivirus to provide cloud-delivered protection|`*.wdcp.microsoft.com` <br/> `*.wdcpalt.microsoft.com` <br/> `*.wd.microsoft.com`|
| Microsoft Update Service (MU)|	Security intelligence and product updates	|`*.update.microsoft.com`|
|Security intelligence updates Alternate Download Location (ADL)|	Alternate location for Windows Defender Antivirus Security intelligence updates if the installed Security intelligence is out of date (7 or more days behind)|	`*.download.microsoft.com`|
| Malware submission storage|Upload location for files submitted to Microsoft via the Submission form or automatic sample submission	| `ussus1eastprod.blob.core.windows.net` <br/>    `ussus1westprod.blob.core.windows.net` <br/>    `usseu1northprod.blob.core.windows.net` <br/>    `usseu1westprod.blob.core.windows.net` <br/>    `ussuk1southprod.blob.core.windows.net` <br/>    `ussuk1westprod.blob.core.windows.net` <br/>    `ussas1eastprod.blob.core.windows.net` <br/>    `ussas1southeastprod.blob.core.windows.net` <br/>    `ussau1eastprod.blob.core.windows.net` <br/>    `ussau1southeastprod.blob.core.windows.net` |
| Certificate Revocation List (CRL)|Used by Windows when creating the SSL connection to MAPS for updating the CRL	| `https://www.microsoft.com/pkiops/crl/` <br/> `https://www.microsoft.com/pkiops/certs` <br/>   `https://crl.microsoft.com/pki/crl/products` <br/> `https://www.microsoft.com/pki/certs` |
| Symbol Store|Used by Windows Defender Antivirus to restore certain critical files during remediation flows	| `https://msdl.microsoft.com/download/symbols` |
| Universal Telemetry Client| Used by Windows to send client diagnostic data; Windows Defender Antivirus uses this for product quality monitoring purposes	| This update uses SSL (TCP Port 443) to download manifests and upload diagnostic data to Microsoft that uses the following DNS endpoints:   `vortex-win.data.microsoft.com` <br/>   `settings-win.data.microsoft.com`|

## Validate connections between your network and the cloud

After whitelisting the URLs listed above, you can test if you are connected to the Windows Defender Antivirus cloud service and are correctly reporting and receiving information to ensure you are fully protected.

**Use the cmdline tool to validate cloud-delivered protection:**

Use the following argument with the Windows Defender Antivirus command-line utility (`mpcmdrun.exe`) to verify that your network can communicate with the Windows Defender Antivirus cloud service:

```DOS
"%ProgramFiles%\Windows Defender\MpCmdRun.exe" -ValidateMapsConnection
```

> [!NOTE]
> You need to open an administrator-level version of the command prompt. Right-click the item in the Start menu, click **Run as administrator** and click **Yes** at the permissions prompt. This command will only work on Windows 10, version 1703 or higher.

For more information, see [Manage Windows Defender Antivirus with the mpcmdrun.exe commandline tool](command-line-arguments-windows-defender-antivirus.md).

**Attempt to download a fake malware file from Microsoft:**

You can download a sample file that Windows Defender Antivirus will detect and block if you are properly connected to the cloud.

Download the file by visiting the following link:
- https://aka.ms/ioavtest

>[!NOTE]
>This file is not an actual piece of malware. It is a fake file that is designed to test if you are properly connected to the cloud.

If you are properly connected, you will see a warning Windows Defender Antivirus notification:

![Windows Defender Antivirus notification informing the user that malware was found](images/defender/wdav-malware-detected.png)

If you are using Microsoft Edge, you'll also see a notification message:

![Microsoft Edge informing the user that malware was found](images/defender/wdav-bafs-edge.png)

A similar message occurs if you are using Internet Explorer:

![Windows Defender Antivirus notification informing the user that malware was found](images/defender/wdav-bafs-ie.png)

You will also see a detection under **Quarantined threats** in the **Scan history** section in the Windows Security app:

1. Open the Windows Security app by clicking the shield icon in the task bar or searching the start menu for **Defender**.

2. Click the **Virus & threat protection** tile (or the shield icon on the left menu bar) and then the **Scan history** label:

    ![Screenshot of the Scan history label in the Windows Security app](images/defender/wdav-history-wdsc.png)

3. Under the **Quarantined threats** section, click the **See full history** label to see the detected fake malware:

    ![Screenshot of quarantined items in the Windows Security app](images/defender/wdav-quarantined-history-wdsc.png)

>[!NOTE]
>Versions of Windows 10 before version 1703 have a different user interface. See [Windows Defender Antivirus in the Windows Security app](windows-defender-security-center-antivirus.md).

The Windows event log will also show [Windows Defender client event ID 2050](troubleshoot-windows-defender-antivirus.md).

>[!IMPORTANT]
>You will not be able to use a proxy auto-config (.pac) file to test network connections to these URLs. You will need to verify your proxy servers and any network filtering tools manually to ensure connectivity.

## Related articles

- [Windows Defender Antivirus in Windows 10](windows-defender-antivirus-in-windows-10.md)

- [Enable cloud-delivered protection](enable-cloud-protection-windows-defender-antivirus.md)

- [Run an Windows Defender Antivirus scan from the command line](command-line-arguments-windows-defender-antivirus.md) and [Command line arguments](command-line-arguments-windows-defender-antivirus.md)

- [Important changes to Microsoft Active Protection Services endpoint](https://techcommunity.microsoft.com/t5/Configuration-Manager-Archive/Important-changes-to-Microsoft-Active-Protection-Service-MAPS/ba-p/274006) 
