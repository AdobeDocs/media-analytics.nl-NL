---
title: VOD afspelen met voorroladvertenties
description: Bekijk een voorbeeld van hoe u VOD-inhoud kunt bijhouden die pre-roll-advertenties bevat met de Media SDK.
uuid: 5d1022a8-88cb-40aa-919c-60dd592a639e
exl-id: c77f6457-ac3b-4d7a-8eed-e7ebd357a6a5
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---

# VOD afspelen met pre-roll-advertenties{#vod-playback-with-pre-roll-ads}

In dit scenario zijn pre-roll-advertenties ingevoegd vóór de hoofdinhoud. Tenzij gespecificeerd, zijn de netwerkvraag het zelfde als de vraag in de [ playback VOD zonder advertenties ](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md) scenario. De netwerkvraag gebeurt tezelfdertijd, maar de nuttige lading is verschillend.

| Trigger | Hartslagmethode | Netwerkaanroepen   | Notities   |
| --- | --- | --- | --- |
| De gebruiker klikt op [!UICONTROL Play] | `trackSessionStart` | Start inhoud analyse, Start inhoud hartslag | De metingsbibliotheek weet niet dat er een pre-rol advertentie is, zodat zijn deze netwerkvraag nog identiek aan de [ playback VOD zonder advertenties ](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md) scenario. |
| De advertentie begint. | <ul> <li> `trackEvent:AdBreakStart` </li> <li> `trackEvent:AdStart` </li> </ul> | Analyses en begin, hartslag en begin | |
| Het frame van advertentie 1 wordt afgespeeld. | `trackPlay` | Hartslag en Afspelen | De inhoud van de advertentie wordt afgespeeld vóór de hoofdinhoud en de hartslagen beginnen bij het starten van de advertentie. |
| De advertentie wordt afgespeeld. | | Hartbeats toevoegen | |
| Advertentie 2 voltooit het afspelen. | `trackEvent:trackAdComplete` | Hartslag en voltooid | Het einde van de advertentie is bereikt. |
| Het eerste frame van advertentie 2 wordt afgespeeld. | `trackEvent:AdStart` | Analyses en begin, hartslag en begin | |
| De advertentie speelt. | | Hartbeats toevoegen | |
| Advertentie 2 voltooit het afspelen. | <ul> <li> `trackEvent:trackAdComplete` </li> <li> `trackEvent:AdBreakComplete` </li> </ul> | Hartslag en voltooid | Het einde van de advertentie en de pod is bereikt. |
| De inhoud wordt afgespeeld. | | Content Heartbeats | Deze netwerkvraag is identiek aan de [ playback VOD zonder advertenties ](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md) scenario. |
| De inhoud is voltooid. | `trackComplete` | Hartslaginhoud voltooid | Deze netwerkvraag is identiek aan de [ playback VOD zonder advertenties ](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md) scenario. |
| De sessie is beëindigd | `trackSessionEnd` | | `SessionEnd` |

## Parameters {#parameters}

Wanneer het afspelen van een advertentie begint, wordt een `Heartbeat Ad Start` -aanroep verzonden. Wanneer het begin van de advertentie niet samenvalt met de timer van 10 seconden, wordt de aanroep van `Heartbeat Ad Start` met een paar seconden vertraagd en gaat de aanroep naar het volgende interval van 10 seconden. Wanneer dit gebeurt, gaat a `Content Heartbeat` uit in het zelfde interval, en u kunt tussen de twee vraag onderscheiden door het gebeurtenistype en het activatype te bekijken:

### Hartslag en begin

| Parameter | Waarde | Notities |
|---|---|---|
| `s:event:type` | `start` |  |
| `s:asset:type` | `ad` |  |

Advertenties volgen hetzelfde basismodel als `Content Heartbeats` , zodat de `Ad Play` -aanroep vergelijkbaar is met de `Content Play` -aanroep.

### Aanroep hartslag en afspelen

| Parameter | Waarde | Notities |
|---|---|---|
| `s:event:type` | `play` |  |
| `s:asset:type` | `ad` |  |

Deze parameters zijn vergelijkbaar met de aanroep van `Content Heartbeats` , maar de aanroep van `Ad Heartbeats` bevat een aantal extra parameters:

### Hartbeats toevoegen

| Parameter | Waarde | Notities |
|---|---|---|
| `s:event:type` | `play` |  |
| `s:asset:type` | `ad` |  |
| `s:asset:ad_id` | &lt;ad-id> |  |
| `s:asset:pod_id` | &lt;pod-id toevoegen> |  |

Net als bij `Heartbeat Content Complete` -aanroepen wordt een `Heartbeat Ad Complete` -aanroep verzonden wanneer het afspelen van de advertentie is voltooid en het einde van de afspeelkop is bereikt. Deze aanroep ziet er net zo uit als andere `Heartbeat Ad` -aanroepen, maar bevat een paar specifieke dingen:

### Hartslagslag en Volledige Vraag

| Parameter | Waarde | Notities |
|---|---|---|
| `s:event:type` | `complete` |  |
| `s:asset:type` | `ad` |  |

