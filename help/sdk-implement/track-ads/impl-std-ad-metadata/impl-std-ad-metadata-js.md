---
title: Standaard en metagegevens implementeren in JavaScript
description: Standaardinstellingen en metagegevens gebruiken voor het bijhouden van advertenties in JS-apps (Browser).
uuid: 4ea10c5a-ae2b-45d0-aad3-9f10028ee7c3
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Standaard en metagegevens implementeren in JavaScript{#implement-standard-ad-metadata-on-javascript}

## Advertentieconstanten

| Naam van constante | Beschrijving |
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

