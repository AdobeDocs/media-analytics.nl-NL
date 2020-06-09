---
title: Migreren van Mijlsteen naar Media Analytics
description: null
uuid: fdc96146-af63-48ce-b938-c0ca70729277
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 5%

---


# Migreren van Mijlsteen naar Media Analytics {#migrating-from-milestone-to-media-analytics}

## Overzicht {#overview}

De kernconcepten van videometing zijn hetzelfde voor Mijlpaal en Media Analytics, die videospelergebeurtenissen neemt en deze toewijst aan analytische methoden, terwijl ook de metagegevens en waarden van de speler worden opgehaald en aan analytische variabelen worden toegewezen. De oplossing van de Analyse van Media groeide uit Mijlpaal, zo veel van de methodes en metriek zijn het zelfde, echter, is de configuratiebenadering en de code beduidend veranderd. Het zou mogelijk moeten zijn om de spelergebeurteniscode bij te werken om aan de nieuwe methodes van de Analyse van Media te richten. Zie Overzicht [en het](/help/sdk-implement/setup/setup-overview.md) Volgen Overzicht [](/help/sdk-implement/track-av-playback/track-core-overview.md) van SDK voor meer details bij het uitvoeren van de Analytics van Media.

De volgende lijsten verstrekken vertalingen tussen de oplossing van de Mijlpaal en de oplossing van de Analyse van Media.

## Migratiehandleiding {#migration-guide}

### Referentie variabele

| Mijlsteen, metrisch | Type variabele | Metrisch voor media-analyse |
| --- | --- | --- |
| Inhoud | Vervaldatum<br/><br/>eVarDefault: Bezoek | Inhoud |
| Inhoudstype | Standaardvervaldatum van eVar<br/><br/> : Paginaweergave | Inhoudstype |
| Tijd van inhoud besteed | Type gebeurtenis<br/><br/> : Teller | Tijd van inhoud besteed |
| Video wordt gestart | Type gebeurtenis<br/><br/> : Teller | Video wordt gestart |
| Video voltooid | Type gebeurtenis<br/><br/> : Teller | Inhoud voltooid |

### Variabelen van de mediamodule

