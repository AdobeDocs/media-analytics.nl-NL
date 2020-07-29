---
title: Migreren van mijlpaal naar medialanalyse
description: null
uuid: fdc96146-af63-48ce-b938-c0ca70729277
translation-type: tm+mt
source-git-commit: e25c4d0add969ad31393f2eeb33b1a12b7205586
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 12%

---


# Migreren van mijlpaal naar medialanalyse {#migrating-from-milestone-to-media-analytics}

## Overzicht {#overview}

De kernconcepten van videometing zijn het zelfde voor Mijlpaal en de Analyse van Media, die videospelergebeurtenissen neemt en hen in kaart brengt aan analysemethodes, terwijl ook het graven van spelermeta-gegevens en waarden en hen in kaart brengen aan analytische variabelen. De oplossing van de Analyse van Media groeide uit Mijlpaal, zodat zijn veel van de methodes en de metriek het zelfde, nochtans, de configuratiebenadering en de code beduidend veranderd. Het zou mogelijk moeten zijn om de code van de spelergebeurtenis bij te werken om aan de nieuwe methodes van de Analyse van Media te richten. Zie [Overzicht SDK](/help/sdk-implement/setup/setup-overview.md) en [Overzicht volgen](/help/sdk-implement/track-av-playback/track-core-overview.md) voor meer details bij het uitvoeren van de Analyse van Media.

De volgende lijsten verstrekken vertalingen tussen de oplossing van de Mijlpaal en de oplossing van de Analyse van Media.

## Migratiehandleiding {#migration-guide}

### Variabele referentie

| Milestone Metric | Type variabele | Mediaanalyse Metrisch |
| --- | --- | --- |
| Inhoud | eVar <br> Standaardvervaldatum: Bezoek | Inhoud |
| Inhoudstype | eVar <br> Standaardvervaldatum: Pagina-weergave | Inhoudstype |
| Inhoud Tijd besteed | Gebeurtenis <br> Type: Teller | Inhoud Tijd besteed |
| Video start | Gebeurtenis <br> Type: Teller | Video start |
| Video voltooid | Gebeurtenis <br> Type: Teller | Inhoud voltooid |

### Variabelen mediamodule

| Mijlsteen | Milestone Syntax | Mediaanalyse | Mediaanalyticasynbelastingen |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | N.v.t. | Alle gegevens van de Analyse van Media worden slechts verzonden gebruikend de Gegevens van de Context. |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | N.v.t. | De de contextgegevens van de Analyse van media worden automatisch bevolkt in gereserveerde variabelen. Het in kaart brengen aan eVars, steunen, en gebeurtenissen die ik niet meer binnen de implementatiecode nodig had. De klanten kunnen contextgegevens aan variabelen in kaart brengen gebruikend verwerkingsregels. |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | N.v.t. | Niet meer nodig aangezien de afbeelding via gereserveerde variabelen en verwerkingsregels gebeurt. |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | N.v.t. | Niet meer nodig aangezien de afbeelding via gereserveerde variabelen en verwerkingsregels gebeurt. |

### Facultatieve variabelen

| Mijlsteen | Milestone Syntax | Mediaanalyse | Mediaanalyticasynbelastingen |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | N.v.t. | We bieden geen vooraf gebouwde spelerafbeeldingen meer. |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | N.v.t. | We bieden geen vooraf gebouwde spelerafbeeldingen meer. |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | N.v.t. | De inhoud Volledig steunt slechts een 100% vooruitgangsteller. |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | N.v.t. | De inhoud Volledig steunt slechts een 100% vooruitgangsteller. |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | SDK-toets: playerName;<br> API-sleutel: media.playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | N.v.t. | De Analyse van media wordt geplaatst aan 10 seconden voor inhoud en 1 seconde voor advertenties. Er zijn geen andere opties beschikbaar. |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | N.v.t. | Media Analytics volgt altijd vooruitgangsmarkers bij 10%, 25%, 50%, 75%, 95%. |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | N.v.t. | Media Analytics volgt altijd vooruitgangsmarkers bij 10%, 25%, 50%, 75%, 95%. |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | N.v.t. | Automatisch spoor is niet meer beschikbaar. |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | N.v.t. | Automatisch spoor is niet meer beschikbaar. |

