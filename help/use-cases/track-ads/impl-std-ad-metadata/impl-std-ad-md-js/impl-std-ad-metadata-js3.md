---
title: Meer informatie over het implementeren van standaard-advertentiemetagegevens met JavaScript 3.x
description: In deze video ziet u hoe u standaard- en metagegevens gebruikt in een browser met JavaScript 3.x-apps.
exl-id: ba9abf1d-3778-49ef-a2fc-6c0eafa3b227
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 0%

---

# Standaard en metagegevens implementeren met JavaScript 3.x{#implement-standard-ad-metadata-on-javascript}

## Standaardinstellingen en metagegevens implementeren

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
