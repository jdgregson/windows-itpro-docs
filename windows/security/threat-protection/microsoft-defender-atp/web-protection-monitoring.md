---
title: Monitoring web browsing security in Microsoft Defender ATP
description: Use web protection in Microsoft Defender ATP to monitor web browsing security
keywords: web protection, web threat protection, web browsing, monitoring, reports, cards, domain list, security, phishing, malware, exploit, websites, network protection, Edge, Internet Explorer, Chrome, Firefox, web browser 
search.product: eADQiWindows 10XVcnh
search.appverid: met150
ms.prod: w10
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: security
ms.author: lomayor
author: lomayor
ms.localizationpriority: medium
manager: dansimp
audience: ITPro
ms.collection: M365-security-compliance 
ms.topic: article
ms.date: 08/30/2019
---

# Monitor web browsing security

>Want to experience Microsoft Defender ATP? [Sign up for a free trial.](https://www.microsoft.com/microsoft-365/windows/microsoft-defender-atp?ocid=docs-wdatp-main-abovefoldlink&rtc=1)

Web protection lets you monitor your organization’s web browsing security through reports under **Reports > Web protection** in the Microsoft Defender Security Center. The report contains cards that provide web threat detection statistics.

- **Web threat protection detections over time** — this trending card displays the number of web threats detected by type during the selected time period (Last 30 days, Last 3 months, Last 6 months)
 
    ![Image of the card showing web threats protection detections over time](images/wtp-blocks-over-time.png)

- **Web threat protection summary** — this card displays the total web threat detections in the past 30 days, showing distribution across the different types of web threats. Selecting a slice opens the list of the domains that were found with malicious or unwanted websites.

    ![Image of the card showing web threats protection summary](images/wtp-summary.png)

>[!Note]
>It can take up to 12 hours before a block is reflected in the cards or the domain list.

## Types of web threats
Web protection categorizes malicious and unwanted websites as:
- **Phishing** — websites that contain spoofed web forms and other phishing mechanisms designed to trick users into divulging credentials and other sensitive information
- **Malicious** — websites that host malware and exploit code
- **Custom indicator** — websites whose URLs or domains you've added to your [custom indicator list](manage-indicators.md) for blocking

## View the domain list
Select a specific web threat category in the **Web threat protection summary** card to open the **Domains** page and display the list of the domains under that threat category. The page provides the following information for each domain:

- **Access count** — number of requests for URLs in the domain
- **Blocks** — number of times requests were blocked
- **Access trend** — change in number of access attempts
- **Threat category** — type of web threat
- **Machines** — number of machines with access attempts

Select a domain to view the list of machines that have attempted to access URLs in that domain as well as the list of URLs.

## Related topics
- [Web protection overview](web-protection-overview.md)
- [Respond to web threats](web-protection-response.md)
