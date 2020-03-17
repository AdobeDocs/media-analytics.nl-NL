---
title: Standaardmetagegevens implementeren op iOS
description: Beschrijft het plaatsen van standaardvideo en admeta-gegevens die met het volgen vraag op iOS moeten worden verzonden.
uuid: 75a80f08-4a95-49d4-a27a-8ce531d64d31
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Standaardmetagegevens implementeren op iOS{#implement-standard-metadata-on-ios}

## Metagegevensconstanten

| Naam van constante | Beschrijving |
|---|---|
| `ADBMediaObjectKeyStandardMediaMetadata` | Constante voor het koppelen van standaardmetagegevens op `MediaInfo ADBMediaObject` |

## Implementatie

1. Een woordenboek maken van standaardwaardeparen voor metagegevens met de opdracht `ADBStandardMetadataKeys`
   [IOS-metagegevens](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

1. Stel het standaardmetagegevenswoordenboek voor `MediaInfo` een `ADBMediaObject` instantie in met de standaardmetagegevensconstante voor metagegevens.

1. Geef dit `MediaInfo` object op terwijl de `trackSessionStart` API wordt aangeroepen.

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

