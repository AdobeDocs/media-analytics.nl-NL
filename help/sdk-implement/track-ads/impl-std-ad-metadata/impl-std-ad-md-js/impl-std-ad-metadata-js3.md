---
title: Meer informatie over het implementeren van standaard-advertentiemetagegevens met JavaScript 3.x
description: De standaardinstellingen en metagegevens in een browser gebruiken met JavaScript 3.x-toepassingen.
exl-id: ba9abf1d-3778-49ef-a2fc-6c0eafa3b227
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '58'
ht-degree: 0%

---

# Standaard- en metagegevens implementeren met JavaScript 3.x{#implement-standard-ad-metadata-on-javascript}

## Implementatiestandaard en metagegevens

Voor standaard- en metagegevens maakt u een woordenboek van standaard- en metagegevenssleutelwaardeparen met behulp van de toetsen voor uw platform:

```js
var adObject =
ADB.Media.createAdObject(<AD_NAME>,
                              <AD_ID>,
                              <POSITION>,
                              <LENGTH>);

// Set standard Ad Metadata
var adMetadata = {};
adMetadata[MediaHeartbeat.AdMetadataKeys.Advertiser] = "Sample Advertiser";
adMetadata[MediaHeartbeat.AdMetadataKeys.CampaignId] = "Sample Campaign";

tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);
```
