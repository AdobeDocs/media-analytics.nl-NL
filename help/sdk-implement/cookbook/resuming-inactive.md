---
title: Niet-actieve sessies hervatten
description: Hoe te om het hervatten van een inactieve zitting te behandelen.
uuid: 3ff1205d-7bbe-4016-9bd7-6e34b7862c4c
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Niet-actieve sessies hervatten{#resuming-inactive-sessions}

## Lange pauzes

De SDK van Media houdt automatisch bij hoe lang het afspelen van media zich in een van de volgende niet-actieve staten bevindt:

* Gepauzeerd
* Zoeken
* Gestopt
* Bufferen

Als een sessie voor het bijhouden van media langer dan 30 minuten in een niet-actieve status blijft, wordt de sessie automatisch gesloten. Als de gebruiker na een eerder inactieve video het volgen zitting (`trackPlay`) hervat, leidt de Hartslag van Media automatisch tot een nieuwe videozitting gebruikend de eerder gebruikte videoinformatie en meta-gegevens, en verzendt een hervattingshartgebeurtenis. Zie Parameters voor [audio en video voor meer informatie.](/help/metrics-and-metadata/audio-video-parameters.md)

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