<table>
<thead>
<tr>
<th>Mijlsteen
</th>
<th>Mijlsteensyntaxis
</th>
<th>Media Analytics
</th>
<th>Syntaxis voor medianalyse
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.trackUsingContextData
</td>
<td>
<pre>
s.Media.trackUsingContextData = true;
</pre>
</td>
<td>N.v.t.
</td>
<td>Alle gegevens van de Analyse van Media worden slechts verzonden gebruikend de Gegevens van de Context.
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
</td>
<td>
<pre>
s.Media.contextDataMapping = { "a.media.name":"eVar2,prop2", "a.media.segment":"eVar3", "a.contentType":"eVar1", "a.media.timePlayed":"event3", "a.media.view":"event1", "a.media.segment Weergave":"event2", "a.media.complete":"event7", "a.media.milestone": {25:"event4", 50:"event5", 75:"event6" };
</pre>
</td>
<td>N.v.t.
</td>
<td>Contextgegevens van Media Analytics worden automatisch ingevuld met geïndexeerde variabelen. Toewijzing aan eVars, props en gebeurtenissen die ik niet meer nodig heb in de implementatiecode. De klanten kunnen contextdata aan variabelen in kaart brengen gebruikend verwerkingsregels.
</td>
</tr>
<tr>
<td>
Media.trackVars
</td>
<td>
<pre>
s.Media.trackVars = "events, prop2, eVar1, eVar2, eVar3";
</pre>
</td>
<td>N.v.t.
</td>
<td>Niet meer nodig omdat de afbeelding plaatsvindt via gereserveerde variabelen en verwerkingsregels.
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s.Media.trackEvents = "event1, event2, event3, event4, event5, event6, event7"
</pre>
</td>
<td>N.v.t.
</td>
<td>Niet meer nodig omdat de afbeelding plaatsvindt via gereserveerde variabelen en verwerkingsregels.
</td>
</tr>
</tbody>
</table>

### Optionele variabelen

<table>
<thead>
<tr>
<th>Mijlsteen
</th>
<th>Mijlsteensyntaxis
</th>
<th>Media Analytics
</th>
<th>Syntaxis voor medianalyse
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.autoTrack
</td>
<td>
<pre>
s.Media.autoTrack = true;
</pre>
</td>
<td>N.v.t.
</td>
<td>We bieden geen vooraf gebouwde spelertoewijzingen meer.
</td>
</tr>
<tr>
<td>
Media.autoTrackNetStreams
</td>
<td>
<pre>
s.Media.
  autoTrackNetStreams = true
</pre>
</td>
<td>N.v.t.
</td>
<td>We bieden geen vooraf gebouwde spelertoewijzingen meer.
</td>
</tr>
<tr>
<td>
Media.completeByCloseOffset
</td>
<td>
<pre>
s.Media.
  completeByCloseOffset = true
</pre>
</td>
<td>N.v.t.
</td>
<td>Inhoud voltooid ondersteunt alleen een voortgangsmarkering van 100%.
</td>
</tr>
<tr>
<td>
Media.completeCloseOffsetThreshold
</td>
<td>
<pre>
s.Media.
  completeCloseOffsetThreshold = 1
</pre>
</td>
<td>N.v.t.
</td>
<td>Inhoud voltooid ondersteunt alleen een voortgangsmarkering van 100%.
</td>
</tr>
<tr>
<td>
Media.playerName
</td>
<td>
<pre>
s.Media.playerName = "Naam van aangepaste speler"
</pre>
</td>
<td>
SDK-sleutel: playerName; 
API-sleutel: media.playerName
</td>
<td>
<pre>
MediaHeartboneConfig.
  playerName
</pre>
</p>
</td>
</tr>
<tr>
<td>
Media.trackSeconds
</td>
<td>
<pre>
s.Media.
  trackSeconds = 15
</pre>
</td>
<td>N.v.t.
</td>
<td>Media Analytics wordt ingesteld op 10 seconden voor inhoud en 1 seconde voor advertenties. Er zijn geen andere opties beschikbaar.
</td>
</tr>
<tr>
<td>
Media.trackMilestones
</td>
<td>
<pre>
s.Media.
  trackMijlpalen = "25,50,75";
</pre>
</td>
<td>N.v.t.
</td>
<td>Media Analytics houdt voortgangsmarkeringen altijd bij op 10%, 25%, 50%, 75%, 95%
</td>
</tr>
<tr>
<td>
Media.trackOffsetMilestones
</td>
<td>
<pre>
s.Media.
  trackOffsetMilestone = "20,40,60";
</pre>
</td>
<td>N.v.t.
</td>
<td>Media Analytics houdt voortgangsmarkeringen altijd bij op 10%, 25%, 50%, 75%, 95%
</td>
</tr>
<tr>
<td>
Media.segmentByMilestones
</td>
<td>
<pre>
s.Media.segmentByMijlpalen = true;
</pre>
</td>
<td>N.v.t.
</td>
<td>Auto track is niet meer beschikbaar
</td>
</tr>
<tr>
<td>
Media.segmentByOffsetMilestones
</td>
<td>
<pre>
s.Media.
  segmentByOffsetMilestone = true;
</pre>
</td>
<td>N.v.t.
</td>
<td>Auto track is niet meer beschikbaar
</td>
</tr>
</tbody>
</table>

### Variabelen voor bijhouden toevoegen

<table>
<thead>
<tr>
<th>Mijlsteen
</th>
<th>Mijlsteensyntaxis
</th>
<th>Media Analytics
</th>
<th>Syntaxis voor medianalyse
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.adTrackSeconds
</td>
<td>
<pre>
s.Media.
  adTrackSeconds = 15
</pre>
</td>
<td>N.v.t.
</td>
<td>Media Analytics wordt ingesteld op 10 seconden voor inhoud en 1 seconde voor advertenties. Er zijn geen andere opties beschikbaar.
</td>
</tr>
<tr>
<td>
Media.adTrackMilestones
</td>
<td>
<pre>
s.Media.
  adTrackMijlpalen = "25,50,75";
</pre>
</td>
<td>N.v.t.
</td>
<td>Voortgangsmarkeringen worden niet standaard weergegeven voor advertenties. De maatstaven die worden gebruikt voor het maken en markeren van vorderingen.
</td>
</tr>
<tr>
<td>
Media.adTrackOffsetMilestones
</td>
<td>
<pre>
s.Media.
  adTrackOffsetMijlpalen = "20,40,60";
</pre>
</td>
<td>N.v.t.
</td>
<td>Media Analytics is ingesteld op 1 seconde voor advertenties. Er zijn geen andere opties beschikbaar.
</td>
</tr>
<tr>
<td>
Media.adSegmentByMilestones
</td>
<td>
<pre>
s.Media.
  adSegmentByMilestone = true;
</pre>
</td>
<td>N.v.t.
</td>
<td>Auto track is niet meer beschikbaar
</td>
</tr>
<tr>
<td>
Media.adSegmentByOffsetMilestones
</td>
<td>
<pre>
s.Media.
  adSegmentByOffsetMilestone = true;
</pre>
</td>
<td>N.v.t.
</td>
<td>Auto track is niet meer beschikbaar
</td>
</tr>
</tbody>
</table>

### Methoden van Media Module

<table>
<thead>
<tr>
<th>Mijlsteen
</th>
<th>Mijlsteensyntaxis
</th>
<th>Media Analytics
</th>
<th>Syntaxis voor medianalyse
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.open
</td>
<td>
<pre>
s.Media.open( mediaName, mediaLength, mediaPlayerName)
</pre>
</td>
<td>
<pre>
trackSessionStart
</pre>
</td>
<td>
<pre>
trackSessionStart( mediaObject, contextData)
</pre>
</td>
</tr>
<tr>
<td>
mediaName - (Vereist) de naam van de video aangezien u het in videorapporten wilt verschijnen.
</td>
<td>
<pre>
mediaName
</pre>
</td>
<td>
<pre>
name
</pre>
</td>
<td>
<pre>
createMediaObject( naam, mediaId, lengte, streamType)
</pre>
</td>
</tr>
<tr>
<td>
mediaLength - (Vereist) de lengte van de video in seconden.
</td>
<td>
<pre>
mediaLength
</pre>
</td>
<td>
<pre>
length
</pre>
</td>
<td>
<pre>
createMediaObject( naam, mediaId, lengte, streamType)
</pre>
</td>
</tr>
<tr>
<td>
mediaPlayerName - (Vereist) De naam van de mediaspeler die wordt gebruikt om de video weer te geven, zoals u deze wilt weergeven in videoverslagen.
</td>
<td>
<pre>
mediaPlayerName
</pre>
</td>
<td>
<pre>
playerName
</pre>
</td>
<td>
<pre>
MediaHeartboneConfig.
  playerName
</pre>
</td>
</tr>
<tr>
<td>
Media.openAd
</td>
<td>
<pre>
s.Media.openAd( naam, lengte, spelernaam, bovenliggendeNaam, bovenliggendePod, bovenliggendePodPosition, CPM)
</pre>
</td>
<td>
<pre>
trackEvent
</pre>
</td>
<td>
<pre>
mediaHeartbone.trackEvent( MediaHeartbone.
    Gebeurtenis.
    AdBreakStart, adBreakObject);
...
trackEvent( MediaHeartbone.
    Gebeurtenis.
    AdStart, addObject, adCustomMetadata);
</pre>
</td>
</tr>
<tr>
<td>
name - (Required) De naam of identiteitskaart van de advertentie.
</td>
<td>
<pre>
name
</pre>
</td>
<td>
<pre>
name
</pre>
</td>
<td>
<pre>
createAdObject( naam, adId, positie, lengte)
</pre>
</td>
</tr>
<tr>
<td>
length(Vereist) De lengte van de advertentie.
</td>
<td>
<pre>
length
</pre>
</td>
<td>
<pre>
length
</pre>
</td>
<td>
<pre>
createAdObject( naam, adId, positie, lengte)
</pre>
</td>
</tr>
<tr>
<td>
playerName - (Vereist) De naam van de mediaplayer die wordt gebruikt om de advertentie weer te geven.
</td>
<td>
<pre>
playerName
</pre>
</td>
<td>
<pre>
playerName
</pre>
</td>
<td>
<pre>
MediaHeartboneConfig.
  playerName
</pre>
</td>
</tr>
<tr>
<td>
parentName - De naam of id van de primaire inhoud waarin de advertentie is ingesloten.
</td>
<td>
<pre>
parentName
</pre>
</td>
<td>N.v.t.
</td>
<td>Automatisch overgeërfd
</td>
</tr>
<tr>
<td>
parentPod - De positie in de primaire inhoud die de advertentie is afgespeeld.
</td>
<td>
<pre>
parentPod
</pre>
</td>
<td>
<pre>
positie
</pre>
</td>
<td>
<pre>
createAdBreakObject( naam, positie, begintijd)
</pre>
</td>
</tr>
<tr>
<td>
parentPodPosition - De positie binnen de pod waar de advertentie wordt afgespeeld.
</td>
<td>
<pre>
parentPodPosition
</pre>
</td>
<td>
<pre>
positie
</pre>
</td>
<td>
<pre>
createAdObject( naam, adId, positie, lengte)
</pre>
</td>
</tr>
<tr>
<td>
CPMTthe CPM of encrypted CPM (gefixeerd met "~") die op deze playback van toepassing is.
</td>
<td>
<pre>
CPM
</pre>
</td>
<td>N.v.t.
</td>
<td>Niet standaard beschikbaar in Media Analytics
</td>
</tr>
<tr>
<td>
Media.click
</td>
<td>
<pre>
s.Media.click( naam, verschuiving)
</pre>
</td>
<td>N.v.t.
</td>
<td>Een aanroep van aangepaste koppelingsanalyses gebruiken om klikbewerkingen bij te houden
</td>
</tr>
<tr>
<td>
Media.close
</td>
<td>
<pre>
s.Media.close( mediaName)
</pre>
</td>
<td>
<pre>
trackSessionEnd
</pre>
</td>
<td>
<pre>
trackSessionEnd()
</pre>
</td>
</tr>
<tr>
<td>
Media.complete
</td>
<td>
<pre>
s.Media.complete( naam, verschuiving)
</pre>
</td>
<td>
<pre>
trackComplete
</pre>
</td>
<td>
<pre>
trackComplete()
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.play
</pre>
</td>
<td>
<pre>
s.Media.play( naam, offset, segmentNum, segment, segmentlengte)
</pre>
</td>
<td>
<pre>
trackPlay
</pre>
</td>
<td>
<pre>
trackPlay()
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.stop
</pre>
</td>
<td>
<pre>
s.Media.stop( mediaName, mediaOffset)
</pre>
</td>
<td>
<pre>
trackPause
</pre> of 
<pre>
trackEvent
</pre>
</td>
<td>
<pre>
trackPause()
</pre> 
of
<pre>
trackEvent( MediaHeartbone.
  Gebeurtenis.
  SeekStart)
</pre> of
<pre>
trackEvent( MediaHeartbone.
  Gebeurtenis.
  BufferStart);
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.monitor
</pre>
</td>
<td>
<pre>
s.Media.monitor(s, media)
</pre>
</td>
<td>Aangepaste of standaardmetagegevens gebruiken om extra variabelen in te stellen
</td>
<td>
<pre>
var customVideoMetadata = { isUserLoggedIn: 
    "false", tvStation: 
    "Voorbeeld-tv-station", programmeur: 
    "Sample programer"};
...
var standardVideoMetadata = {};
standardVideoMetadata [MediaHeartbone.
   VideoMetadataKeys.
   EPISODE] = "Bemonsteringsepisode";
standardVideoMetadata [MediaHeartbone.
   VideoMetadataKeys.
   SHOW] = "Sample Show";
...
mediaObject.setValue( MediaHeartbeat).
  MediaObjectKey.
  StandardVideoMetadata, standardVideoMetadata);
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.track
</pre>
</td>
<td>
<pre>
s.Media.track( mediaName)
</pre>
</td>
<td>N.v.t.
</td>
<td>De het volgen vraagfrequentie wordt automatisch geplaatst.
</td>
</tr>
</tbody>
</table>

