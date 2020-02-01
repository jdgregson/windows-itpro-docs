---
title: Application Control for Windows
description: Application Control restricts which applications users are allowed to run and the code that runs in the system core.
keywords: whitelisting, security, malware
ms.assetid: 8d6e0474-c475-411b-b095-1c61adb2bdbb
ms.prod: w10
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: security
ms.localizationpriority: medium
audience: ITPro
ms.collection: M365-security-compliance
author: denisebmsft
ms.reviewer: isbrahm
ms.author: deniseb
manager: dansimp
ms.date: 01/08/2019
ms.custom: asr
---

# Application Control

**Applies to:**

-   Windows 10
-   Windows Server 2016
-   Windows Server 2019 

With thousands of new malicious files created every day, using traditional methods like antivirus solutions—signature-based detection to fight against malware—provides an inadequate defense against new attacks.

In most organizations, information is the most valuable asset, and ensuring that only approved users have access to that information is imperative. However, when a user runs a process, that process has the same level of access to data that the user has. As a result, sensitive information could easily be deleted or transmitted out of the organization if a user knowingly or unknowingly runs malicious software.

Application control can help mitigate these types of security threats by restricting the applications that users are allowed to run and the code that runs in the System Core (kernel). Application control policies can also block unsigned scripts and MSIs, and restrict Windows PowerShell to run in [Constrained Language Mode](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_language_modes).

Application control is a crucial line of defense for protecting enterprises given today’s threat landscape, and it has an inherent advantage over traditional antivirus solutions. Specifically, application control moves away from an application trust model where all applications are assumed trustworthy to one where applications must earn trust in order to run. Many organizations, like the Australian Signals Directorate, understand this and frequently cite application control as one of the most effective means for addressing the threat of executable file-based malware (.exe, .dll, etc.).

> [!NOTE]
> Although application control can significantly harden your computers against malicious code, we recommend that you continue to maintain an enterprise antivirus solution for a well-rounded enterprise security portfolio.

Windows 10 includes two technologies that can be used for application control depending on your organization's specific scenarios and requirements:<br>
-   **Windows Defender Application Control**; and
-   **AppLocker**

## Windows Defender Application Control

Windows Defender Application Control (WDAC) was introduced with Windows 10 and allows organizations to control what drivers and applications are allowed to run on their Windows 10 clients. WDAC was designed as a security feature under the [servicing criteria](https://www.microsoft.com/msrc/windows-security-servicing-criteria) defined by the Microsoft Security Response Center (MSRC).

> [!NOTE]
> Prior to Windows 10, version 1709, Windows Defender Application Control was known as configurable code integrity policies.

WDAC policies apply to the managed computer as a whole and affects all users of the device. WDAC rules can be defined based on:
-   Attributes of the codesigning certificate(s) used to sign an app and its binaries;
-   Attributes of the app's binaries that come from the signed metadata for the files, such as Original Filename and version, or the hash of the file;
-   The reputation of the app as determined by Microsoft's Intelligent Security Graph;
-   The identity of the process that initiated the installation of the app and its binaries (managed installer);
-   The path from which the app or file is launched (beginning with Windows 10 version 1903);
-   The process that launched the app or binary.

### WDAC System Requirements

WDAC policies can only be created on computers beginning with Windows 10 Enterprise or Windows Server 2016 and above.
They can be applied to computers running any edition of Windows 10 or Windows Server 2016 and optionally managed via Mobile Device Management (MDM), such as Microsoft Intune.
Group Policy can also be used to deploy WDAC policies to Windows 10 Enterprise edition or Windows Server 2016 and above.

## AppLocker

AppLocker was introduced with Windows 7 and allows organizations to control what applications their users are allowed to run on their Windows clients. AppLocker provides security value as a defense in depth feature and helps end users avoid running unapproved software on their computers.

AppLocker policies can apply to all users on a computer or to individual users and groups. AppLocker rules can be defined based on:
-   Attributes of the codesigning certificate(s) used to sign an app and its binaries;
-   Attributes of the app's binaries that come from the signed metadata for the files, such as Original Filename and version, or the hash of the file;
-   The path from which the app or file is launched (beginning with Windows 10 version 1903).

### AppLocker System Requirements

AppLocker policies can only be configured on and applied to computers that are running on the supported versions and editions of the Windows operating system. For more info, see [Requirements to Use AppLocker](applocker/requirements-to-use-applocker.md). 
AppLocker policies can be deployed using Group Policy or MDM.

## Choose when to use WDAC or AppLocker

Although either AppLocker or WDAC can be used to control application execution on Windows 10 clients, the following factors can help you decide when to use each of the technologies. 

### WDAC is best when:

-   You are adopting application control primarily for security reasons.
-   Your application control policy can be applied to all users on the managed computers.
-   All of the devices you wish to manage are running Windows 10.

### AppLocker is best when:

-   You have a mixed Windows operating system (OS) environment and need to apply the same policy controls to Windows 10 and earlier versions of the OS.
-   You need to apply different policies for different users or groups on a shared computer.
-   You are using application control to help users avoid running unapproved software, but you do not require a solution designed as a security feature.
-   You do not wish to enforce application control on application files such as DLLs or drivers.

## When to use both WDAC and AppLocker together

AppLocker can also be deployed as a complement to WDAC to add user- or group-specific rules for shared device scenarios where its important to prevent some users from running specific apps.
As a best practice, you should enforce WDAC at the most restrictive level possible for your organization, and then you can use AppLocker to fine-tune the restrictions to an even lower level.

## See also

- [WDAC design guide](windows-defender-application-control-design-guide.md)
- [WDAC deployment guide](windows-defender-application-control-deployment-guide.md)
- [AppLocker overview](applocker/applocker-overview.md)
