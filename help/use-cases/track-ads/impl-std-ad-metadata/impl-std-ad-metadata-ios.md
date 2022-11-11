---
title: Meer informatie over het implementeren van standaard-advertentiemetagegevens op iOS
description: Standaardinstellingen en metagegevens gebruiken voor het bijhouden van advertenties op iOS.
uuid: f15fb727-5a5b-46c5-bf12-93b376c10fd1
exl-id: 018ae833-51d9-4ff0-80e7-3dbcaefb997c
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '65'
ht-degree: 10%

---

# Standaardmetadata voor advertenties implementeren in iOS{#implement-standard-ad-metadata-on-ios}

## Advertentieconstanten

| Naam van constante | Beschrijving   |
|---|---|
| `ADBMediaObjectKeyStandardAdMetadata` | Constante voor het koppelen van standaard- en metagegevens op `AdInfo ADBMediaObject` |

## Implementatiestandaard en metagegevens

Voor standaard- en metagegevens maakt u een woordenboek van standaard- en metagegevenssleutelwaardeparen met behulp van de toetsen voor uw platform:

```
// Sample implementation for using standard metadata keys for Ad 
NSMutableDictionary *standardAdMetadata = [[NSMutableDictionary alloc] init]; 
[standardAdMetadata setObject:@"Sample Advertiser" forKey:ADBAdMetadataKeyADVERTISER]; 
[standardAdMetadata setObject:@"Sample Campaign" forKey:ADBAdMetadataKeyCAMPAIGN_ID]; 
 
[adObject setValue:standardAdMetadata forKey:ADBMediaObjectKeyStandardAdMetadata];
```

[iOS-metagegevenssleutels](/help/use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
