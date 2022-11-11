---
title: Meer informatie over het implementeren van standaardmetagegevens op iOS
description: Leer hoe u standaardvideo- en advertentiemetagegevens instelt die moeten worden verzonden met trackingoproepen op iOS.
uuid: 75a80f08-4a95-49d4-a27a-8ce531d64d31
exl-id: e0981346-3d3c-4a0c-82a4-19942634fd03
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 9%

---

# Standaardmetadata implementeren in iOS{#implement-standard-metadata-on-ios}

## Metagegevensconstanten

| Naam van constante | Beschrijving   |
|---|---|
| `ADBMediaObjectKeyStandardMediaMetadata` | Constante voor het koppelen van standaardmetagegevens op `MediaInfo ADBMediaObject` |

## Implementatie

1. Een woordenboek maken van standaardwaardeparen voor metagegevens met de opdracht `ADBStandardMetadataKeys`
   [iOS-metagegevenssleutels](/help/use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

1. Het standaardmetagegevenswoordenboek instellen op `MediaInfo` `ADBMediaObject` instantie met de standaardmetagegevensconstante voor metagegevens.

1. Geef deze `MediaInfo` object terwijl het `trackSessionStart` API.

### Voorbeeldimplementatie

Instantiëren van een standaard metagegevensobject, vullen van de gewenste variabelen en stellen het metagegevensobject in op het Media Heartbone-object. Bijvoorbeeld:

```
// Sample implementation for using standard video metadata keys 
 
NSMutableDictionary *standardVideoMetadata = [[NSMutableDictionary alloc] init]; 
 
[standardVideoMetadata setObject:@"Sample Show" forKey:ADBVideoMetadataKeySHOW]; 
 
[standardVideoMetadata setObject:@"Sample Season" forKey:ADBVideoMetadataKeySEASON]; 
 
[standardVideoMetadata setObject:@"Sample Episode" forKey:ADBVideoMetadataKeyEPISODE]; 
 
[mediaObject setValue:standardVideoMetadata forKey:ADBMediaObjectKeyStandardMediaMetadata];
```

```
// Sample implementation for using standard audio metadata keys 
 
NSMutableDictionary *standardAudioMetadata = [[NSMutableDictionary alloc] init];  
 
[standardAudioMetadata setObject:@"Sample Album"   forKey:ADBAudioMetadataKeyALBUM];  
 
[standardAudioMetadata setObject:@"Sample Label"   forKey:ADBAudioMetadataKeyLABEL]; 
 
[mediaObject setValue:standardAudioMetadata   forKey:ADBMediaObjectKeyStandardMediaMetadata];
```
