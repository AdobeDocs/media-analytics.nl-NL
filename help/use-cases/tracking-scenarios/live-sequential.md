---
title: Actieve hoofdinhoud met opeenvolgende reeksspatiëring
description: Bekijk een voorbeeld van hoe u live-inhoud kunt bijhouden met sequentiële tracking met de Media SDK.
uuid: b03477b6-9be8-4b67-a5a0-4cef3cf262ab
exl-id: 277a72b8-453b-41e5-b640-65c43587baf8
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# Actieve hoofdinhoud met opeenvolgende spatiëring{#live-main-content-with-sequential-tracking}

## Scenario {#scenario}

In dit scenario is er één actief dat gedurende 40 seconden geen advertenties bevat nadat de live stream is samengevoegd.

Dit is het zelfde scenario zoals de [&#x200B; playback van VOD zonder advertenties &#x200B;](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md) scenario, maar een deel van de inhoud wordt geschaad door en een vraag wordt voltooid van één punt in belangrijkste inhoud aan een ander punt.

| Trigger | Hartslagmethode |  Netwerkaanroepen  |  Notities   |
| --- | --- | --- | --- |
| Gebruiker klikt [!UICONTROL Play] | trackSessionStart | Start inhoud analyse, Start inhoud hartslag | De metingsbibliotheek is zich niet bewust dat er een pre-rol advertentie is, zodat zijn deze netwerkvraag identiek aan de [&#x200B; playback van VOD zonder advertenties &#x200B;](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md) scenario. |
| Het eerste frame van de inhoud wordt afgespeeld. | trackPlay | Hartslaginhoud afspelen | Wanneer de hoofdstukinhoud vóór hoofdinhoud wordt afgespeeld, begint de hartslag wanneer het hoofdstuk begint. |
| Inhoud afspelen | | Content Heartbeats | Deze netwerkvraag is precies het zelfde als de [&#x200B; playback van VOD zonder advertenties &#x200B;](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md) scenario. |
| Session1 Boven (Aflevering1 beëindigd) | trackComplete / trackSessionEnd | Hartslaginhoud voltooid | Complete betekent dat session1 voor de eerste aflevering is bereikt en volledig is gecontroleerd. Deze sessie moet worden beëindigd voordat de sessie voor de volgende aflevering wordt gestart. |
| Episode2 begonnen (Sessie2 start) | trackSessionStart | Begin hartslaginhoud voor analyse inhoud | De reden hiervoor is dat de gebruiker de eerste aflevering heeft bekeken en verder heeft gekeken naar een andere aflevering |
| Eerste frame van media | trackPlay | Hartslaginhoud afspelen | Deze methode activeert de timer en vanaf dit punt worden hartslagen elke 10 seconden verzonden zolang het afspelen wordt voortgezet. |
| Inhoud afspelen | | Content Heartbeats | |
| Sessie over (Episode2 beëindigd) | trackComplete / trackSessionEnd | Hartslaginhoud voltooid | Complete betekent dat session2 voor de tweede aflevering is bereikt en volledig is gecontroleerd. Deze sessie moet worden beëindigd voordat de sessie voor de volgende aflevering wordt gestart. |

## Parameters {#parameters}

### Begin van hartslaginhoud

| Parameter | Waarde | Notities |
|---|---|---|
| `s:sc:rsid` | &lt;Uw Adobe-rapportsuite-id> |  |
| `s:sc:tracking_serve` | &lt;Uw URL voor Analytics Tracking Server> |  |
| `s:user:mid` | `s:user:mid` | Moet overeenkomen met de gemiddelde waarde van de Adobe Analytics Content Start Call |
| `s:event:type` | `"start"` |  |
| `s:asset:type` | `"main"` |  |
| `s:asset:media_id` | &lt;Uw mediumnaam> |  |
| `s:stream:type` | `live` |  |
| `s:meta:*` | *facultatief* | Aangepaste metagegevens ingesteld op het medium |

## Hartslaginhoud afspelen {#heartbeat-content-play}

Dit zou bijna precies als de vraag van het Begin van de Inhoud moeten kijken Heartbeat, maar met het belangrijkste verschil in de &quot;s :event: type&quot;parameter. Alle parameters zouden hier nog moeten zijn.

| Parameter | Waarde | Notities |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `s:asset:type` | `"main"` |  |

## Content Heartbeats {#content-heartbeats}

Tijdens het afspelen van media is er een timer die elke 10 seconden een of meer hartslagen voor de hoofdinhoud en elke seconde voor advertenties verzendt. Deze hartslagen bevatten informatie over afspelen, advertenties, buffering en een aantal andere elementen. De exacte inhoud van elke hartslag valt buiten het bereik van dit document. Het belangrijkste voor validatie is dat hartslagen consistent worden geactiveerd terwijl het afspelen wordt voortgezet.

Zoek in de inhoudslooplijst naar een aantal specifieke dingen:

| Parameter | Waarde | Notities |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `l:event:playhead` | &lt;positie van afspeelkop> bijv. 50, 60, 70 | Dit moet de huidige positie van de afspeelkop aangeven. |

## Hartslaginhoud voltooid {#heartbeat-content-complete}

Wanneer het afspelen voor een bepaalde aflevering is voltooid (de afspeelkop overschrijdt de grens van de aflevering), wordt een volledige aanroep van de inhoud van de hartslag verzonden. Dit kijkt als andere Vraag van de Hartslag, maar zal een paar specifieke dingen bevatten:

| Parameter | Waarde | Notities |
|---|---|---|
| `s:event:type` | `"complete"` |  |
| `s:asset:type` | `"main"` |  |

## Voorbeeldcode {#sample-code}

![](assets/ios-live-noads-multiplesessions.png)

### Android

Hier volgt de verwachte API-oproepvolgorde:

```java
// Set up mediaObject 
MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.LIVE 
); 

HashMap<String, String> mediaMetadata = new HashMap<String, String>(); 
mediaMetadata.put(CUSTOM_VAL_1, CUSTOM_KEY_1); 
mediaMetadata.put(CUSTOM_VAL_2, CUSTOM_KEY_2); 

// 1. Call trackSessionStart() when the user clicks Play or if autoplay is used,  
//    i.e., when there is an intent to start playback.  
_mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the first  
//    frame of main content is rendered on the screen.  
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackComplete() when the playback reaches the end of session,  
//    i.e., when the media completes and finishes playing 1st episode/session.  
_mediaHeartbeat.trackComplete(); 

........ 
........ 

// 4. Call trackSessionEnd() to end session 1 
_mediaHeartbeat.trackSessionEnd(); 

........ 
........ 

// Start tracking session 2 /episode 2 of the same live stream.  
// There is no need to reinstantiate a mediaHeartbeat instance for tracking sesison 2. 
// Set up mediaObject 
MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.LIVE 
); 

HashMap<String, String> mediaMetadata = new HashMap<String, String>(); 
mediaMetadata.put(CUSTOM_VAL_1, CUSTOM_KEY_1); 
mediaMetadata.put(CUSTOM_VAL_2, CUSTOM_KEY_2); 

// 5. Call trackSessionStart() when the playhead reaches a point that denotes the 
//    start of session 2 
_mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 6. Call trackPlay() to start tracking session 2 playback  
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 7. Call trackComplete() when the playback reaches the end of session 2,  
//    i.e., the media completes and finishes playing.  
_mediaHeartbeat.trackComplete(); 

........ 
........ 

// 8. Call trackSessionEnd() to end session 2 
_mediaHeartbeat.trackSessionEnd(); 

........ 
........ 

// Continue similarly tracking further sessions in the live stream if required 
```

### iOS

Hier volgt de verwachte API-oproepvolgorde:

```
// Set up mediaObject 
ADBMediaObject *mediaObject =  
[ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                   length:MEDIA_LENGTH  
                   streamType:ADBMediaHeartbeatStreamTypeLIVE]; 
  
NSMutableDictionary *mediaContextData = [[NSMutableDictionary alloc] init]; 
[mediaContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
[mediaContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
  
// 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback. 
[_mediaHeartbeat trackSessionStart:mediaObject data:mediaContextData]; 
...... 
...... 
  
// 2. Call trackPlay when the playback actually starts, i.e., when the first  
//    frame of main content is rendered on the screen. 
[_mediaHeartbeat trackPlay]; 
....... 
....... 

// 3. Call trackComplete when the playback reaches the end of session,  
//    i.e., when the media completes and finishes playing the first 
//    episode/session. 
[_mediaHeartbeat trackComplete]; 
....... 
....... 

// 4. Call trackSessionEnd to end session 1 
[_mediaHeartbeat trackSessionEnd]; 
........ 
........ 

// Start tracking session 2 / episode 2 of the same live stream, No need to  
// reinstantiate mediaHeartbeat instance for tracking sesison 2. 

// Set up mediaObject 
ADBMediaObject *mediaObject =  
[ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                   length:MEDIA_LENGTH  
                   streamType:ADBMediaHeartbeatStreamTypeLIVE]; 
 
NSMutableDictionary *mediaContextData = [[NSMutableDictionary alloc] init]; 
[mediaContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
[mediaContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
 
// 5. Call trackSessionStart when the playhead reaches a point that denotes  
//    start of session 2 
[_mediaHeartbeat trackSessionStart:mediaObject data:mediaContextData]; 
...... 
...... 
 
// 6. Call trackPlay to start tracking session 2 playback 
[_mediaHeartbeat trackPlay]; 
....... 
....... 
 
// 7. Call trackComplete when the playback reaches the end of session 2,  
//    i.e., when the media completes and finishes playing. 
[_mediaHeartbeat trackComplete]; 
........ 
........ 
 
// 8. Call trackSessionEnd to end the session 2 
[_mediaHeartbeat trackSessionEnd]; 
........ 
........ 

// Continue tracking further sessions in live stream similarly if required 
```

### JavaScript

Hier volgt de verwachte API-oproepvolgorde:

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
//    first frame of media is rendered on the screen. 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackComplete() when the playback reaches the end of a session,  
//    i.e., whn playback completes and finishes playing the 1st episode/session. 
this._mediaHeartbeat.trackComplete(); 

........ 
........ 

// 4. Call trackSessionEnd() to end session 1 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........ 

// Start tracking session 2/episode 2 of the same live stream. There is no need  
// to reinstantiate a mediaHeartbeat instance for tracking sesison 2. 

// Set up mediaObject 
var mediaInfo2 = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.LIVE 
); 

var mediaMetadata2 = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 
}; 

// 5. Call trackSessionStart() when the playhead reaches a point that denotes  
//    the start of session 2 
this._mediaHeartbeat.trackSessionStart(mediaInfo2, mediaMetadata2); 

...... 
...... 

// 6. Call trackPlay() to start tracking session 2 playback 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 7. Call trackComplete() when the playback reaches the end of session 2,  
//    i.e., playback completes and finishes playing. 
this._mediaHeartbeat.trackComplete(); 

........ 
........ 

// 8. Call trackSessionEnd() to end session 2 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........ 

// Continue tracking further sessions in live stream similarly if required 
```
