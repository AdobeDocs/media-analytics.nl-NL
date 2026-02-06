---
title: Leer hoe u standaardmetagegevens kunt implementeren op Roku
description: Leer hoe te om standaardvideo en admeta-gegevens te plaatsen die met het volgen vraag op Roku moeten worden verzonden.
uuid: ae14d809-343f-452c-832a-f94bd3d83a90
exl-id: 1552b16a-3c2d-4caa-b571-e6628f0b6866
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---

# Standaardmetagegevens implementeren op Roku{#implement-standard-metadata-on-roku}

Instantiëren van een standaard metagegevensobject, vullen van de gewenste variabelen en stellen het metagegevensobject in op het Media Heartbone-object.

**Video:**

```
standardMetadata = {}
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeySHOW] = "sample show"
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeySEASON] = "sample season"
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeyEPISODE] = "sample episode"

mediaInfo[ADBMobile().MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata
```

**Audio:**

```
standardMetadata = {}
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyARTIST] = "sample artist"
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyALBUM] = "sample album"
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyLABEL] = "sample label"

mediaInfo[ADBMobile().MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata
```

Zie de uitvoerige lijst van videometagegevens hier: [ Audio en videoparameters ](/help/implementation/variables/audio-video-parameters.md)