### Volgvariabelen voor advertentie

| Mijlsteen | Milestone Syntax | Mediaanalyse | Mediaanalyticasynbelastingen |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | N.v.t. | De Analyse van media wordt geplaatst aan 10 seconden voor inhoud en 1 seconde voor advertenties. Er zijn geen andere opties beschikbaar. |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | N.v.t. | Voortgangsmarkeringen worden standaard niet voor advertenties geleverd. De berekende metriek van het gebruik om tellers te bouwen en vooruit te lopen. |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | N.v.t. | De Analyse van media wordt geplaatst aan 1 seconde voor advertenties. Er zijn geen andere opties beschikbaar. |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | N.v.t. | Automatisch spoor is niet meer beschikbaar. |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | N.v.t. | Automatisch spoor is niet meer beschikbaar. |

### Methoden voor mediamodule

| Mijlsteen | Milestone Syntax | Mediaanalyse | Mediaanalyticasynbelastingen |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | trackSessionStart | `trackSessionStart(` <br> `  mediaObject,` <br> `  contextData)` |
| mediaName | `mediaName`: (vereist) de naam van de video aangezien u het in videorapporten wilt verschijnen. | name | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaLength | `mediaLength`: (vereist) de lengte van de video in seconden. | length | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaPlayerName | `mediaPlayerName`: (vereist) de naam van de media speler die wordt gebruikt om de video te bekijken, aangezien u het in videorapporten wilt verschijnen. | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | trackEvent | `mediaHeartbeat.trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdBreakStart, ` <br> `  adBreakObject);` <br> `...` <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdStart, ` <br> `  adObject, ` <br> `  adCustomMetadata);` |
| naam | `name`: (vereist) de naam of het identificatienummer van de advertentie. | naam | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| lengte | `length`: (vereist) De lengte van de advertentie. | lengte | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| playerName | `playerName`: (vereist) de naam van de media speler die wordt gebruikt om de advertentie te bekijken. | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| parentName | `parentName`: De naam of identiteitskaart van de primaire inhoud waar de advertentie wordt ingebed. | N.v.t. | Automatisch overgenomen. |
| parentPod | `parentPod`: De positie in de primaire inhoud de advertentie werd gespeeld. | position | `createAdBreakObject(` <br> `  name, ` <br> `  position, ` <br> `  startTime)` |
| parentPodPosition | `parentPodPosition`: De positie in de peul waar de advertentie wordt gespeeld. | positie | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| CPM | `CPM`: CPM of gecodeerde CPM (vooraf bepaald met &quot;~&quot;) die op deze playback van toepassing is. | N.v.t. | Niet standaard beschikbaar in Media Analytics. |
| Media.click | `s.Media.click(name, offset)` | N.v.t. | Gebruik een vraag van de de verbindingsanalyse van de douane om kliks te volgen. |
| Media.close | `s.Media.close(mediaName)` | trackSessionEnd | `trackSessionEnd()` |
| Media.complete | `s.Media.complete(name, offset)` | trackComplete | `trackComplete()` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | trackPlay | `trackPlay()` |
| Media.stop | `s.Media.stop(mediaName, mediaOffset)` | trackPauze <br> of <br> trackEvent | `trackPause()` <br> of `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  SeekStart)` <br> of <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  BufferStart);` |
| Media.monitor | `s.Media.monitor(s, media)` | De douane of de standaardmeta-gegevens van het gebruik om extra variabelen te plaatsen. | `var customVideoMetadata = ` <br> `{` <br> `  isUserLoggedIn: ` <br> `    "false",` <br> `  tvStation: ` <br> `    "Sample TV station",` <br> `  programmer: ` <br> `    "Sample programmer"` <br> `};` <br> `...` <br> `var standardVideoMetadata ` <br> `  = {};` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   EPISODE] = ` <br> `  "Sample Episode";` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   SHOW] = "Sample Show";` <br> `...` <br> `mediaObject.setValue(` <br> `  MediaHeartbeat.` <br> `  MediaObjectKey.` <br> `  StandardVideoMetadata, ` <br> `  standardVideoMetadata);` |
| Media.track | `s.Media.track(mediaName)` | N.v.t. | Het volgen van vraagfrequentie is automatisch plaatste. |
