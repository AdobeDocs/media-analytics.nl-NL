---
title: VOD afspelen met zoeken in de hoofdinhoud
description: Een voorbeeld van hoe te om VOD inhoud te volgen waarin het zoeken voorkwam gebruikend SDK van Media.
uuid: 5c2392f6-9b9c-42f5-833f-77423d1e6222
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# VOD afspelen met zoeken in de hoofdinhoud{#vod-playback-with-seeking-in-the-main-content}

## Scenario {#scenario}

Dit scenario omvat het zoeken in de belangrijkste inhoud tijdens playback.

Dit is hetzelfde scenario als het afspelen [VOD zonder advertentiescenario](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md) , maar een deel van de inhoud wordt doorgescrubd en een zoekopdracht wordt uitgevoerd van het ene punt in de hoofdinhoud naar het andere.

| Trigger | Hartslagmethode | Netwerkaanroepen | Notities |
| --- | --- | --- | --- |
| Gebruiker klikt [!UICONTROL Play] | `trackSessionStart` | Start inhoud analyse, Start inhoud hartslag | De metingsbibliotheek is zich niet bewust dat er een pre-rol advertentie is, zodat zijn deze netwerkvraag identiek aan de playback [VOD zonder ad-hocscenario](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md) . |
| Het eerste frame van de inhoud wordt afgespeeld. | `trackPlay` | Hartslaginhoud afspelen | Wanneer de hoofdstukinhoud vóór hoofdinhoud wordt afgespeeld, begint de hartslag wanneer het hoofdstuk begint. |
| Inhoud afspelen |  | Content Heartbeats | Deze netwerkaanroep is precies hetzelfde als de [VOD-weergave zonder advertentiescenario](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md) . |
| Gebruiker begint de zoekbewerking op inhoud | `trackSeekStart` |  | Er gaan geen hartslagen uit tot de zoekactie is voltooid, bijvoorbeeld `trackSeekComplete` |
| De zoekbewerking is voltooid | `trackSeekComplete` |  | De hartslagen beginnen uit te gaan aangezien het zoeken volledig is.  Tip:  De waarde van de afspeelkop moet de juiste nieuwe afspeelkop na de zoekactie aangeven. |
| Inhoud is voltooid | `trackComplete` | Hartslaginhoud voltooid | Deze netwerkaanroep is precies hetzelfde als de [VOD-weergave zonder advertentiescenario](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md) . |
| Sessie over | `trackSessionEnd` |  | `SessionEnd` |

## Voorbeeldcode {#sample-code}

In dit scenario zoekt de gebruiker wanneer de hoofdinhoud wordt afgespeeld.

![](assets/seek-main-to-main.png)

### Android

Stel de volgende code in om dit scenario in Android weer te geven:

```java
// Set up mediaObject 
MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.VOD 
); 

HashMap<String, String> mediaMetadata = new HashMap<String, String>(); 
mediaMetadata.put(CUSTOM_KEY_1, CUSTOM_VAL_1); 
mediaMetadata.put(CUSTOM_KEY_2, CUSTOM_VAL_2); 

// 1. Call trackSessionStart() when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback.  
_mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., whn the first frame  
//    of the main content is rendered on the screen.  
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Track the MediaHeartbeat.Event.SeekStart event when the user begins to seek.  
_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart, null, null); 

....... 
....... 

// 4. Track the MediaHeartbeat.Event.SeekComplete event when the user completes seeking 
_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete, null, null); 

....... 
....... 

// 5. Call trackComplete() when the playback reaches the end, i.e., when the media 
//    completes and finishes playing. 
_mediaHeartbeat.trackComplete(); 

........ 
........ 

// 6. Call trackSessionEnd() when the playback session is over. This method must be  
//    called even if the user does not watch the media to completion.  
_mediaHeartbeat.trackSessionEnd(); 

........ 
........ 
```

### iOS

Stel de volgende code in om dit scenario in iOS weer te geven:

```
// Set up mediaObject 
ADBMediaObject *mediaObject =  
[ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME o 
                   length:MEDIA_LENGTH  
                   streamType:ADBMediaHeartbeatStreamTypeVOD]; 
 
NSMutableDictionary *mediaContextData = [[NSMutableDictionary alloc] init]; 
[mediaContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
[mediaContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 

// 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback. 
[_mediaHeartbeat trackSessionStart:mediaObject data:mediaContextData]; 
....... 
....... 

// 2. Call trackPlay when the playback actually starts, i.e., when the 
//    first frame of the main content is rendered on the screen. 
[_mediaHeartbeat trackPlay];  
....... 
....... 

// 3. Track the trackEvent:ADBMediaHeartbeatEventSeekStart event when the user  
//    begins to seek out of the chapter with the intent to skip it. 
[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekStart  
               mediaObject:nil  
               data:nil]; 
....... 
....... 

// 4. Track the trackEvent:ADBMediaHeartbeatEventSeekComplete event when the  
//    user seeks out of the chapter with the intent to skip it. 
[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekComplete  
               mediaObject:nil  
               data:nil]; 
....... 
....... 

// 5. Call trackComplete when the playback reaches the end, i.e., completes  
//    and finishes playing. 
[_mediaHeartbeat trackComplete]; 
....... 
....... 

// 6. Call trackSessionEnd when the playback session is over. This method must  
//    be called even if the user does not watch the media to completion. 
[_mediaHeartbeat trackSessionEnd]; 
....... 
....... 
```

### JavaScript

Voer de volgende tekst in om dit scenario weer te geven:

```js
// Set up mediaObject 
var mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.VOD 

); 

var mediaMetadata = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 

}; 

// 1. Call trackSessionStart() when Play is clicked or if autoplay is used,  
//    i.e., there's an intent to start playback. 
this._mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the  
//    first frame of the ad media is rendered on the screen. 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Track the MediaHeartbeat.Event.SeekStart event when the user  
//    begins to seek. 
this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart); 

....... 
....... 

// 4. Track the MediaHeartbeat.Event.SeekComplete event when the user  
//    completes seeking. 
this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete); 

....... 
....... 

// 5. Call trackComplete() when the playback reaches the end, i.e., when 
//    playback completes and finishes playing. 
this._mediaHeartbeat.trackComplete(); 

........ 
........ 

// 6. Call trackSessionEnd() when the playback session is over. This method must be called  
//    even if the user does not watch the media to completion. 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........ 
```

