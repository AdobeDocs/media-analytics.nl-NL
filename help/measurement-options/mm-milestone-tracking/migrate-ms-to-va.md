---
title: Migreren van Milestone naar Media Analytics
description: null
uuid: fdc96146-af63-48ce-b938-c0ca70729277
translation-type: tm+mt
source-git-commit: aa2a230daa96b823f9963345ac4578799e59d3f5
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 10%

---


# Migreren van Milestone naar Media Analytics {#migrating-from-milestone-to-media-analytics}

## Overzicht {#overview}

De kernconcepten van videometing zijn hetzelfde voor Mijlsteen en Media Analytics, die videospelergebeurtenissen neemt en deze toewijst aan analytische methoden, terwijl ze ook metagegevens en waarden van spelers vastzetten en toewijzen aan analytische variabelen. De oplossing van Media Analytics groeide uit Mijlpaal, zo veel van de methodes en metriek zijn het zelfde, echter, is de configuratiebenadering en de code beduidend veranderd. Het zou mogelijk moeten zijn om de spelergebeurteniscode bij te werken om aan de nieuwe methodes van Media Analytics te richten. Zie Overzicht [en Overzicht](/help/sdk-implement/setup/setup-overview.md) van het [](/help/sdk-implement/track-av-playback/track-core-overview.md) Volgen van SDK voor meer details bij het uitvoeren van Media Analytics.

De volgende lijsten verstrekken vertalingen tussen de oplossing van de Mijlpaal en de oplossing van Media Analytics.

## Migratiehandleiding {#migration-guide}

### Referentie variabele

| Mijlsteen, metrisch | Type variabele | Media Analytics Metric |
| --- | --- | --- |
| Inhoud | Vervaldatum<br>eVarDefault: Bezoek | Inhoud |
| Inhoudstype | Standaardvervaldatum van eVar<br> : Paginaweergave | Inhoudstype |
| Tijd van inhoud besteed | Type gebeurtenis<br> : Teller | Tijd van inhoud besteed |
| Video wordt gestart | Type gebeurtenis<br> : Teller | Video wordt gestart |
| Video voltooid | Type gebeurtenis<br> : Teller | Inhoud voltooid |

### Variabelen van de mediamodule

| Mijlsteen | Mijlsteensyntaxis | Media Analytics | Analytics-syntaxis voor media |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | N.v.t. | Alle Media Analytics-gegevens worden alleen verzonden met gebruik van Context Data. |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | N.v.t. | Media Analytics-contextgegevens worden automatisch ingevuld in gereserveerde variabelen. Toewijzing aan eVars, props en gebeurtenissen die ik niet meer nodig heb in de implementatiecode. De klanten kunnen contextgegevens aan variabelen in kaart brengen gebruikend verwerkingsregels. |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | N.v.t. | Niet meer nodig omdat de afbeelding plaatsvindt via gereserveerde variabelen en verwerkingsregels. |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | N.v.t. | Niet meer nodig omdat de afbeelding plaatsvindt via gereserveerde variabelen en verwerkingsregels. |

### Optionele variabelen

| Mijlsteen | Mijlsteensyntaxis | Media Analytics | Analytics-syntaxis voor media |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | N.v.t. | We bieden geen vooraf gebouwde spelertoewijzingen meer. |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | N.v.t. | We bieden geen vooraf gebouwde spelertoewijzingen meer. |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | N.v.t. | Inhoud voltooid ondersteunt alleen een voortgangsmarkering van 100%. |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | N.v.t. | Inhoud voltooid ondersteunt alleen een voortgangsmarkering van 100%. |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | SDK-sleutel: playerName;<br> API-sleutel: media.playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | N.v.t. | Media Analytics wordt ingesteld op 10 seconden voor inhoud en 1 seconde voor advertenties. Er zijn geen andere opties beschikbaar. |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | N.v.t. | Media Analytics houdt voortgangsmarkeringen altijd bij op 10%, 25%, 50%, 75%, 95% |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | N.v.t. | Media Analytics houdt voortgangsmarkeringen altijd bij op 10%, 25%, 50%, 75%, 95% |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | N.v.t. | Auto track is niet meer beschikbaar. |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | N.v.t. | Auto track is niet meer beschikbaar. |

### Variabelen voor bijhouden toevoegen

