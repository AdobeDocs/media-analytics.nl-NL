---
title: Meer informatie over het implementeren van standaardmetagegevens op Android
description: Leer hoe u standaardvideo- en advertentiemetagegevens instelt die moeten worden verzonden met trackingoproepen op Android.
uuid: c48b4190-b062-4c4e-9c40-8dde4598a50e
exl-id: 31afd8b5-0f23-4025-afcb-6df906cf6be5
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 1%

---

# Standaardmetagegevens implementeren op Android{#implement-standard-metadata-on-android}

## Standaardmetagegevensconstanten

| Naam van constante | Beschrijving   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardMediaMetadata` | Constante voor het koppelen van standaardmetagegevens op `MediaObject` . |

## API-naslaggids voor metagegevens

* Maak een `HashMap` van standaard waardeparen voor metagegevens.
   * [&#x200B; VideoMeta-gegevens Sleutels &#x200B;](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
   * [&#x200B; AudioMeta-gegevenssleutels &#x200B;](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.AudioMetadataKeys.html)
* Stel de standaardmetagegevens `HashMap` in op `MediaInfo` met de standaardmetagegevensconstante voor de metagegevens.
* Geef dit `MediaInfo` -object op terwijl de `trackSessionStart()` API wordt aangeroepen.

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
