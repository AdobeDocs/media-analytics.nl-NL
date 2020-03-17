---
title: Standaardmetagegevens implementeren op Android
description: Beschrijft het plaatsen van standaardvideo en admeta-gegevens die met het volgen vraag op Android moeten worden verzonden.
uuid: c48b4190-b062-4c4e-9c40-8dde4598a50e
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Standaardmetagegevens implementeren op Android{#implement-standard-metadata-on-android}

## Standaardmetagegevensconstanten

| Naam van constante | Beschrijving |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardMediaMetadata` | Constante voor het koppelen van standaardmetagegevens op `MediaObject`. |

## API-naslaggids voor metagegevens

* Maak een `HashMap` standaard waarde voor de metagegevenssleutel.
   * [Videometagegevens](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
   * [Toetsen voor audiometagegevens](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.AudioMetadataKeys.html)
* Stel de standaardmetagegevens in `HashMap` op het `MediaInfo` gebruik van de standaardconstante Metagegevens voor de metagegevens.
* Geef dit `MediaInfo` object op terwijl de `trackSessionStart()` API wordt aangeroepen.

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
