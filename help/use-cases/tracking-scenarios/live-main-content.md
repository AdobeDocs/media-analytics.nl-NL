---
title: Actieve hoofdinhoud
description: Bekijk een voorbeeld van hoe u live-inhoud kunt bijhouden met de Media SDK.
uuid: e92e99f4-c395-48aa-8a30-cbdd2f5fc07c
exl-id: f6a00ffd-da6a-4d62-92df-15d119cfc426
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 0%

---

# Actieve hoofdinhoud{#live-main-content}

## Scenario {#scenario}

In dit scenario is er één actief dat gedurende 40 seconden geen advertenties bevat nadat de live stream is samengevoegd.

| Trigger | Hartslagmethode | Netwerkaanroepen | Notities   |
|---|---|---|---|
| Gebruiker klikt **[!UICONTROL Play]** | `trackSessionStart` | Start inhoud analyse, Start inhoud hartslag | Dit kan een gebruiker zijn die **[!UICONTROL Play]** klikt of een automatisch afgespeelde gebeurtenis. |
| Het eerste frame van de media wordt afgespeeld. | `trackPlay` | Hartslaginhoud afspelen | Deze methode activeert de timer. Hartslagen worden elke 10 seconden verzonden zolang het afspelen duurt. |
| De inhoud wordt afgespeeld. |  | Content Heartbeats |  |
| De sessie is afgelopen. | `trackSessionEnd` |  | `SessionEnd` betekent het einde van een weergavesessie. Deze API moet worden aangeroepen, zelfs als de gebruiker de media niet voor voltooiing gebruikt. |

## Parameters {#parameters}

Veel van de zelfde waarden die u op de Vraag van het Begin van de Inhoud van Adobe Analytics ziet zult u ook op de Vraag van het Begin van de Inhoud van de Hartslag zien. U zult ook veel andere parameters zien die Adobe gebruikt om de verschillende Media-rapporten in Adobe Analytics te vullen. We zullen ze hier niet allemaal behandelen, alleen de echt belangrijke.

### Begin van hartslaginhoud

| Parameter | Waarde | Notities |
|---|---|---|
| `s:sc:rsid` | &lt;Uw Adobe-rapportsuite-id> |  |
| `s:sc:tracking_serve` | &lt;Uw URL voor Analytics Tracking Server> |  |
| `s:user:mid` | `s:user:mid` | Moet overeenkomen met de gemiddelde waarde van de Adobe Analytics Content Start Call |
| `s:event:type` | &quot;start&quot; |  |
| `s:asset:type` | &quot;main&quot; |  |
| `s:asset:mediao_id` | &lt;Uw mediumnaam> |  |
| `s:stream:type` | leven |  |
| `s:meta:*` | optioneel | Aangepaste metagegevens ingesteld op het medium |

## Content Heartbeats {#content-heartbeats}

Tijdens het afspelen van media is er een timer die een of meer hartslagen (of pingelt) om de 10 seconden verzendt voor de hoofdinhoud en elke seconde voor advertenties. Deze hartslagen bevatten informatie over afspelen, advertenties, buffering en een aantal andere elementen. De exacte inhoud van elke hartslag valt buiten het bereik van dit document. Het belangrijkste voor validatie is dat hartslagen consistent worden geactiveerd terwijl het afspelen wordt voortgezet.

Zoek in de inhoudslooplijst naar een aantal specifieke dingen:

| Parameter | Waarde | Notities |
|---|---|---|
| `s:event:type` | &quot;play&quot; |  |
| `l:event:playhead` | &lt;positie van afspeelkop> bijv. 50, 60, 70 | Dit moet de huidige positie van de afspeelkop aangeven. |

## Hartslaginhoud voltooid {#heartbeat-content-complete}

Er zal geen volledige vraag in dit scenario zijn, omdat de levende stroom nooit werd voltooid.

## Waardeinstellingen afspeelkop

Voor LIVE-streams moet u de waarde van de afspeelkop instellen als het aantal seconden sinds middernacht van de UTC op die dag, zodat analisten in de rapportage kunnen bepalen op welk punt gebruikers zich aansluiten bij en de LIVE-stream verlaten binnen een weergave van 24 uur.

### Bij starten

Wanneer een gebruiker de stream afspeelt bij LIVE-media, moet u `l:event:playhead` instellen op het aantal seconden dat is verstreken sinds middernacht van de UTC op die dag. Dit is in tegenstelling tot VOD, waar u playhead aan &quot;0&quot;zou plaatsen. Opmerking: wanneer u voortgangsmarkeringen gebruikt, is de duur van de inhoud vereist en moet de afspeelkop worden bijgewerkt in het aantal seconden vanaf het begin van het media-item, te beginnen met 0.

Bijvoorbeeld, zeg een LIVE het stromen gebeurtenis begint bij middernacht en looppas 24 uren (`a.media.length=86400`; `l:asset:length=86400`). Stel vervolgens dat een gebruiker die LIVE-stream begint af te spelen om 12:00 uur. In dit scenario moet u `l:event:playhead` instellen op 43200 (12 uur sinds middernacht UTC op die dag in seconden).

### Bij pauzeren

Dezelfde logica &#39;live playhead&#39; die aan het begin van het afspelen is toegepast, moet worden toegepast wanneer een gebruiker het afspelen pauzeert. Wanneer de gebruiker aan het spelen van de LIVE stroom terugkeert, moet u de `l:event:playhead` waarde volgens het nieuwe aantal seconden sinds middernacht UTC plaatsen, _niet_ aan het punt waar de gebruiker de LIVE stroom pauzeerde.

## Voorbeeldcode {#sample-code}

![](assets/live-content-playback.png)

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
//    i.e., there is an intent to start playback.  
_mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the first  
//    frame of main content is rendered on the screen. 
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackSessionEnd() when user ends the playback session.  
//    Since the user does not watch live media to completion, there  
//    is no need to call trackComplete().  
_mediaHeartbeat.trackSessionEnd(); 
....... 
....... 
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
//    frame of the main content is rendered on the screen. 
[_mediaHeartbeat trackPlay]; 
....... 
....... 
 
// 3. Call trackSessionEnd when user ends the playback session. Since the user  
//    does not watch live media to completion, there is no need to call  
//    trackComplete. 
[_mediaHeartbeat trackSessionEnd]; 
........ 
........ 
```

### JavaScript

Hier volgt de verwachte API-oproepvolgorde:

```js
// Set up mediaObject 
var mediaInfo =  
MediaHeartbeat.createMediaObject(Configuration.MEDIA_NAME,  
                                 Configuration.MEDIA_ID,  
                                 Configuration.MEDIA_LENGTH,  
                                 MediaHeartbeat.StreamType.VOD); 

var mediaMetadata = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 
}; 

// 1. Call trackSessionStart() when Play is clicked or if autoplay  
//    is used, i.e., there's an intent to start playback. 
this._mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the  
//    first frame of media is rendered on the screen. 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackSessionEnd() when user ends the playback session.  
//    Since user does not watch live media to completion, there is  
//    no need to call trackComplete(). 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........ 
```