## Voorbeeldcode voor een pre-roll en break {#sample-code-for-a-pre-roll-ad-break}

In dit scenario bestaat de VOD uit een pre-roll advertentie, een tweede pre-roll advertentie, en dan wordt de inhoud gespeeld.

![](assets/preroll-regular-playback.png)

* **Android** om dit scenario in Android te bekijken, opstelling de volgende code:

  ```java
  // Set up  mediaObject 
  MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
      Configuration.MEDIA_NAME,  
      Configuration.MEDIA_ID,  
      Configuration.MEDIA_LENGTH,  
      MediaHeartbeat.StreamType.VOD 
  ); 
  
  HashMap<String, String> videoMetadata = new HashMap<String, String>(); 
  videoMetadata.put(CUSTOM_KEY_1, CUSTOM_VAL_1); 
  videoMetadata.put(CUSTOM_KEY_2, CUSTOM_VAL_2); 
  
  // 1. Call trackSessionStart() when the user clicks Play or if autoplay is used,  
  //    i.e., there's an intent to start playback.  
  _mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 
  
  ...... 
  ...... 
  
  // Pre-roll 
  MediaObject adBreakInfo =  
    MediaHeartbeat.createAdBreakObject(ADBREAK_NAME,  
                                       ADBREAK_POSITION,  
                                       ADBREAK_START_TIME); 
  MediaObject adInfo =  
    MediaHeartbeat.createAdObject(AD_NAME,  
                                  AD_ID,  
                                  AD_POSITION,  
                                  AD_LENGTH); 
  
  // Context ad data 
  HashMap<String, String> adMetadata = new HashMap<String, String>(); 
  adMetadata.put(CUSTOM_KEY_1, CUSTOM_VAL_1); 
  adMetadata.put(CUSTOM_KEY_2, CUSTOM_VAL_2); 
  
  // 2. Track the MediaHeartbeat.Event.AdBreakStart event when the pre-roll pod starts  
  //    to play. Note that since this is a pre-roll, call must track the 
  //    "MediaHeartbeat.Event.AdBreakStart" event before you call trackPlay().  
  _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo, null); 
  
  ....... 
  ....... 
  
  // 3. Track the MediaHeartbeat.Event.AdStart event when the pre-roll pod's ad starts  
  //    to play. Note that since this is a pre-roll, you must track the  
  //    "MediaHeartbeat.Event.AdStart" event before you call trackPlay(). 
  _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
  
  ....... 
  ....... 
  
  // 4. Call trackPlay() when the playback actually starts, i.e., when the first frame  
  //    of the ad video is rendered on the screen. 
  _mediaHeartbeat.trackPlay(); 
  
  ....... 
  ....... 
  
  // 5. Track the MediaHeartbeat.Event.AdComplete event when the ad reaches the end,  
  //    i.e., when the ad completes and finishes playing.  
  _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete, null, null); 
  
  ....... 
  ....... 
  
  // 6. Track the MediaHeartbeat.Event.AdStart event when the pre-roll pod's second ad  
  //    starts to play. 
  _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
  
  ....... 
  ....... 
  
  // 7. Track the MediaHeartbeat.Event.AdComplete event when the second ad reaches the  
  //    end, i.e., the second ad completes and finishes playing. 
  _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete, null, null); 
  
  ....... 
  ....... 
  
  // 8. Track the MediaHeartbeat.Event.AdBreakComplete event when all of the ads in the  
  //    pod finish playing.  
  _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete, null, null); 
  
  ....... 
  ....... 
  
  // 9. Call trackComplete() when the playback reaches the end, i.e., when the video 
  //    completes and finishes playing. 
  _mediaHeartbeat.trackComplete(); 
  
  ........ 
  ........ 
  
  // 10. Call trackSessionEnd() when the playback session is over. This method must be  
  //     called even if the user does not watch the video to completion.  
  _mediaHeartbeat.trackSessionEnd(); 
  
  ........ 
  ........ 
  ```

