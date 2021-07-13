---
title: Leer hoe u standaardmetagegevens kunt implementeren op iOS
description: Leer hoe u standaardvideo- en advertentiemetagegevens instelt die moeten worden verzonden met trackingoproepen op iOS.
uuid: 75a80f08-4a95-49d4-a27a-8ce531d64d31
exl-id: e0981346-3d3c-4a0c-82a4-19942634fd03
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 8%

---

# Standaardmetadata implementeren in iOS{#implement-standard-metadata-on-ios}

## Metagegevensconstanten

| Naam van constante | Beschrijving   |
|---|---|
| `ADBMediaObjectKeyStandardMediaMetadata` | Constante voor het bijvoegen van standaardmetagegevens op `MediaInfo ADBMediaObject` |

## Implementatie

1. Een woordenboek maken van standaardwaardeparen voor metagegevens met de `ADBStandardMetadataKeys`
   [IOS-metagegevens](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

1. Stel het standaardmetagegevenswoordenboek in op `MediaInfo` `ADBMediaObject`-instantie met de standaardmetagegevensconstante voor metagegevens.

1. Geef dit `MediaInfo`-object op terwijl de `trackSessionStart`-API wordt aangeroepen.

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
