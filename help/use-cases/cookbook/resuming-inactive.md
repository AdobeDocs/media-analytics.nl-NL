---
title: Inactieve sessies hervatten
description: Leer hoe u een inactieve sessie kunt hervatten.
uuid: 3ff1205d-7bbe-4016-9bd7-6e34b7862c4c
exl-id: ee4cf7f5-5788-4d35-a04d-4ed714ccd663
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 3%

---

# Niet-actieve sessies hervatten{#resuming-inactive-sessions}

## Lange pauzes

De SDK van Media houdt automatisch bij hoe lang het afspelen van media zich in een van de volgende niet-actieve staten bevindt:

* Gepauzeerd
* Zoeken
* Gestopt
* Bufferen

Als een sessie voor het bijhouden van media langer dan 30 minuten in een niet-actieve status blijft, wordt de sessie automatisch gesloten. Als de gebruiker na een eerder inactieve video het volgen zitting hervat (`trackPlay`), wordt automatisch een nieuwe videosessie gemaakt met behulp van de eerder gebruikte videogegevens en metagegevens en wordt een resume-hartslaggebeurtenis verzonden. Zie voor meer informatie [Parameters voor audio en video.](/help/implementation/variables/audio-video-parameters.md)


## Eerder gesloten sessie handmatig hervatten

De Media SDK hervat alleen automatisch sessies als de toepassing niet is gesloten. Als de toepassing gebruikersgegevens opslaat en de mogelijkheid heeft om een eerder gesloten medium te hervatten, is het mogelijk om handmatig een hervattingsgebeurtenis te activeren. Stel bij het starten van de videolesessie de optionele eigenschap Video hervat in.

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