* **iOS -** om dit scenario in iOS te bekijken, opstelling de volgende code:

  ```
  //  Set up mediaObject 
  ADBMediaObject *mediaObject =  
    [ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                       length:MEDIA_LENGTH  
                       streamType:ADBMediaHeartbeatStreamTypeVOD]; 
  
  NSMutableDictionary *videoContextData = [[NSMutableDictionary alloc] init]; 
  [videoContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
  [videoContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
  
  // 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
  //    i.e., there is an intent to start playback. 
  [_mediaHeartbeat trackSessionStart:mediaObject data:videoContextData]; 
  ....... 
  ....... 
  
  // Pre-roll 
  ADBMediaObject *adBreakInfo =  
    [ADBMediaHeartbeat createAdBreakObjectWithName:AD_BREAK_NAME  
                       position:AD_BREAK_POSITION  
                       startTime:AD_BREAK_START_TIME]; 
  ADBMediaObject *adInfo =  
    [ADBMediaHeartbeat createAdObjectWithName:AD_NAME  
                       adId:AD_ID  
                       position:AD_POSITION  
                       length:AD_LENGTH]; 
  
  // context ad data 
  NSMutableDictionary *adDictionary = [[NSMutableDictionary alloc] init]; 
  [adDictionary setObject:@"custom-val1" forKey:@"custom-key1"]; 
  [adDictionary setObject:@"custom-val2" forKey:@"custom-key2"]; 
  
  // 2. Track the ADBMediaHeartbeatEventAdBreakStart event when the pre-roll pod  
  //    starts to play. Note that since this is a pre-roll, you must track the  
  //    "ADBMediaHeartbeatEventAdBreakStart" event before you call trackPlay. 
  [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakStart  
                   mediaObject:adBreakObject  
                   data:nil]; 
  ....... 
  ....... 
  
  // 3. Track the ADBMediaHeartbeatEventAdStart event when the pre-roll pod's  
  //    ad starts to play. Note that since this is a pre-roll, you must track  
  //    the "ADBMediaHeartbeatEventAdStart" event before you call trackPlay. 
  [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdStart  
                   mediaObject:adObject  
                   data:adDictionary]; 
  ....... 
  ....... 
  
  // 4. Call trackPlay when the playback actually starts, i.e., when the   
  //    first frame of the main content is rendered on the screen. 
  [_mediaHeartbeat trackPlay]; 
  ....... 
  ....... 
  
  // 5. Track the ADBMediaHeartbeatEventAdComplete event when the ad reaches  
  //    the end, i.e., when the video completes and finishes playing. 
  [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdComplete  
                   mediaObject:nil  
                   data:nil]; 
  ....... 
  ....... 
  
  // 6. Track the ADBMediaHeartbeatEventAdStart event when the pre-roll pod's  
  //    second ad starts to play. 
  [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdStart  
                   mediaObject:adBreakObject  
                   data:nil]; 
  ....... 
  ....... 
  
  // 7. Track the ADBMediaHeartbeatEventAdComplete event when the second ad  
  //    reaches the end, i.e., it completes and finishes playing. 
  [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdComplete  
                   mediaObject:nil  
                   data:nil]; 
  ....... 
  ....... 
  
  // 8. Track the ADBMediaHeartbeatEventAdBreakComplete event when all the  
  //    ads in the pod finish playing. 
  [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakComplete  
                   mediaObject:adBreakObject  
                   data:nil]; 
  ....... 
  ....... 
  
  // 9. Call trackComplete when the playback reaches the end, i.e., when the  
  //    video completes and finishes playing. 
  [_mediaHeartbeat trackComplete]; 
  ....... 
  ....... 
  
  // 10. Call trackSessionEnd when the playback session is over. This method  
  //     must be called even if the user does not watch the video to completion. 
  [_mediaHeartbeat trackSessionEnd]; 
  ....... 
  ....... 
  ```

* **JavaScript** om dit scenario in JavaScript te bekijken, ga de volgende tekst in:

  ```js
  // Set up mediaObject 
  var mediaInfo =  
    MediaHeartbeat.createMediaObject(Configuration.MEDIA_NAME,  
                                     Configuration.MEDIA_ID,  
                                     Configuration.MEDIA_LENGTH,MediaHeartbeat.StreamType.VOD); 
  var videoMetadata = { 
      CUSTOM_KEY_1 : CUSTOM_VAL_1,  
      CUSTOM_KEY_2 : CUSTOM_VAL_2, 
      CUSTOM_KEY_3 : CUSTOM_VAL_3 
  }; 
  
  // 1. Call trackSessionStart() when Play is clicked or if autoplay is used,  
  //    i.e., there's an intent to start playback. 
  this._mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 
  
  ...... 
  ...... 
  
  // Preroll 
  var adBreakInfo =  
    MediaHeartbeat.createAdBreakObject(ADBREAK_NAME, ADBREAK_POSITION, ADBREAK_START_TIME); 
  var adInfo =  
    MediaHeartbeat.createAdObject(AD_NAME, AD_ID, AD_POSITION, AD_LENGTH); 
  
  // Custom ad metadata 
  var adMetadata = { 
      CUSTOM_AD_KEY_1 : CUSTOM_AD_VAL_1,  
      CUSTOM_AD_KEY_2 : CUSTOM_AD_VAL_2 
  }; 
  
  // 2. Track the MediaHeartbeat.Event.AdBreakStart event when the preroll pod starts to play.  
  //    Note that since this is a preroll, track the MediaHeartbeat.Event.AdBreakStart  
  //    event before you call trackPlay(). 
  this._mediaheartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo, null); 
  
  ....... 
  ....... 
  
  // 3. Track the MediaHeartbeat.Event.AdStart event when the preroll pod's ad starts to play.  
  //    Note that since this is a preroll, track the MediaHeartbeat.Event.AdStart event before  
  //    you call trackPlay(). 
  this._mediaheartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
  
  ....... 
  ....... 
  
  // 4. Call trackPlay() when the playback actually starts, i.e., the first frame of the  
        main content is rendered on the screen.  
  this._mediaHeartbeat.trackPlay(); 
  
  ....... 
  ....... 
  
  // 5. Track event MediaHeartbeat.Event.AdComplete when the ad reaches the end,  
  //    i.e., when it completes and finishes playing. 
  this._mediaheartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
  
  ....... 
  ....... 
  
  // 6. Track the MediaHeartbeat.Event.AdStart event when the preroll pod's second  
  //    ad starts to play. 
  this._mediaheartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
  
  ....... 
  ....... 
  
  // 7. Track the MediaHeartbeat.Event.AdComplete event when the second ad reaches  
  //    the end, i.e., when it completes and finishes playing. 
  this._mediaheartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
  
  ....... 
  ....... 
  
  // 8. Track the MediaHeartbeat.Event.AdBreakComplete event when all the ads  
  //    in the pod finish playing. 
  this._mediaheartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
  
  ....... 
  ....... 
  
  // 9. Call trackComplete() when the playback reaches the end, i.e., when it 
  //    completes and finishes playing.  
  this._mediaHeartbeat.trackComplete(); 
  
  // 10. Call trackSessionEnd() when the playback session is over. This method must  
  //     be called even if the user does not watch the video to completion. 
  this._mediaHeartbeat.trackSessionEnd(); 
  
  ....... 
  .......
  ```

