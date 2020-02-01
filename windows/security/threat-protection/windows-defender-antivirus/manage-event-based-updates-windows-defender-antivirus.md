---
title: Apply Windows Defender Antivirus updates after certain events
description: Manage how Windows Defender Antivirus applies security intelligence updates after startup or receiving cloud-delivered detection reports.
keywords: updates, protection, force updates, events, startup, check for latest, notifications
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
ms.date: 09/03/2018
ms.reviewer: 
manager: dansimp
---

# Manage event-based forced updates

**Applies to:**

- [Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP)](https://go.microsoft.com/fwlink/p/?linkid=2069559)

Windows Defender Antivirus allows you to determine if updates should (or should not) occur after certain events, such as at startup or after receiving specific reports from the cloud-delivered protection service.

## Check for protection updates before running a scan

You can use System Center Configuration Manager, Group Policy, PowerShell cmdlets, and WMI to force Windows Defender Antivirus to check and download protection updates before running a scheduled scan.

### Use Configuration Manager to check for protection updates before running a scan

1. On your System Center Configuration Manager console, open the antimalware policy you want to change (click **Assets and Compliance** in the navigation pane on the left, then expand the tree to **Overview** > **Endpoint Protection** > **Antimalware Policies**)

2. Go to the **Scheduled scans** section and set **Check for the latest security intelligence updates before running a scan** to **Yes**.

3. Click **OK**.

4. [Deploy the updated policy as usual](https://docs.microsoft.com/sccm/protect/deploy-use/endpoint-antimalware-policies#deploy-an-antimalware-policy-to-client-computers).

### Use Group Policy to check for protection updates before running a scan

1. On your Group Policy management machine, open the [Group Policy Management Console](https://docs.microsoft.com/previous-versions/windows/desktop/gpmc/group-policy-management-console-portal), right-click the Group Policy Object you want to configure and click **Edit**.

2. Using the **Group Policy Management Editor** go to **Computer configuration**.

3. Click **Policies** then **Administrative templates**.

4. Expand the tree to **Windows components** > **Windows Defender Antivirus** > **Scan**.

5. Double-click **Check for the latest virus and spyware definitions before running a scheduled scan** and set the option to **Enabled**.

6. Click **OK**.

### Use PowerShell cmdlets to check for protection updates before running a scan

Use the following cmdlets:

```PowerShell
Set-MpPreference -CheckForSignaturesBeforeRunningScan
```

For more information, see [Use PowerShell cmdlets to configure and run Windows Defender Antivirus](use-powershell-cmdlets-windows-defender-antivirus.md) and [Defender cmdlets](https://docs.microsoft.com/powershell/module/defender/index).

### Use Windows Management Instruction (WMI) to check for protection updates before running a scan

Use the [**Set** method of the **MSFT_MpPreference**](https://msdn.microsoft.com/library/dn455323(v=vs.85).aspx) class for the following properties:

```WMI
CheckForSignaturesBeforeRunningScan
```

For more information, see [Windows Defender WMIv2 APIs](https://docs.microsoft.com/previous-versions/windows/desktop/defender/windows-defender-wmiv2-apis-portal).

## Check for protection updates on startup

You can use Group Policy to force Windows Defender Antivirus to check and download protection updates when the machine is started.

1. On your Group Policy management computer, open the [Group Policy Management Console](https://docs.microsoft.com/previous-versions/windows/desktop/gpmc/group-policy-management-console-portal), right-click the Group Policy Object you want to configure and click **Edit**.

2. Using the **Group Policy Management Editor** go to **Computer configuration**.

3. Click **Policies** then **Administrative templates**.

4. Expand the tree to **Windows components** > **Windows Defender Antivirus** > **Signature Updates**.

5. Double-click **Check for the latest virus and spyware definitions on startup** and set the option to **Enabled**. 

6. Click **OK**.

You can also use Group Policy, PowerShell, or WMI to configure Windows Defender Antivirus to check for updates at startup even when it is not running.

### Use Group Policy to download updates when Windows Defender Antivirus is not present

1. On your Group Policy management machine, open the [Group Policy Management Console](https://docs.microsoft.com/previous-versions/windows/desktop/gpmc/group-policy-management-console-portal), right-click the Group Policy Object you want to configure and click **Edit**.

2. Using the **Group Policy Management Editor**, go to **Computer configuration**.

3. Click **Policies** then **Administrative templates**.

4. Expand the tree to **Windows components** > **Windows Defender Antivirus** > **Security Intelligence Updates**.

5. Double-click **Initiate security intelligence update on startup** and set the option to **Enabled**.

6. Click **OK**.

### Use PowerShell cmdlets to download updates when Windows Defender Antivirus is not present

Use the following cmdlets:

```PowerShell
Set-MpPreference -SignatureDisableUpdateOnStartupWithoutEngine
```

For more information, see [Use PowerShell cmdlets to manage Windows Defender Antivirus](use-powershell-cmdlets-windows-defender-antivirus.md) and [Defender cmdlets](https://docs.microsoft.com/powershell/module/defender/index) for more information on how to use PowerShell with Windows Defender Antivirus.

### Use Windows Management Instruction (WMI) to download updates when Windows Defender Antivirus is not present

Use the [**Set** method of the **MSFT_MpPreference**](https://docs.microsoft.com/previous-versions/windows/desktop/legacy/dn455323(v=vs.85)) class for the following properties:

```WMI
SignatureDisableUpdateOnStartupWithoutEngine
```

For more information, see [Windows Defender WMIv2 APIs](https://docs.microsoft.com/previous-versions/windows/desktop/defender/windows-defender-wmiv2-apis-portal).

<a id="cloud-report-updates"></a>

## Allow ad hoc changes to protection based on cloud-delivered protection

Windows Defender AV can make changes to its protection based on cloud-delivered protection. Such changes can occur outside of normal or scheduled protection updates.

If you have enabled cloud-delivered protection, Windows Defender AV will send files it is suspicious about to the Windows Defender cloud. If the cloud service reports that the file is malicious, and the file is detected in a recent protection update, you can use Group Policy to configure Windows Defender AV to automatically receive that protection update. Other important protection updates can also be applied.

### Use Group Policy to automatically download recent updates based on cloud-delivered protection

1. On your Group Policy management machine, open the [Group Policy Management Console](https://docs.microsoft.com/previous-versions/windows/desktop/gpmc/group-policy-management-console-portal), right-click the Group Policy Object you want to configure and click **Edit**.

2. Using the **Group Policy Management Editor** go to **Computer configuration**.

3. Click **Policies** then **Administrative templates**.

4. Expand the tree to **Windows components** > **Windows Defender Antivirus** > **Signature Updates**.

5. Double-click **Allow real-time security intelligence updates based on reports to Microsoft MAPS** and set the option to **Enabled**. Then click **OK**.

6. **Allow notifications to disable definitions-based reports to Microsoft MAPS** and set the option to **Enabled**. Then click **OK**.
    
> [!NOTE]
> "Allow notifications to disable definitions based reports" enables Microsoft MAPS to disable those definitions known to cause false-positive reports. You must configure your computer to join Microsoft MAPS for this function to work.

## Related articles

- [Deploy Windows Defender Antivirus](deploy-manage-report-windows-defender-antivirus.md)
- [Manage Windows Defender Antivirus updates and apply baselines](manage-updates-baselines-windows-defender-antivirus.md)
- [Manage when protection updates should be downloaded and applied](manage-protection-update-schedule-windows-defender-antivirus.md)
- [Manage updates for endpoints that are out of date](manage-outdated-endpoints-windows-defender-antivirus.md)
- [Manage updates for mobile devices and virtual machines (VMs)](manage-updates-mobile-devices-vms-windows-defender-antivirus.md)
- [Windows Defender Antivirus in Windows 10](windows-defender-antivirus-in-windows-10.md)
