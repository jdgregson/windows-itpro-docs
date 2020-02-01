---
title: Protect security settings with tamper protection
ms.reviewer: 
manager: dansimp
description: Use tamper protection to prevent malicious apps from changing important security settings.
keywords: malware, defender, antivirus, tamper protection
search.product: eADQiWindows 10XVcnh
ms.pagetype: security
ms.prod: w10
ms.mktglfcycl: manage
ms.sitesec: library
ms.pagetype: security
ms.localizationpriority: medium
audience: ITPro
author: denisebmsft
ms.author: deniseb
ms.custom: nextgen
---

# Protect security settings with tamper protection

**Applies to:**

- Windows 10

## Overview

During some kinds of cyber attacks, bad actors try to disable security features, such as anti-virus protection, on your machines. They do this to get easier access to your data, to install malware, or to otherwise exploit your data, identity, and devices. Tamper protection helps prevent this from occurring. 

With tamper protection, malicious apps are prevented from taking actions like these:
- Disabling virus and threat protection
- Disabling real-time protection
- Turning off behavior monitoring
- Disabling antivirus (such as IOfficeAntivirus (IOAV))
- Disabling cloud-delivered protection
- Removing security intelligence updates

Tamper protection now integrates with [Threat & Vulnerability Management](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/next-gen-threat-and-vuln-mgt). Security recommendations include a check to make sure tamper protection is turned on.

![Tamper protection results in security recommendations](../images/securityrecs-tamperprotect.jpg)

In the results, you can select **Turn on Tamper Protection** to learn more and turn it on.

![Turn on tamper protection](images/turnontamperprotection.png)

## How it works

 Tamper protection essentially locks Windows Defender Antivirus and prevents your security settings from being changed through apps and methods like these:
- Configuring settings in Registry Editor on your Windows machine 
- Changing settings through PowerShell cmdlets
- Editing or removing security settings through group policies
- and so on.

Tamper protection doesn't prevent you from viewing your security settings. And, tamper protection doesn't affect how third-party antivirus apps register with the Windows Security app. If your organization is using Windows 10 Enterprise E5, individual users can't change the tamper protection setting; this is managed by your security team.

### What do you want to do?