## Voorbeeldcode voor meerdere advertentiepunten {#sample-code-for-multiple-ad-breaks}

In dit scenario wordt VOD-inhoud afgespeeld met een pre-roll-advertentie, de inhoud, een mid-roll-advertentie, de inhoud en een post-roll-advertentie.

![](assets/ad-content-regular-playback.png)

* **Android** om dit scenario in Android te bekijken, opstelling de volgende code:

  ```java
  // Set up mediaObject 
  MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
      Configuration.MEDIA_NAME,  
      Configuration.MEDIA_ID,  
      Configuration.MEDIA_LENGTH,  
      MediaHeartbeat.StreamType.VOD 
  ); 
  
  HashMap<String, String> videoMetadata = new HashMap<String, String>(); 
  videoMetadata.put(CUSTOM_KEY_1, CUSTOM_VAL_1); 
  videoMetadata.put(CUSTOM_KEY_2, CUSTOM_VAL_2); 
  
  // 1. Call trackSessionStart() when the user clicks Play or if autoplay is used,  
  //   i.e., there's an intent to start playback. 
  _mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 
  
  ...... 
  ...... 
  
  // Pre-roll 
  MediaObject adBreakInfo =  
    MediaHeartbeat.createAdBreakObject(ADBREAK_NAME,  
                                       ADBREAK_POSITION,  
                                       ADBREAK_START_TIME); 
  MediaObject adInfo = MediaHeartbeat.createAdObject(AD_NAME,  
                                                     AD_ID,  
                                                     AD_POSITION,  
                                                     AD_LENGTH); 
  
  // Context ad data 
  HashMap<String, String> adMetadata = new HashMap<String, String>(); 
  adMetadata.put(CUSTOM_KEY_1, CUSTOM_VAL_1); 
  adMetadata.put(CUSTOM_KEY_2, CUSTOM_VAL_2); 
  
  // 2. Track the MediaHeartbeat.Event.AdBreakStart event when the pre-roll pod  
  //    starts to play. Note that since this is a pre-roll, you must track the  
  //    "MediaHeartbeat.Event.AdBreakStart" event before you call trackPlay().  
  _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo, null); 
  
  ....... 
  ....... 
  
  // 3. Track the MediaHeartbeat.Event.AdStart event when the pre-roll pod's ad  
  //    starts to play. Note that since this is a pre-roll, you must track the  
  //    "MediaHeartbeat.Event.AdStart" event before you call trackPlay().  
  _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
  
  ....... 
  ....... 
  
  // 4. Call trackPlay() when the playback actually starts, i.e., when the first  
  //    frame of the main content is rendered on the screen.  
  _mediaHeartbeat.trackPlay(); 
  
  ....... 
  ....... 
  
  // 5. Track the MediaHeartbeat.Event.AdComplete event when the ad reaches the end,  
  //    i.e., when the ad completes and finishes playing.  
  _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete, null, null); 
  
  ....... 
  ....... 
  
  // 6. Track the MediaHeartbeat.Event.AdBreakComplete event when all of the ads in  
  //;    the pod finish playing. 
  _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete, null, null); 
  
  ....... 
  ....... 
  
  // Mid-roll 
  MediaObject adBreakInfo =  
    MediaHeartbeat.createAdBreakObject(mid-roll_BREAK_NAME,  
                                       mid-roll_BREAK_POSITION,  
                                       mid-roll_BREAK_START_TIME); 
  MediaObject adInfo =  
    MediaHeartbeat.createAdObject(mid-roll_AD_NAME,  
                                  mid-roll_AD_ID,  
                                  mid-roll_AD_POSITION,  
                                  mid-roll_AD_LENGTH); 
  
  // Context ad data 
  HashMap<String, String> adMetadata = new HashMap<String, String>(); 
  adMetadata.put(CUSTOM_KEY_1, CUSTOM_VAL_1); 
  adMetadata.put(CUSTOM_KEY_2, CUSTOM_VAL_2); 
  
  // 7. Track the MediaHeartbeat.Event.AdBreakStart event when the mid-roll pod  
  //    starts to play.  
  _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo, null); 
  
  ....... 
  ....... 
  
  // 8. Track the MediaHeartbeat.Event.AdStart event when the mid-roll pod's ad  
  //    starts to play.  
  _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
  
  ....... 
  ....... 
  
  // 9. Track the MediaHeartbeat.Event.AdComplete event when the ad reaches the end,  
  //    i.e., when the adcompletes and finishes playing.  
  _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete, null, null); 
  
  ....... 
  ....... 
  
  // 10. Track the MediaHeartbeat.Event.AdBreakComplete event when all the ads in the  
  //      mid-roll pod finish playing.  
  _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete, null, null); 
  
  ....... 
  ....... 
  
  // Post-roll 
  MediaObject adBreakInfo =  
    MediaHeartbeat.createAdBreakObject(POSTROLL_BREAK_NAME,  
                                       POSTROLL_BREAK_POSITION,  
                                       POSTROLL_BREAK_START_TIME); 
  MediaObject adInfo =  
    MediaHeartbeat.createAdObject(POSTROLL_AD_NAME,  
                                  POSTROLL_AD_ID,  
                                  POSTROLL_AD_POSITION,  
                                  POSTROLL_AD_LENGTH); 
  
  // Context ad data 
  HashMap<String, String> adMetadata = new HashMap<String, String>(); 
  adMetadata.put(CUSTOM_KEY_1, CUSTOM_VAL_1); 
  adMetadata.put(CUSTOM_KEY_2, CUSTOM_VAL_2); 
  
  // 11. Track the MediaHeartbeat.Event.AdBreakStart event when the post-roll pod  
  //     starts to play.  
  _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo, null); 
  
  ....... 
  ....... 
  
  // 12. Track the MediaHeartbeat.Event.AdStart event when the post-roll pod's  
  //     ad starts to play.  
  _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
  
  ....... 
  ....... 
  
  // 13. Track the MediaHeartbeat.Event.AdComplete event when the ad reaches the  
  //     end, i.e., when the ad completes and finishes playing. 
  _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete, null, null); 
  
  ....... 
  ....... 
  
  // 14. Track the MediaHeartbeat.Event.AdBreakComplete event when all the ads in  
  //     the post-roll pod finish playing.  
  _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete, null, null); 
  
  ....... 
  ....... 
  
  // 15. Call trackComplete() when the playback reaches the end, i.e., when the 
  //     video completes and finishes playing. 
  _mediaHeartbeat.trackComplete(); 
  
  ........ 
  ........ 
  
  // 16. Call trackSessionEnd() when the playback session is over. This method  
  //     must be called even if the user does not watch the video to completion.  
  _mediaHeartbeat.trackSessionEnd(); 
  
  ........ 
  ........ 
  ```

