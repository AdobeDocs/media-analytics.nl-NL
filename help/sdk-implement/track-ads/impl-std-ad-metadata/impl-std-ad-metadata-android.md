---
title: Standaard- en metagegevens implementeren op Android
description: Standaardinstellingen en metagegevens gebruiken voor het bijhouden van advertenties op Android.
uuid: 19b98bc1-c659-4182-a4ff-b3340fe2453c
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Standaard- en metagegevens implementeren op Android{#implement-standard-ad-metadata-on-android}

## Advertentieconstanten

| Naam van constante | Beschrijving |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardAdMetadata` | Constante voor het koppelen van standaard- en metagegevens op advertentie `MediaObject`. |

## Implementatiestandaard en metagegevens

Voor standaard- en metagegevens maakt u een woordenboek van standaard- en metagegevenssleutelwaardeparen met behulp van de toetsen voor uw platform:

```java
// Setting standard Ad Metadata 
Map <String, String> standardAdMetadata = new HashMap<String, String>(); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, "Sample Advertiser"); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, "Sample Campaign"); 
adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata); 
```

