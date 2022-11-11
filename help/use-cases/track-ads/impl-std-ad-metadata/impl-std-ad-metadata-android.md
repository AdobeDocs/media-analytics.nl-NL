---
title: Meer informatie over het implementeren van standaard-advertentiemetagegevens op Android
description: Standaardinstellingen en metagegevens gebruiken voor het bijhouden van advertenties op Android.
uuid: 19b98bc1-c659-4182-a4ff-b3340fe2453c
exl-id: f1aa017f-b2ae-40ca-b4d9-b508cf45cb0c
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 11%

---

# Standaardmetadata voor advertenties implementeren in Android{#implement-standard-ad-metadata-on-android}

## Advertentieconstanten

| Naam van constante | Beschrijving   |
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