* **iOS** om dit scenario in iOS te bekijken, opstelling de volgende code:

  ```
  //  Set up mediaObject 
  ADBMediaObject *mediaObject =  
    [ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                       length:MEDIA_LENGTH  
                       streamType:ADBMediaHeartbeatStreamTypeVOD]; 
  
  NSMutableDictionary *videoContextData =  
    [[NSMutableDictionary alloc] init]; 
  [videoContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
  [videoContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
  
  // 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
  //    i.e., there is an intent to start playback. 
  [_mediaHeartbeat trackSessionStart:mediaObject data:videoContextData]; 
  ....... 
  ....... 
  
  // Pre-roll 
  ADBMediaObject *adBreakInfo =  
    [ADBMediaHeartbeat createAdBreakObjectWithName:AD_BREAK_NAME  
                       position:AD_BREAK_POSITION  
                       startTime:AD_BREAK_START_TIME]; 
  ADBMediaObject *adInfo =  
    [ADBMediaHeartbeat createAdObjectWithName:AD_NAME  
                       adId:AD_ID  
                       position:AD_POSITION  
                       length:AD_LENGTH]; 
  
  // Context ad data 
  NSMutableDictionary *adDictionary =  
    [[NSMutableDictionary alloc] init]; 
  [adDictionary setObject:@"custom-val1" forKey:@"custom-key1"]; 
  [adDictionary setObject:@"custom-val2" forKey:@"custom-key2"]; 
  
  // 2. Track the ADBMediaHeartbeatEventAdBreakStart event when the  
  //    pre-roll pod starts to play. Note that since this is a pre-roll,  
  //    you must track the ADBMediaHeartbeatEventAdBreakStart event  
  //    before you call trackPlay. 
  [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakStart  
                   mediaObject:adBreakObject  
                   data:adDictionary]; 
  ....... 
  ....... 
  
  // 3. Track the ADBMediaHeartbeatEventAdStart when the pre-roll  
  //    pod's ad starts to play. Note that since this is a pre-roll,  
  //    you must track the ADBMediaHeartbeatEventAdStart before you 
  //    call trackPlay. 
  [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdStart  
                    mediaObject:adObject  
                    data:adDictionary]; 
  ....... 
  ....... 
  
  // 4. Call trackPlay when the playback actually starts, i.e., when 
  //    the first frame of the main content is rendered on the screen. 
  [_mediaHeartbeat trackPlay]; 
  ....... 
  ....... 
  
  // 5. Track the ADBMediaHeartbeatEventAdComplete event when the ad  
  //    reaches the end, i.e., when it completes and finishes playing. 
  [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdComplete  
                    mediaObject:nil  
                    data:nil]; 
  ....... 
  ....... 
  
  // 6. Track the ADBMediaHeartbeatEventAdBreakComplete event when all  
  //    of the ads in the pod finish playing. 
  [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakComplete  
                    mediaObject:nil  
                    data:nil]; 
  ....... 
  ....... 
  
  // Mid-roll 
  ADBMediaObject *adBreakInfo =  
    [ADBMediaHeartbeat createAdBreakObjectWithName:MIDROLL_BREAK_NAME  
                       position:MIDROLL_BREAK_POSITION  
                       startTime:MIDROLL_BREAK_START_TIME]; 
  ADBMediaObject *adInfo =  
    [ADBMediaHeartbeat createAdObjectWithName:MIDROLL_AD_NAME  
                       adId:MIDROLL_AD_ID position:MIDROLL_AD_POSITION  
                       length:MIDROLL_AD_LENGTH]; 
  
  // context ad data 
  NSMutableDictionary *midrollAdDictionary = [[NSMutableDictionary alloc] init]; 
  [midrollAdDictionary setObject:@"custom-val1" forKey:@"custom-key1"]; 
  [midrollAdDictionary setObject:@"custom-val2" forKey:@"custom-key2"]; 
  
  // 7. Track the ADBMediaHeartbeatEventAdBreakStart event when the mid-roll pod  
  //    starts to play. 
  [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakStart  
                    mediaObject:adBreakObject  
                    data:nil]; 
  ....... 
  ....... 
  
  // 8. Track the ADBMediaHeartbeatEventAdStart event when the mid-roll pod's  
  //    ad starts to play. 
  [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdStart  
                   mediaObject:adObject  
                   data:midrollAdDictionary]; 
  ....... 
  ....... 
  
  // 9. Track the ADBMediaHeartbeatEventAdComplete event when the ad reaches  
  //    the end, i.e., when it completes and finishes playing. 
  [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdComplete  
                   mediaObject:nil  
                   data:nil]; 
  ....... 
  ....... 
  
  // 10. Track the ADBMediaHeartbeatEventAdBreakComplete event when all the  
  //     ads in the mid-roll pod finish playing. 
  [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakComplete  
                   mediaObject:nil  
                   data:nil]; 
  ....... 
  ....... 
  
  // Post-roll 
  ADBMediaObject *postrollBreakInfo =  
    [ADBMediaHeartbeat createAdBreakObjectWithName:POSTROLL_BREAK_NAME  
                       position:POSTROLL_BREAK_POSITION  
                       startTime:POSTROLL_BREAK_START_TIME]; 
  ADBMediaObject *adInfo =  
    [ADBMediaHeartbeat createAdObjectWithName:POSTROLL_AD_NAME  
                       adId:POSTROLL_AD_ID  
                       position:POSTROLL_AD_POSITION  
                       length:POSTROLL_AD_LENGTH]; 
  
  // Context ad data 
  NSMutableDictionary *postrollAdDictionary =  
    [[NSMutableDictionary alloc] init]; 
  [postrollAdDictionary setObject:@"custom-val1" forKey:@"custom-key1"]; 
  [postrollAdDictionary setObject:@"custom-val2" forKey:@"custom-key2"]; 
  
  // 11. Track the ADBMediaHeartbeatEventAdBreakStart event when the  
  //     post-roll pod starts to play. 
  [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakStart  
                   mediaObject:adBreakObject  
                   data:nil]; 
  ....... 
  ....... 
  
  // 12. Track the ADBMediaHeartbeatEventAdStart event when the  
  //     post-roll pod's ad starts to play. 
  [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdStart  
                   mediaObject:adObject  
                   data:postrollAdDictionary]; 
  ....... 
  ....... 
  
  // 13. Track the ADBMediaHeartbeatEventAdComplete event when the  
  //     post-roll pod's ad finishes playing. 
  [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdComplete  
                   mediaObject:nil  
                   data:nil]; 
  ....... 
  ....... 
  
  // 14. Track the ADBMediaHeartbeatEventAdBreakComplete event when  
  //     all the ads in the post-roll pod finish playing. 
  [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakComplete  
                   mediaObject:nil data:nil]; 
  ....... 
  ....... 
  
  // 15. Call trackComplete when the playback reaches the end,  
  //     i.e., when the video completes and finishes playing. 
  [_mediaHeartbeat trackComplete]; 
  ....... 
  ....... 
  
  // 16. Call trackSessionEnd when the playback session is over. This method  
  //     must be called even if the user does not watch the video to completion. 
  [_mediaHeartbeat trackSessionEnd]; 
  ....... 
  ....... 
  ```