[Turn tamper protection on (or off) for an individual machine using Windows Security](#turn-tamper-protection-on-or-off-for-an-individual-machine)

[Turn tamper protection on (or off) for your organization using Intune](#turn-tamper-protection-on-or-off-for-your-organization-using-intune)

## Turn tamper protection on (or off) for an individual machine

> [!NOTE]
> Tamper protection blocks attempts to modify Windows Defender Antivirus settings through the registry.
> 
> To help ensure that tamper protection doesn’t interfere with third-party security products or enterprise installation scripts that modify these settings, go to **Windows Security** and update **Security intelligence** to version 1.287.60.0 or later. (See [Security intelligence updates](https://www.microsoft.com/wdsi/definitions).)
> 
> Once you’ve made this update, tamper protection will continue to protect your registry settings, and will also log attempts to modify them without returning errors.

If you are a home user, or you are not subject to settings managed by a security team, you can use the Windows Security app to turn tamper protection on or off. You must have appropriate admin permissions on your machine to perform the following task.

1. Click **Start**, and start typing *Defender*. In the search results, select **Windows Security**.

2. Select **Virus & threat protection** > **Virus & threat protection settings**.

3. Set **Tamper Protection** to **On** or **Off**.

## Turn tamper protection on (or off) for your organization using Intune

If you are part of your organization's security team, you can turn tamper protection on (or off) for your organization in the Microsoft 365 Device Management portal (Intune). (This feature is rolling out now; if you don't have it yet, you should very soon, assuming your organization has [Microsoft Defender Advanced Threat Protection](../microsoft-defender-atp/whats-new-in-microsoft-defender-atp.md) (Microsoft Defender ATP) and that you meet the prerequisites listed below.) 

You must have appropriate [permissions](../microsoft-defender-atp/assign-portal-access.md), such as global admin, security admin, or security operations, to perform the following task. 

1. Make sure your organization meets all of the following requirements:

    - Your organization must have [Microsoft Defender ATP E5](https://www.microsoft.com/microsoft-365/windows/microsoft-defender-atp) (this is included in Microsoft 365 E5. See [Microsoft 365 Enterprise overview](https://docs.microsoft.com/microsoft-365/enterprise/microsoft-365-overview) for more details.)
    - Your organization's devices must be managed by [Intune](https://docs.microsoft.com/intune/device-management-capabilities).
    - Your Windows machines must be running [Windows OS 1709](https://docs.microsoft.com/windows/release-information/status-windows-10-1709) or later.
    - You must be using Windows security with [security intelligence](https://www.microsoft.com/wdsi/definitions) updated to version 1.287.60.0 (or above)
    - Your machines must be using anti-malware platform version 4.18.1906.3 (or above) and anti-malware engine version 1.1.15500.X (or above). (See [Manage Windows Defender Antivirus updates and apply baselines](manage-updates-baselines-windows-defender-antivirus.md).)

2. Go to the Microsoft 365 Device Management portal ([https://devicemanagement.microsoft.com](https://devicemanagement.microsoft.com)) and sign in with your work or school account. 

3. Select **Device configuration** > **Profiles**.

4. Create a profile that includes the following settings:

    - **Platform**: Windows 10 and later

    - **ProfileType**: Endpoint protection
    
    - **Settings** > Windows Defender Security Center > Tamper Protection 

5. Assign the profile to one or more groups.

### Are you using Windows OS 1709?

If you are using Windows OS 1709, you don't have the Windows Security app on your computer. In this case, the one of the following procedures to determine whether tamper protection is enabled.

#### To determine whether tamper protection is turned on by using PowerShell

1. Open the Windows PowerShell app.

2. Use the [Get-MpComputerStatus](https://docs.microsoft.com/powershell/module/defender/get-mpcomputerstatus?view=win10-ps) PowerShell cmdlet.

3. In the list of results, look for `IsTamperProtected`. (A value of *true* means tamper protection is enabled.)

#### To determine whether tamper protection is turned on by viewing a registry key

1. Open the Registry Editor app.

2. Go to **HKEY_LOCAL_MACHINE** > **SOFTWARE** > **Microsoft** > **Windows Defender** > **Features**.

3. Look for an entry of **TamperProtection** of type **REG_DWORD**, with a value of **0x5**.<br/>
    - If you see **TamperProtection** with a value of **0**, tamper protection is not turned on. 
    - If you do not see **TamperProtection** at all, tamper protection is not turned on.  

## Frequently asked questions

### To which Windows OS versions is configuring tamper protection is applicable?

[Windows 1709](https://docs.microsoft.com/windows/release-information/status-windows-10-1709) or later together with [Microsoft Defender Advanced Threat Protection E5](https://www.microsoft.com/microsoft-365/windows/microsoft-defender-atp).

### Is configuring tamper protection in Intune supported on servers?

No

### Will tamper protection have any impact on third party antivirus registration?

No, third-party antivirus will continue to register with the Windows Security application.

### What happens if Windows Defender Antivirus is not active on a device?

Tamper protection will not have any impact on such devices.

### How can I turn tamper protection on/off?

If you are a home user, see [Turn tamper protection on (or off) for an individual machine](#turn-tamper-protection-on-or-off-for-an-individual-machine).

If you are an organization using [Microsoft Defender ATP E5](https://www.microsoft.com/microsoft-365/windows/microsoft-defender-atp), you should be able to manage tamper protection in Intune similar to how you manage other endpoint protection features. See [Turn tamper protection on (or off) for your organization using Intune](#turn-tamper-protection-on-or-off-for-your-organization-using-intune).

 
### How does configuring tamper protection in Intune affect how I manage Windows Defender Antivirus through my group policy?

Your regular group policy doesn’t apply to tamper protection, and changes to Windows Defender Antivirus settings will be ignored when tamper protection is on.


>[!NOTE]
>A small delay in Group Policy (GPO) processing may occur if Group Policy settings include values that control Windows Defender Antivirus features protected by tamper protection. To avoid any potential delays, we recommend that you remove settings that control Windows Defender Antivirus related behavior from GPO and simply allow tamper protection to protect Windows Defender Antivirus settings. <br><br>
> Sample Windows Defender Antivirus settings:<br>
> Turn off Windows Defender Antivirus <br>
> Computer Configuration\Administrative Templates\Windows Components\Windows Defender\
Value DisableAntiSpyware = 0 <br><br>
>Turn off real-time protection<br>
Computer Configuration\Administrative Templates\Windows Components\Windows Defender Antivirus\Real-time Protection\
Value DisableRealtimeMonitoring = 0


### For Microsoft Defender ATP E5, is configuring tamper protection in Intune targeted to the entire organization only?

Configuring tamper protection in Intune can be targeted to your entire organization as well as to devices and user groups with Intune.

### Can I configure tamper protection in System Center Configuration Manager?

Currently we do not have support to manage tamper protection through System Center Configuration Manager.

### I have the Windows E3 enrollment. Can I use configuring tamper protection in Intune?

Currently, configuring tamper protection in Intune is only available for customers who have [Microsoft Defender Advanced Threat Protection E5](https://www.microsoft.com/microsoft-365/windows/microsoft-defender-atp).

### What happens if I try to change Microsoft Defender ATP settings in Intune, System Center Configuration Manager, and Windows Management Instrumentation when tamper protection is enabled on a device?

You won’t be able to change the features that are protected by tamper protection; those change requests are ignored.

### I’m an enterprise customer. Can local admins change tamper protection on their devices?

No. Local admins cannot change or modify tamper protection settings.

### What happens if my device is onboarded with Microsoft Defender ATP and then goes into an off-boarded state?

In this case, tamper protection status changes, and this feature is no longer applied.

### Will there be an alert about tamper protection status changing in the Microsoft Defender Security Center?

Yes. The alert is shown in [https://securitycenter.microsoft.com](https://securitycenter.microsoft.com) under **Alerts**. 

In addition, your security operations team can use hunting queries, such as the following:

`AlertEvents | where Title == "Tamper Protection bypass"`

### Will there be a group policy setting for tamper protection?

No.

## Related resources

[Windows 10 Enterprise Security](https://docs.microsoft.com/windows/security/index)

[Help secure Windows PCs with Endpoint Protection for Microsoft Intune](https://docs.microsoft.com/intune/help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune)

[Microsoft 365 Enterprise overview (at a glance)](https://docs.microsoft.com/microsoft-365/enterprise/microsoft-365-overview#at-a-glance)

[Microsoft Defender ATP E5](https://www.microsoft.com/microsoft-365/windows/microsoft-defender-atp)