| Mijlsteen | Mijlsteensyntaxis | Media Analytics | Analytics-syntaxis voor media |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | N.v.t. | Media Analytics wordt ingesteld op 10 seconden voor inhoud en 1 seconde voor advertenties. Er zijn geen andere opties beschikbaar. |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | N.v.t. | Voortgangsmarkeringen worden niet standaard weergegeven voor advertenties. Gebruik berekende metriek om markeringen voor voortgang samen te stellen. |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | N.v.t. | Media Analytics wordt ingesteld op 1 seconde voor advertenties. Er zijn geen andere opties beschikbaar. |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | N.v.t. | Auto track is niet meer beschikbaar. |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | N.v.t. | Auto track is niet meer beschikbaar. |

### Methoden van Media Module

| Mijlsteen | Mijlsteensyntaxis | Media Analytics | Analytics-syntaxis voor media |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | trackSessionStart | `trackSessionStart(` <br> `  mediaObject,` <br> `  contextData)` |
| mediaName - (Vereist) <br> De naam van de video zoals u het in videorapporten wilt verschijnen. | `mediaName` | name | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaLength - (Vereist) <br> De lengte van de video in seconden. | `mediaLength` | length | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaPlayerName - (Vereist) <br> De naam van de mediaspeler die wordt gebruikt om de video weer te geven, zoals u deze wilt weergeven in videoverslagen. | `mediaPlayerName` | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | trackEvent | `mediaHeartbeat.trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdBreakStart, ` <br> `  adBreakObject);` <br> `...` <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdStart, ` <br> `  adObject, ` <br> `  adCustomMetadata);` |
| name - (Required) <br> De naam of identiteitskaart van de advertentie. | `name` | name | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| length - (vereist) <br> De lengte van de advertentie. | `length` | length | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| playerName - (Vereist) <br> De naam van de mediaspeler die wordt gebruikt om de advertentie weer te geven. | `playerName` | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| parentName <br> De naam of id van de primaire inhoud waarin de advertentie is ingesloten. | `parentName` | N.v.t. | Automatisch overgeërfd |
| parentPod <br> De positie in de primaire inhoud de advertentie werd gespeeld. | `parentPod` | position | `createAdBreakObject(` <br> `  name, ` <br> `  position, ` <br> `  startTime)` |
| parentPodPosition <br> De positie in de pod waar de advertentie wordt afgespeeld. | `parentPodPosition` | position | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| CPM <br> CPM of gecodeerde CPM (vooraf bevestigd met &quot;~&quot;) die op deze playback van toepassing is. | `CPM` | N.v.t. | Niet standaard beschikbaar in Media Analytics. |
| Media.click | `s.Media.click(` <br> `  name,` <br> `  offset)` | N.v.t. | Gebruik een aanroep van een aangepaste koppelingsanalyse om kliks bij te houden. |
| Media.close | `s.Media.close(` <br> `  mediaName)` | trackSessionEnd | `trackSessionEnd()` |
| Media.complete | `s.Media.complete(` <br> `  name,` <br> `  offset)` | trackComplete | `trackComplete()` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | trackPlay | `trackPlay()` |
| Media.stop | `s.Media.stop(` <br> `  mediaName,` <br> `  mediaOffset)` | trackPause <br> of <br> trackEvent | `trackPause()` <br> of `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  SeekStart)` <br> of <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  BufferStart);` |
| Media.monitor | `s.Media.monitor(s, media)` | Gebruik aangepaste of standaardmetagegevens om extra variabelen in te stellen. | `var customVideoMetadata = ` <br> `{` <br> `  isUserLoggedIn: ` <br> `    "false",` <br> `  tvStation: ` <br> `    "Sample TV station",` <br> `  programmer: ` <br> `    "Sample programmer"` <br> `};` <br> `...` <br> `var standardVideoMetadata ` <br> `  = {};` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   EPISODE] = ` <br> `  "Sample Episode";` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   SHOW] = "Sample Show";` <br> `...` <br> `mediaObject.setValue(` <br> `  MediaHeartbeat.` <br> `  MediaObjectKey.` <br> `  StandardVideoMetadata, ` <br> `  standardVideoMetadata);` |
| Media.track | `s.Media.track(` <br> `  mediaName)` | N.v.t. | De het volgen vraagfrequentie wordt automatisch geplaatst. |

