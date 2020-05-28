---
title: Standaard- en metagegevens implementeren met JavaScript 2.x
description: De standaardinstellingen en metagegevens in een browser gebruiken met JavaScript 2.x-toepassingen.
uuid: 4ea10c5a-ae2b-45d0-aad3-9f10028ee7c3
translation-type: tm+mt
source-git-commit: 30ed54924c75a9c33e6122b2d7ddbb84c06b8c0c
workflow-type: tm+mt
source-wordcount: '68'
ht-degree: 1%

---


# Standaard- en metagegevens implementeren met JavaScript 2.x{#implement-standard-ad-metadata-on-javascript}

## Advertentieconstanten

| Naam van constante | Beschrijving   |
|---|---|
| `StandardAdMetadata` | Constante voor het koppelen van standaard- en metagegevens op advertentieobject |

## Implementatiestandaard en metagegevens

Voor standaard- en metagegevens maakt u een woordenboek van standaard- en metagegevenssleutelwaardeparen met behulp van de toetsen voor uw platform:

```js
var adObject =  
MediaHeartbeat.createAdObject(<AD_NAME>,  
                              <AD_ID>,  
                              <POSITION>,  
                              <LENGTH>);

// Set standard Ad Metadata
var standardAdMetadata = {};
standardAdMetadata[MediaHeartbeat.AdMetadataKeys.ADVERTISER] = "Sample Advertiser";
standardAdMetadata[MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID] = "Sample Campaign";
adObject.setValue(MediaObjectKey.StandardAdMetadata, standardAdMetadata);
```
