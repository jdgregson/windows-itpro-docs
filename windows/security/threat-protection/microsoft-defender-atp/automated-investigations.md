---
title: Use automated investigations to investigate and remediate threats
description: Understand the automated investigation flow in Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP).
keywords: automated, investigation, detection, source, threat types, id, tags, machines, duration, filter export
search.product: eADQiWindows 10XVcnh
search.appverid: met150
ms.prod: w10
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: security
ms.author: deniseb
author: denisebmsft
ms.localizationpriority: medium
manager: dansimp
audience: ITPro
ms.collection: M365-security-compliance 
ms.topic: conceptual
---

# Overview of automated investigations

Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) offers a wide breadth of visibility on multiple machines. With this kind of optics, the service generates a multitude of alerts. The volume of alerts generated can be challenging for a typical security operations team to individually address. To address this challenge, Microsoft Defender ATP uses automated investigation and remediation capabilities to significantly reduce the volume of alerts that must be investigated individually. 

The automated investigation feature leverages various inspection algorithms, and processes used by analysts (such as playbooks) to examine alerts and take immediate remediation action to resolve breaches. This significantly reduces alert volume, allowing security operations experts to focus on more sophisticated threats and other high value initiatives. The **Automated investigations** list shows all the investigations that were initiated automatically, and includes details, such as status, detection source, and when the investigation was initiated.

> [!TIP]
> Want to experience Microsoft Defender ATP? [Sign up for a free trial.](https://www.microsoft.com/microsoft-365/windows/microsoft-defender-atp?ocid=docs-wdatp-automated-investigations-abovefoldlink)


## Understand the automated investigation flow

### How the automated investigation starts

When an alert is triggered, a security playbook goes into effect. Depending on the security playbook, an automated investigation can start. For example, suppose a malicious file resides on a machine. When that file is detected, an alert is triggered. The automated investigation process begins. Microsoft Defender ATP checks to see if the malicious file is present on any other machines in the organization. Details from the investigation, including verdicts (Malicious, Suspicious, and Clean) are available during and after the automated investigation.

>[!NOTE]
>Currently, automated investigation only supports the following OS versions:
>- Windows Server 2019
>- Windows 10, version 1709 (OS Build 16299.1085 with [KB4493441](https://support.microsoft.com/help/4493441/windows-10-update-kb4493441)) or later
>- Windows 10, version 1803 (OS Build 17134.704 with [KB4493464](https://support.microsoft.com/help/4493464/windows-10-update-kb4493464)) or later
>- Later versions of Windows 10

### Details of an automated investigation

During and after an automated investigation, you can view details about the investigation. Selecting a triggering alert brings you to the investigation details view where you can pivot from the **Investigation graph**, **Alerts**, **Machines**, **Evidence**, **Entities**, and **Log** tabs.

|Tab |Description |
|--|--|
|**Alerts**| Shows the alert that started the investigation.|
|**Machines** |Shows where the alert was seen.|
|**Evidence** |Shows the entities that were found to be malicious during the investigation.|
|**Entities** |Provides details about each analyzed entity, including a determination for each entity type (*Malicious*, *Suspicious*, or *Clean*). |
|**Log** |Shows the chronological detailed view of all the investigation actions taken on the alert.|
|**Pending actions** |If there are pending actions on the investigation, the **Pending actions** tab will be displayed where you can approve or reject actions. |

> [!IMPORTANT]
> Go to the **Action center** to get an aggregated view all pending actions and manage remediation actions. The **Action center** also acts as an audit trail for all automated investigation actions. 

### How an automated investigation expands its scope

While an investigation is running, any other alerts generated from the machine are added to an ongoing automated investigation until that investigation is completed. In addition, if the same threat is seen on other machines, those machines are added to the investigation.

If an incriminated entity is seen in another machine, the automated investigation process will expand its scope to include that machine, and a general security playbook will start on that machine. If 10 or more machines are found during this expansion process from the same entity, then that expansion action will require an approval and will be seen in the **Pending actions** view.

### How threats are remediated

Depending on how you set up the machine groups and their level of automation, the automated investigation will either require user approval (default) or automatically remediate threats.

You can configure the following levels of automation:

|Automation level | Description|
|---|---|
|No automated response | Machines do not get any automated investigations run on them. |
|Semi - require approval for any remediation | This is the default automation level.<br><br>  An approval is needed for any remediation action. |
|Semi - require approval for non-temp folders remediation | An approval is required on files or executables that are not in temporary folders. <br><br> Files or executables in temporary folders, such as the user's download folder or the user's temp folder, will automatically be remediated if needed.|
|Semi - require approval for core folders remediation | An approval is required on files or executables that are in the operating system directories such as Windows folder and Program files folder. <br><br> Files or executables in all other folders will  automatically be remediated if needed.|
|Full - remediate threats automatically | All remediation actions will be performed automatically.|

> [!TIP]
> For more information on how to configure these automation levels, see [Create and manage machine groups](machine-groups.md).

The default machine group is configured for semi-automatic remediation. This means that any malicious entity that calls for remediation requires an approval and the investigation is added to the **Pending actions** section. This can be changed to fully automatic so that no user approval is needed. 

When a pending action is approved, the entity is then remediated and this new state is reflected in the **Entities** tab of the investigation.

## Next step

- [Learn about the automated investigations dashboard](manage-auto-investigation.md)
