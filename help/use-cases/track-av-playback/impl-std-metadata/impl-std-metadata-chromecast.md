---
title: Leer hoe u standaardmetagegevens kunt implementeren in Chromecast
description: Leer hoe u standaardvideo- en advertentiemetagegevens instelt op Chromecast.
uuid: 1560d3e0-29f5-4678-9f01-c672e0ae547b
exl-id: 052ede4b-ea8a-4ca6-bf02-0aab22a8bcda
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 3%

---

# Standaardmetagegevens toepassen op Chromecast{#implement-standard-metadata-on-chromecast}

Instantiëren van een standaard metagegevensobject, vullen van de gewenste variabelen en stellen het metagegevensobject in op het Media Heartbone-object. Bijvoorbeeld:

```js
var standardVideoMetadata = {};
standardVideoMetadata[VideoMetadataKeys.SHOW] = "Sample show";
standardVideoMetadata[VideoMetadataKeys.SEASON] = "Sample season";

mediaObject[ADBMobile.media.MediaObjectKey.StandardVideoMetadata] = standardVideoMetadata;
```

```js
var standardAudioMetadata = {};
standardAudioMetadata[AudioMetadataKeys.ARTIST] = "Sample artist";
standardAudioMetadata[AudioMetadataKeys.ALBUM] = "Sample album";

mediaObject[ADBMobile.media.MediaObjectKey.StandardAudioMetadata] = standardAudioMetadata;
```

Zie de uitvoerige lijst van audio en videometa-gegevens hier: [ Audio en videoparameters.](/help/implementation/variables/audio-video-parameters.md)
