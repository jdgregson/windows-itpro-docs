---
title: Enforce Windows Defender Application Control (WDAC) policies (Windows 10)
description: Learn how to test a Windows Defender Application Control (WDAC) policy in enforced mode by following these steps in an elevated Windows PowerShell session.
keywords: whitelisting, security, malware
ms.assetid: 8d6e0474-c475-411b-b095-1c61adb2bdbb
ms.prod: w10
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: security
ms.localizationpriority: medium
audience: ITPro
ms.collection: M365-security-compliance
author: jsuther1974
ms.reviewer: isbrahm
ms.author: dansimp
manager: dansimp
ms.date: 05/03/2018
---

# Enforce Windows Defender Application Control policies

**Applies to:**

-   Windows 10
-   Windows Server 2016

Every WDAC policy is created with audit mode enabled. After you have successfully deployed and tested a WDAC policy in audit mode and are ready to test the policy in enforced mode, complete the following steps in an elevated Windows PowerShell session:

> [!NOTE]
> Every WDAC policy should be tested in audit mode first. For information about how to audit WDAC policies, see [Audit Windows Defender Application Control policies](audit-windows-defender-application-control-policies.md), earlier in this topic.

1. Initialize the variables that will be used:

   `$CIPolicyPath=$env:userprofile+"\Desktop\"`

   `$InitialCIPolicy=$CIPolicyPath+"InitialScan.xml"`

   `$EnforcedCIPolicy=$CIPolicyPath+"EnforcedPolicy.xml"`

   `$CIPolicyBin=$CIPolicyPath+"EnforcedDeviceGuardPolicy.bin"`

   > [!NOTE]
   > The initial WDAC policy that this section refers to was created in the [Create a Windows Defender Application Control policy from a reference computer](create-initial-default-policy.md) section. If you are using a different WDAC policy, update the **CIPolicyPath** and **InitialCIPolicy** variables.

2. Ensure that rule options 9 (“Advanced Boot Options Menu”) and 10 (“Boot Audit on Failure”) are set the way that you intend for this policy. We strongly recommend that you enable these rule options before you run any enforced policy for the first time. Enabling these options provides administrators with a pre-boot command prompt, and allows Windows to start even if the WDAC policy blocks a kernel-mode driver from running. When ready for enterprise deployment, you can remove these options.

    To ensure that these options are enabled in a policy, use [Set-RuleOption](https://docs.microsoft.com/powershell/module/configci/set-ruleoption) as shown in the following commands. You can run these commands even if you're not sure whether options 9 and 10 are already enabled—if so, the commands have no effect.
    
    `Set-RuleOption -FilePath $InitialCIPolicy -Option 9`
    
    `Set-RuleOption -FilePath $InitialCIPolicy -Option 10`

3. Copy the initial file to maintain an original copy:

   `copy $InitialCIPolicy $EnforcedCIPolicy`

4. Use Set-RuleOption to delete the audit mode rule option:

   `Set-RuleOption -FilePath $EnforcedCIPolicy -Option 3 -Delete`

   > [!NOTE]
   > To enforce a WDAC policy, you delete option 3, the **Audit Mode Enabled** option. There is no “enforced” option that can be placed in a WDAC policy.

5. Use [ConvertFrom-CIPolicy](https://docs.microsoft.com/powershell/module/configci/convertfrom-cipolicy) to convert the new WDAC policy to binary format:

   `ConvertFrom-CIPolicy $EnforcedCIPolicy $CIPolicyBin`

Now that this policy is in enforced mode, you can deploy it to your test computers. Rename the policy to SIPolicy.p7b and copy it to C:\\Windows\\System32\\CodeIntegrity for testing, or deploy the policy through Group Policy by following the instructions in [Deploy and manage Windows Defender Application Control with Group Policy](deploy-windows-defender-application-control-policies-using-group-policy.md). You can also use other client management software to deploy and manage the policy.
