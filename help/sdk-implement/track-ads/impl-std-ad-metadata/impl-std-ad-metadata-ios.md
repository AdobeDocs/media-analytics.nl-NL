---
title: Standaard en metagegevens implementeren op iOS
description: Standaardinstellingen en metagegevens gebruiken voor het bijhouden van advertenties op iOS.
uuid: f15fb727-5a5b-46c5-bf12-93b376c10fd1
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Standaard en metagegevens implementeren op iOS{#implement-standard-ad-metadata-on-ios}

## Advertentieconstanten

| Naam van constante | Beschrijving |
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

[iOS-metagegevenssleutels](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
