---
title: Inactieve sessies hervatten
description: Leer hoe u een inactieve sessie kunt hervatten.
uuid: 3ff1205d-7bbe-4016-9bd7-6e34b7862c4c
exl-id: ee4cf7f5-5788-4d35-a04d-4ed714ccd663
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# Niet-actieve sessies hervatten{#resuming-inactive-sessions}

## Lange pauzes

De Media SDK houdt automatisch bij hoe lang het afspelen van media zich in een van de volgende niet-actieve staten bevindt:

* Gepauzeerd
* Zoeken
* Gestopt
* Bufferen

Als een sessie voor het bijhouden van media langer dan 30 minuten in een niet-actieve status blijft, wordt de sessie automatisch gesloten. Als de gebruiker na een eerder inactieve video het volgen zitting (`trackPlay`) hervat, leidt de Hartslag van Media automatisch tot een nieuwe videozitting gebruikend de eerder gebruikte videoinformatie en meta-gegevens, en verzendt een summehartgebeurtenis. Voor meer informatie, zie [ Audio en videoparameters.](/help/implementation/variables/audio-video-parameters.md)


## Eerder gesloten sessie handmatig hervatten

De Media SDK hervat alleen automatisch sessies als de toepassing niet is gesloten. Als de toepassing gebruikersgegevens opslaat en de mogelijkheid heeft om een eerder gesloten medium te hervatten, is het mogelijk om handmatig een hervattingsgebeurtenis te activeren. Wanneer u de videolesessie voor het bijhouden van de video start, stelt u de optionele eigenschap Video hervat in.

### Android

```java
// Set MediaHeartbeat.MediaObjectKey.mediaResumed to true
public void onmediaLoad(Observable observable, Object data) {

  // Replace <MEDIA_NAME> with the media name.
  // Replace <MEDIA_ID> with a media unique identifier.
  // Replace <MEDIA_LENGTH> with the media length.  
  MediaObject mediaInfo = MediaHeartbeat.createMediaObject(  
      <MEDIA_NAME>,  
      <MEDIA_ID>,  
      <MEDIA_LENGTH>,  
      MediaHeartbeat.StreamType.VOD
  );

  // Set to true if this is a resume playback scenario
  mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.mediaResumed, true);

  _heartbeat.trackSessionStart(mediaInfo, mediaMetadata);
}
```

### iOS

```
- (void)onMainmediaLoaded:(NSNotification *)notification {
  //Replace <MEDIA_NAME> with the media name.
  //Replace <MEDIA_ID> with a media unique identifier.
  //Replace <MEDIA_LENGTH> with the media length.     
  ADBMediaObject *mediaObject =  
    [ADBMediaHeartbeat createMediaObjectWithName:<MEDIA_NAME>
                       mediaId:<MEDIA_ID>
                       length:<MEDIA_LENGTH>
                       streamType:ADBMediaHeartbeatStreamTypeVOD];

  //Set to YES if this user is resuming a previously closed media session
  [mediaObject setValue:@(YES) forKey:ADBMediaObjectKeymediaResumed];

  [_mediaHeartbeat trackSessionStart:mediaObject data:mediaMetadata];
}
```

### JavaScript

```js
_onmediaLoad = function () {
  // Replace <MEDIA_NAME> with the media name.
  // Replace <MEDIA_ID> with a media unique identifier.
  // Replace <MEDIA_LENGTH> with the media length.  
  var mediaObject =  
    MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                     <MEDIA_ID,  
                                     <MEDIA_LENGTH>,  
                                     MediaHeartbeat.StreamType.VOD);

  // Set to true if this user is resuming a previously closed media session
  mediaObject.setValue(MediaObjectKey.mediaResumed, true);
  this._mediaHeartbeat.trackSessionStart(mediaObject, contextData);
};
```