* **JavaScript** om dit scenario in JavaScript te bekijken, ga de volgende tekst in:

  ```js
  // Set up mediaObject 
  MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
      Configuration.MEDIA_NAME,  
      Configuration.MEDIA_ID,  
      Configuration.MEDIA_LENGTH,  
      MediaHeartbeat.StreamType.VOD 
  ); 
  
  var videoMetadata = { 
      CUSTOM_KEY_1 : CUSTOM_VAL_1,  
      CUSTOM_KEY_2 : CUSTOM_VAL_2,  
      CUSTOM_KEY_3 : CUSTOM_VAL_ 
  }; 
  
  // 1. Call trackSessionStart() when Play is clicked or if autoplay is used,  
  //    i.e., when there's an intent to start playback.  
  this._mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 
  
  ...... 
  ...... 
  
  // Preroll 
  var adBreakInfo =  
    MediaHeartbeat.createAdBreakObject(ADBREAK_NAME,  
                                       ADBREAK_POSITION,  
                                       ADBREAK_START_TIME); 
  var adInfo =  
    MediaHeartbeat.createAdObject(AD_NAME,  
                                  AD_ID,  
                                  AD_POSITION,  
                                  AD_LENGTH); 
  
  // Custom ad metadata 
  var adMetadata = { 
      CUSTOM_KEY_1 : CUSTOM_VAL_1,  
      CUSTOM_KEY_2 : CUSTOM_VAL_2 
  
  }; 
  
  // 2. Track the MediaHeartbeat.Event.AdBreakStart event when the preroll pod  
  //    starts to play. Note that since this is a preroll, you must track the  
  //    MediaHeartbeat.Event.AdBreakStart event before you call trackPlay().  
  this._trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo, null); 
  
  ....... 
  ....... 
  
  // 3. Track the MediaHeartbeat.Event.AdStart event when the preroll pod's ad  
  //    starts to play. Note that since this is a preroll, you must track the 
  //    MediaHeartbeat.Event.AdStart event before you call trackPlay().  
  this._heartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
  
  ....... 
  ....... 
  
  // 4. Call trackPlay() when the main content actually starts, i.e., when the  
  //    first frame of the video content is rendered on the screen.  
  this._mediaHeartbeat.trackPlay(); 
  
  ....... 
  ....... 
  
  // 5. Track the MediaHeartbeat.Event.AdComplete event when the ad reaches the end,  
  //    i.e., when the ad completes and finishes playing. 
  this._heartbeat.trackEvent(MediaHeartbeat.Event.AdComplete, null, null); 
  
  ....... 
  ....... 
  
  // 6. Track the MediaHeartbeat.Event.AdBreakComplete event when all of the ads in  
  //    the pod finish playing. 
  this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
  
  ....... 
  ....... 
  
  // Midroll 
  var adBreakInfo =  
    MediaHeartbeat.createAdBreakObject(MIDROLL_BREAK_NAME,  
                                       MIDROLL_BREAK_POSITION,  
                                       MIDROLL_BREAK_START_TIME); 
  var adInfo =  
    MediaHeartbeat.createAdObject(MIDROLL_AD_NAME,  
                                  MIDROLL_AD_ID, 
                                  MIDROLL_AD_POSITION,  
                                  MIDROLL_AD_LENGTH); 
  
  // Custom ad metadata 
  var adMetadata = { 
      CUSTOM_KEY_1 : CUSTOM_VAL_1,  
      CUSTOM_KEY_2 : CUSTOM_VAL_2 
  
  }; 
  
  // 7. Track the MediaHeartbeat.Event.AdBreakStart event when the  
  //    midroll pod starts to play. 
  this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo); 
  
  ....... 
  ....... 
  
  // 8. Track the MediaHeartbeat.Event.AdStart event when the midroll  
  //    pod's ad starts to play. 
  this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart,  
                                  adInfo,  
                                  adMetadata); 
  
  ....... 
  ....... 
  
  // 9. Track the MediaHeartbeat.Event.AdComplete event when the ad  
  //    reaches the end, i.e., when the ad completes and finishes playing.  
  this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
  
  ....... 
  ....... 
  
  // 10. Track the MediaHeartbeat.Event.AdBreakComplete event when all of  
  //     the ads in the midroll pod finish playing. 
  this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
  
  ....... 
  ....... 
  
  // Set up mediaObject 
  var mediaInfo = MediaHeartbeat.createMediaObject( 
      Configuration.MEDIA_NAME,  
      Configuration.MEDIA_ID,  
      Configuration.MEDIA_LENGTH,  
      MediaHeartbeat.StreamType.VOD 
  
  ); 
  
  var videoMetadata = { 
      CUSTOM_KEY_1 : CUSTOM_VAL_1,  
      CUSTOM_KEY_2 : CUSTOM_VAL_2,  
      CUSTOM_KEY_3 : CUSTOM_VAL_3 
  
  }; 
  
  // 1. Call trackSessionStart() when Play is clicked or if autoplay  
  //    is used, i.e., when there's an intent to start playback. 
  this._mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 
  
  ...... 
  ...... 
  
  // Preroll 
  var adBreakInfo =  
    MediaHeartbeat.createAdBreakObject(ADBREAK_NAME,  
                                       ADBREAK_POSITION,  
                                       ADBREAK_START_TIME); 
  var adInfo =  
    MediaHeartbeat.createAdObject(AD_NAME,  
                                  AD_ID,  
                                  AD_POSITION,  
                                  AD_LENGTH); 
  
  // Custom ad metadata 
  var adMetadata = { 
     CUSTOM_KEY_1 : CUSTOM_VAL_1,  
     CUSTOM_KEY_2 : CUSTOM_VAL_2 
  
  }; 
  
  // 2. Track the MediaHeartbeat.Event.AdBreakStart event when the preroll pod  
  //    starts to play. Note that since this is a preroll, you must track the   
  //    MediaHeartbeat.Event.AdBreakStart event before you call trackPlay(). 
  this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo); 
  
  ....... 
  ....... 
  
  // 3. Track the MediaHeartbeat.Event.AdStart event when the preroll pod's  
  //    ad starts to play. Note that since this is a preroll, you must track   
  //    the MediaHeartbeat.Event.AdStart event before you call trackPlay(). 
  this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
  
  ....... 
  ....... 
  
  // 4. Call trackPlay() when the playback actually starts, i.e., when the first  
  //    frame of the main content is rendered on the screen.  
  _mediaHeartbeat.trackPlay(); 
  
  ....... 
  ....... 
  
  // 5. Track the MediaHeartbeat.Event.AdComplete event when the ad reaches  
  //    the end, i.e., when the ad completes and finishes playing. 
  this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
  
  ....... 
  ....... 
  
  // 6. Track the MediaHeartbeat.Event.AdBreakComplete event when all  
  //    of the ads in the pod finish playing. 
  this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
  
  ....... 
  ....... 
  
  // Mid-roll 
  var adBreakInfo =  
    MediaHeartbeat.createAdBreakObject(MIDROLL_BREAK_NAME, 
                                       MIDROLL_BREAK_POSITION,  
                                       MIDROLL_BREAK_START_TIME); 
  var adInfo =  
    MediaHeartbeat.createAdObject(MIDROLL_AD_NAME,  
                                  MIDROLL_AD_ID,  
                                  MIDROLL_AD_POSITION,  
                                  MIDROLL_AD_LENGTH); 
  
  // Custom ad metadata 
  var adMetadata = { 
     CUSTOM_KEY_1 : CUSTOM_VAL_1,  
     CUSTOM_KEY_2 : CUSTOM_VAL_2 
  
  }; 
  
  // 7. Track the MediaHeartbeat.Event.AdBreakStart event when the midroll  
  //    pod starts to play. 
  this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo); 
  
  ....... 
  ....... 
  
  // 8. Track the MediaHeartbeat.Event.AdStart event when the midroll pod's  
  //    ad starts to play. 
  this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
  
  ....... 
  ....... 
  
  // 9. Track the MediaHeartbeat.Event.AdComplete event when the ad reaches  
  //    the end, i.e., when the ad completes and finishes playing. 
  this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
  
  ....... 
  ....... 
  
  // 10. Track the MediaHeartbeat.Event.AdBreakComplete event when all  
  //     of the ads in the midroll pod finish playing. 
  this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
  
  ....... 
  ....... 
  
  // Postroll 
  var adBreakInfo = MediaHeartbeat.createAdBreakObject(POSTROLL_BREAK_NAME,  
  POSTROLL_BREAK_POSITION, POSTROLL_BREAK_START_TIME); 
  var adInfo = MediaHeartbeat.createAdObject(POSTROLL_AD_NAME, POSTROLL_AD_ID,  
  POSTROLL_AD_POSITION, POSTROLL_AD_LENGTH); 
  
  // Custom ad metadata 
  var adMetadata = { 
     CUSTOM_KEY_1 : CUSTOM_VAL_1,  
     CUSTOM_KEY_2 : CUSTOM_VAL_2 
  
  }; 
  
  // 11. Track the MediaHeartbeat.Event.AdBreakStart event when the postroll  
  //     pod starts to play. 
  this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo); 
  
  ....... 
  ....... 
  
  // 12. Track the MediaHeartbeat.Event.AdStart event when the postroll pod's ad  
  //     starts to play. 
  this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
  
  ....... 
  ....... 
  
  // 13. Track the MediaHeartbeat.Event.AdComplete event when the ad reaches   
  //     the end, i.e., when the ad completes and finishes playing. 
  this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
  
  ....... 
  ....... 
  
  // 14. Track the MediaHeartbeat.Event.AdBreakComplete event when all of  
  //     the ads in the postroll pod finish playing. 
  this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
  
  ....... 
  ....... 
  
  // 15. Call trackComplete() when the playback reaches the end, i.e., when playback 
  //     completes and finishes playing. 
  this._mediaHeartbeat.trackComplete(); 
  
  ........ 
  ........ 
  
  // 16. Call trackSessionEnd() when the playback session is over. This method must be called  
  //     even if the user does 
  not watch the video to completion. 
  this._mediaHeartbeat.trackSessionEnd(); 
  
  ........ 
  ........ 
  ```
