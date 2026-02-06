---
title: Leer hoe u van Mijlsteen naar Media Analytics kunt migreren
description: Leer hoe u Mijlsteenvariabelen wijzigt in Metrics van Media Analytics en Mijlstone-modulemethoden in de syntaxis van Media Analytics.
uuid: fdc96146-af63-48ce-b938-c0ca70729277
exl-id: 655841ed-3a02-4e33-bbc9-46fb14302194
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 12%

---

# Migreren van Mijlsteen naar Media Analytics {#migrating-from-milestone-to-media-analytics}

## Overzicht {#overview}

De kernconcepten van videometing zijn hetzelfde voor Mijlpaal en Media Analytics, die videospelergebeurtenissen neemt en deze toewijst aan analytische methoden, terwijl ook de metagegevens en waarden van de speler worden opgehaald en aan analytische variabelen worden toegewezen. De oplossing van de Analyse van Media groeide uit Mijlpaal, zo veel van de methodes en metriek zijn het zelfde, echter, is de configuratiebenadering en de code beduidend veranderd. Het zou mogelijk moeten zijn om de spelergebeurteniscode bij te werken om aan de nieuwe methodes van de Analyse van Media te richten. Zie [&#x200B; het Overzicht van SDK &#x200B;](/help/legacy/setup/legacy-setup-overview.md) en [&#x200B; het Volgen Overzicht &#x200B;](/help/use-cases/track-av-playback/track-core-overview.md) voor meer details bij het uitvoeren van de Analytics van Media.

De volgende lijsten verstrekken vertalingen tussen de oplossing van de Mijlpaal en de oplossing van de Analyse van Media.

## Migratiehandleiding {#migration-guide}

### Referentie variabele

| Mijlsteen, metrisch | Type variabele | Metrisch voor media-analyse |
| --- | --- | --- |
| Inhoud | eVar <br> Standaardvervaldatum: Bezoek | Inhoud |
| Inhoudstype | eVar <br> Standaardvervaldatum: paginaweergave | Inhoudstype |
| Tijd van inhoud besteed | Event <br> Type: Counter | Tijd van inhoud besteed |
| Video wordt gestart | Event <br> Type: Counter | Video wordt gestart |
| Video voltooid | Event <br> Type: Counter | Inhoud voltooid |


### Variabelen van de mediamodule

| Mijlsteen | Mijlsteensyntaxis | Media Analytics | Syntaxis voor medianalyse |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | N.v.t. | Alle gegevens van de Analyse van Media worden slechts verzonden gebruikend de Gegevens van de Context. |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | N.v.t. | De de contextgegevens van de Analyse van media worden automatisch bevolkt in gereserveerde variabelen. Toewijzing aan eVars, props en gebeurtenissen die ik niet meer nodig heb in de implementatiecode. De klanten kunnen contextgegevens aan variabelen in kaart brengen gebruikend verwerkingsregels. |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | N.v.t. | Niet meer nodig omdat de afbeelding plaatsvindt via gereserveerde variabelen en verwerkingsregels. |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | N.v.t. | Niet meer nodig omdat de afbeelding plaatsvindt via gereserveerde variabelen en verwerkingsregels. |

### Optionele variabelen

| Mijlsteen | Mijlsteensyntaxis | Media Analytics | Syntaxis voor medianalyse |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | N.v.t. | We bieden geen vooraf gebouwde spelertoewijzingen meer. |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | N.v.t. | We bieden geen vooraf gebouwde spelertoewijzingen meer. |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | N.v.t. | Inhoud voltooid ondersteunt alleen een voortgangsmarkering van 100%. |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | N.v.t. | Inhoud voltooid ondersteunt alleen een voortgangsmarkering van 100%. |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | SDK Key: playerName;<br> API Key: media.playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | N.v.t. | Media Analytics wordt ingesteld op 10 seconden voor inhoud en 1 seconde voor advertenties. Geen andere opties beschikbaar. |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | N.v.t. | Media Analytics houdt voortgangsmarkeringen altijd bij op 10%, 25%, 50%, 75% en 95%. |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | N.v.t. | Media Analytics houdt voortgangsmarkeringen altijd bij op 10%, 25%, 50%, 75% en 95%. |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | N.v.t. | Auto track is niet meer beschikbaar. |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | N.v.t. | Auto track is niet meer beschikbaar. |

### Variabelen voor bijhouden toevoegen

| Mijlsteen | Mijlsteensyntaxis | Media Analytics | Syntaxis voor medianalyse |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | N.v.t. | Media Analytics wordt ingesteld op 10 seconden voor inhoud en 1 seconde voor advertenties. Geen andere opties beschikbaar. |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | N.v.t. | Voortgangsmarkeringen worden niet standaard weergegeven voor advertenties. Gebruik berekende metriek om markeringen voor voortgang samen te stellen. |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | N.v.t. | Media Analytics is ingesteld op 1 seconde voor advertenties. Geen andere opties beschikbaar. |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | N.v.t. | Auto track is niet meer beschikbaar. |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | N.v.t. | Auto track is niet meer beschikbaar. |

### Methoden van Media Module

| Mijlsteen | Mijlsteensyntaxis | Media Analytics | Syntaxis voor medianalyse |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | trackSessionStart | `trackSessionStart(` <br> `  mediaObject,` <br> `  contextData)` |
| mediaName | `mediaName`: (vereist) De naam van de video zoals u deze wilt weergeven in videorapporten. | name | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaLength | `mediaLength`: (vereist) De lengte van de video in seconden. | length | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaPlayerName | `mediaPlayerName`: (vereist) De naam van de mediaspeler die wordt gebruikt om de video weer te geven, zoals u deze wilt weergeven in videoverslagen. | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | trackEvent | `mediaHeartbeat.trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdBreakStart, ` <br> `  adBreakObject);` <br> `...` <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdStart, ` <br> `  adObject, ` <br> `  adCustomMetadata);` |
| name | `name`: (vereist) De naam of id van de advertentie. | name | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| length | `length`: (vereist) De lengte van de advertentie. | length | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| playerName | `playerName`: (vereist) De naam van de mediaspeler die wordt gebruikt om de advertentie weer te geven. | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| parentName | `parentName`: De naam of id van de primaire inhoud waarin de advertentie is ingesloten. | N.v.t. | Automatisch overgeërfd. |
| parentPod | `parentPod`: De positie in de primaire inhoud waarop de advertentie is afgespeeld. | position | `createAdBreakObject(` <br> `  name, ` <br> `  position, ` <br> `  startTime)` |
| parentPodPosition | `parentPodPosition`: De positie binnen de pod waar de advertentie wordt afgespeeld. | position | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| CPM | `CPM`: De CPM of de gecodeerde CPM (vooraf voorzien van een &#39;~&#39;) die op dit afspelen van toepassing is. | N.v.t. | Niet standaard beschikbaar in Media Analytics. |
| Media.click | `s.Media.click(name, offset)` | N.v.t. | Gebruik een aanroep van een aangepaste koppelingsanalyse om kliks bij te houden. |
| Media.close | `s.Media.close(mediaName)` | trackSessionEnd | `trackSessionEnd()` |
| Media.complete | `s.Media.complete(name, offset)` | trackComplete | `trackComplete()` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | trackPlay | `trackPlay()` |
| Media.stop | `s.Media.stop(mediaName, mediaOffset)` | trackPause <br> of <br> trackEvent | `trackPause()` <br> of `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  SeekStart)` <br> of <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  BufferStart);` |
| Media.monitor | `s.Media.monitor(s, media)` | Gebruik aangepaste of standaardmetagegevens om extra variabelen in te stellen. | `var customVideoMetadata = ` <br> `{` <br> `  isUserLoggedIn: ` <br> `    "false",` <br> `  tvStation: ` <br> `    "Sample TV station",` <br> `  programmer: ` <br> `    "Sample programmer"` <br> `};` <br> `...` <br> `var standardVideoMetadata ` <br> `  = {};` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   EPISODE] = ` <br> `  "Sample Episode";` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   SHOW] = "Sample Show";` <br> `...` <br> `mediaObject.setValue(` <br> `  MediaHeartbeat.` <br> `  MediaObjectKey.` <br> `  StandardVideoMetadata, ` <br> `  standardVideoMetadata);` |
| Media.track | `s.Media.track(mediaName)` | N.v.t. | De het volgen vraagfrequentie wordt automatisch geplaatst. |
