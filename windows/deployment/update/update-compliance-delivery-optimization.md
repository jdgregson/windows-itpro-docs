---
title: Delivery Optimization in Update Compliance (Windows 10)
ms.reviewer: 
manager: laurawi
description: new Delivery Optimization data displayed in Update Compliance
ms.prod: w10
ms.mktglfcycl: deploy
ms.pagetype: deploy
audience: itpro
author: jaimeo
ms.author: jaimeo
keywords: oms, operations management suite, optimization, downloads, updates, log analytics
ms.localizationpriority: medium
ms.collection: M365-analytics
ms.topic: article
---

# Delivery Optimization in Update Compliance
![DO status](images/UC_workspace_DO_status.png)
The Update Compliance solution of Windows Analytics provides you with information about your Delivery Optimization configuration, including the observed bandwidth savings across all devices that used peer-to-peer distribution over the past 28 days.

## Delivery Optimization Status
 
The Delivery Optimization Status section includes three blades:

- The **Device Configuration** blade shows a breakdown of download configuration for each device
- The **Content Distribution (%)** blade shows the percentage of bandwidth savings for each category
- The **Content Distribution (GB)** blade shows the total amount of data seen from each content type broken down by the download source (peers vs non-peers).

 
## Device Configuration blade
Devices can be set to use different download modes; these download modes determine in what situations Delivery Optimization will use peer-to-peer distribution to accomplish the downloads. The top section shows the number of devices configured to use peer-to-peer distribution in *Peering On* compared to *Peering Off* modes. The table shows a breakdown of the various download mode configurations seen in your environment. For more information about the different configuration options, see [Configure Delivery Optimization for Windows 10 updates](waas-delivery-optimization-setup.md).
 
## Content Distribution (%) blade
The first of two blades showing information on content breakdown, this blade shows a ring chart summarizing **Bandwidth Savings %**, which is the percentage of data received from peer sources out of the total data downloaded (for any device that used peer-to-peer distribution).
The table breaks down the Bandwidth Savings % into specific content categories along with the number of devices seen downloading the given content type that used peer-to-peer distribution.
 
## Content Distribution (GB) blade
The second of two blades showing information on content breakdown, this blade shows a ring chart summarizing the total bytes downloaded by using peer-to-peer distribution compared to HTTP distribution. 
The table breaks down the number of bytes from each download source into specific content categories, along with the number of devices seen downloading the given content type that used peer-to-peer distribution.

The download sources that could be included are:
- LAN Bytes: Bytes downloaded from LAN Peers which are other devices on the same local network
- Group Bytes: Bytes downloaded from Group Peers which are other devices that belong to the same Group (available when the “Group” download mode is used)
- HTTP Bytes: Non-peer bytes. The HTTP download source can be Microsoft Servers, Windows Update Servers, a WSUS server or an SCCM Distribution Point for Express Updates. 
