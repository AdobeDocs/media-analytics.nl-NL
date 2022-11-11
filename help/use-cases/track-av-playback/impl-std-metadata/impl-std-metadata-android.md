---
title: Meer informatie over het implementeren van standaardmetagegevens op Android
description: Leer hoe u standaardvideo- en advertentiemetagegevens instelt die moeten worden verzonden met trackingaanroepen op Android.
uuid: c48b4190-b062-4c4e-9c40-8dde4598a50e
exl-id: 31afd8b5-0f23-4025-afcb-6df906cf6be5
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 6%

---

# Standaardmetadata implementeren in Android{#implement-standard-metadata-on-android}

## Standaardmetagegevensconstanten

| Naam van constante | Beschrijving   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardMediaMetadata` | Constante voor het koppelen van standaardmetagegevens op `MediaObject`. |

## API-naslaggids voor metagegevens

* Een `HashMap` van standaard sleutelwaardeparen voor metagegevens.
   * [Videometagegevens](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
   * [Toetsen voor audiometagegevens](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.AudioMetadataKeys.html)
* Standaardmetagegevens instellen `HashMap` op `MediaInfo` de standaardmetagegevensconstante gebruiken voor de metagegevens.
* Geef deze `MediaInfo` object terwijl het `trackSessionStart()` API.

## Voorbeeldimplementaties

### Video

```java
// Sample code to set standard metadata for tracking sessions 
Map <String, String> standardVideoMetadata= new HashMap<String, String>(); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.EPISODE, "Sample Episode"); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SHOW, "Sample Show"); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SEASON, "Sample Season"); 
mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata, standardVideoMetadata);
```

### Audio

```java
// Sample code to set standard metadata for tracking sessions 
Map <String, String> standardAudiooMetadata= new HashMap<String, String>(); 
standardAudiooMetadata.put(MediaHeartbeat.AudiooMetadataKeys.ARTIST, "Sample Artist"); 
standardAudiooMetadata.put(MediaHeartbeat.AudiooMetadataKeys.ALBUM, "Sample Album"); 
standardAudiooMetadata.put(MediaHeartbeat.AudiooMetadataKeys.LABEL, "Sample Label"); 
mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAudiooMetadata, standardAudiooMetadata);
```
