---
title: Migreren van Milestone naar Custom Link
description: null
uuid: 1c8edde5-0ef1-4bc0-a62d-1747f4907f09
translation-type: tm+mt
source-git-commit: ccdc3e170d125a76d798be7ce1fa5c12eef1f76a

---


# Migreren van Milestone naar Custom Link{#migrating-from-milestone-to-custom-link}

## Overzicht {#overview}

De kernconcepten van videometing zijn hetzelfde voor bijhouden van mijlpaal en aangepaste koppeling. Deze houdt gebeurtenissen van videospelers in en wijst deze toe aan analysemethoden, terwijl de metagegevens en waarden van de speler ook worden opgehaald en aan analytische variabelen worden toegewezen. De benadering van de Verbinding van de Douane zou als afslanking en vereenvoudiging van zowel de implementatie als de verzamelde gegevens moeten worden beschouwd. Met de oplossing van de Verbinding van de Douane, zijn geen variabelen of methodes vooraf bepaald voor videometing, vereist het een volledige douaneopstelling. Het zou mogelijk moeten zijn om de spelergebeurteniscode bij te werken zodat deze naar de aangepaste link tracking-aanroepen voor basisspelergebeurtenissen zoals start en complete verwijst. Zie [de implementatiegids](/help/measurement-options/cl-in-aa/cl-impl-guide.md) van de Verbinding van de Douane en [Handmatige het Volgen van de Verbinding Gebruikend de Code](https://docs.adobe.com/content/help/en/media-analytics/using/measurement-options/cl-in-aa/cl-impl-guide.html) van de Verbinding van de Douane voor meer details.

De volgende lijsten verstrekken vertalingen tussen de oplossing van Milestone en de oplossing van de Verbinding van de Douane.

## Migratiehandleiding {#migration-guide}

### Referentie videovariabele

<table>
<thead>
<tr>
<th><strong>Mijlsteen, metrisch</strong></th>
<th><strong>Type variabele</strong></th>
<th><strong>Aangepaste koppeling</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>Inhoud</td>
<td>
<p>eVar</p>
<p>Standaardvervaldatum: Bezoek</p>
</td>
<td>Uw eigen eVar definiëren</td>
</tr>
<tr>
<td>Inhoudstype</td>
<td>
<p>eVar</p>
<p>Standaardvervaldatum: Paginaweergave</p>
</td>
<td>Uw eigen eVar definiëren</td>
</tr>
<tr>
<td>Tijd van inhoud besteed</td>
<td>
<p>Gebeurtenis</p>
<p>Type: Teller</p>
</td>
<td>Uw eigen gebeurtenis definiëren</td>
</tr>
<tr>
<td>Video wordt gestart</td>
<td>
<p>Gebeurtenis</p>
<p>Type: Teller</p>
</td>
<td>Uw eigen gebeurtenis definiëren</td>
</tr>
<tr>
<td>Video voltooid</td>
<td>
<p>Gebeurtenis</p>
<p>Type: Teller</p>
</td>
<td>Uw eigen gebeurtenis definiëren</td>
</tr>
</tbody>
</table>

### Variabelen van de mediamodule

<table>
<thead>
<tr>
<th>Mijlsteen
</th>
<th>Mijlsteensyntaxis
</th>
<th>Aangepaste koppeling
</th>
<th>Syntaxis aangepaste koppeling
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
s.Media.
  trackUsingContextData = true;
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars = 'events, contextData.video.name'; 
s.contextData["video.name"] = mediaName;
</pre>
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
</td>
<td>
<pre>
s.Media.
  contextDataMapping = { "a.media.name":
    "eVar2,prop2", "a.media.segment":
    "eVar3", "a.contentType":
    "eVar1", "a.media.timePlayed":
    "event3", "a.media.view":
    "event1", "a.media.segmentView":
    "event2", "a.media.complete":
    "event7", "a.media.milestone":{ 25:"event4", 50:"event5", 75:"event6" };
</pre>
</td>
<td>N.v.t.
</td>
<td>Het toewijzen van contextgegevens aan variabelen, profielen en gebeurtenissen wordt nu voltooid door verwerkingsregels.
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
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15, contextData.
       video.name, contextData.
       video.view';
</pre>
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
<td>
linkTrackEvents
</td>
<td>
<pre>
s.linkTrackEvents = 'event2';
</pre>
</td>
</tr>
</tbody>
</table>

<table>
<thead>
<tr>
<th>Mijlsteen
</th>
<th>Mijlsteensyntaxis
</th>
<th>Aangepaste koppeling
</th>
<th>Syntaxis aangepaste koppeling
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
s.Media.
  trackUsingContextData = true;
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars = 'events, contextData.video.name'; 
s.contextData["video.name"] = mediaName;
</pre>
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
</td>
<td>
<pre>
s.Media.contextDataMapping = { "a.media.name":"eVar2,prop2", "a.media.segment":"eVar3", "a.contentType":"eVar1", "a.media.timePlayed":"event3", "a.media.view":"event1", "a.media.segment View":"event2", "a.media.complete":"event7", "a.media.milestone":{ 25:"event4", 50:"event5", 75:"event6" };
</pre>
</td>
<td>N.v.t.
</td>
<td>Het toewijzen van contextgegevens aan variabelen, profielen en gebeurtenissen wordt nu voltooid door verwerkingsregels.
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
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15, contextData.
       video.name, contextData.
       video.view';
</pre>
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
<td>
linkTrackEvents
</td>
<td>
<pre>
s.linkTrackEvents = 'event2';
</pre>
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
<th>Aangepaste koppeling
</th>
<th>Syntaxis aangepaste koppeling
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
<td>Niet beschikbaar
</td>
</tr>
<tr>
<td>
Media.autoTrackNetStreams
</td>
<td>
<pre>
s.Media.autoTrackNetStreams = true
</pre>
</td>
<td>N.v.t.
</td>
<td>Niet beschikbaar
</td>
</tr>
<tr>
<td>
Media.completeByCloseOffset
</td>
<td>
<pre>
s.Media.completeByCloseOffset = true
</pre>
</td>
<td>N.v.t.
</td>
<td>Niet beschikbaar
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
<td>Niet beschikbaar
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
Variabele voor eVar- of contextgegevens instellen in koppelingsaanroep
</td>
<td>
<pre>
s.contextData['video.player'] ="Naam CustomPlayer";
</pre>
</td>
</tr>
<tr>
<td>
Media.trackSeconds
</td>
<td>
<pre>
s.Media.trackSeconds = 15
</pre>
</td>
<td>N.v.t.
</td>
<td>Niet beschikbaar
</td>
</tr>
<tr>
<td>
Media.trackMilestones
</td>
<td>
<pre>
s.Media.trackMijlpalen = "25,50,75";
</pre>
</td>
<td>N.v.t.
</td>
<td>Niet beschikbaar
</td>
</tr>
<tr>
<td>
Media.trackOffsetMilestones
</td>
<td>
<pre>
s.Media.trackOffsetMijlpalen = "20,40,60";
</pre>
</td>
<td>N.v.t.
</td>
<td>Niet beschikbaar
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
<td>Niet beschikbaar
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
<td>Niet beschikbaar
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
<th>Aangepaste koppeling
</th>
<th>Syntaxis aangepaste koppeling
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
s.Media.adTrackSeconds = 15 
</pre>
</td>
<td>N.v.t.
</td>
<td>Niet beschikbaar
</td>
</tr>
<tr>
<td>
Media.adTrackMilestones
</td>
<td>
<pre>
s.Media.adTrackMijlpalen = "25,50,75";
</pre>
</td>
<td>N.v.t.
</td>
<td>Niet beschikbaar
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
<td>Niet beschikbaar
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
<td>Niet beschikbaar
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
<td>Niet beschikbaar
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
<th>Aangepaste koppeling
</th>
<th>Syntaxis aangepaste koppeling
</th>
</tr>
</thead>
<tbody>
<tr>
<td>Media.open</td>
<td>
<pre>
s.Media.open( mediaName, mediaLength, mediaPlayerName)
</pre>
</td>
<td>s.tl()</td>
<td>
<pre>
s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar15, contextData.video.name, contextData.video.view';
s.linkTrackEvents = 'event2';
s.prop10 = mediaName;
s.eVar10 = mediaName;
s.eVar12 = "video";
s.eVar15 = mediaPlayerName;
s.events = 'event2';
s.contextData['video.name'] = mediaName;
s.contextData['video.view'] = 'true';
s.tl(this,'o','Video Start');
</pre>
</td>
</tr>
<tr>
<td>mediaName</td>
<td><b>mediaName:</b> (Vereist) De naam van de video zoals u deze wilt weergeven in videoverslagen.</td>
<td>Variabele voor eVar- of contextgegevens instellen in koppelingsaanroep</td>
<td>
<pre>
s.prop10 = mediaName;
s.eVar10 = mediaName;
s.contextData['video.name'] = mediaName;
</pre>
</td>
</tr>
<tr>
<td>
mediaLength
</td>
<td>
<b>mediaLength:</b> (Vereist) De lengte van de video in seconden.
</td>
<td>
Variabele voor eVar- of contextgegevens instellen in koppelingsaanroep
</td>
<td>
<pre>
s.contextData['video.length'] ="90";
</pre>
</td>
</tr>
<tr>
<td>
mediaPlayerName
</td>
<td>
<b>mediaPlayerName:</b> (Vereist) De naam van de mediaspeler die wordt gebruikt om de video weer te geven, zoals u deze wilt weergeven in videoreporten.
</td>
<td>
Variabele voor eVar- of contextgegevens instellen in koppelingsaanroep
</td>
<td>
<pre>
s.contextData['video.player'] ="Naam CustomPlayer";
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
<td>N.v.t.
</td>
<td>Niet beschikbaar</td>
</tr>
<tr>
<td>name</td>
<td><b>naam:</b> (Vereist) De naam of id van de advertentie.</td>
<td>N.v.t.</td>
<td>Niet beschikbaar</td>
</tr>
<tr>
<td>
length
</td>
<td>
<b>lengte:</b> (vereist) De lengte van de advertentie.
</td>
<td>N.v.t.
</td>
<td>Niet beschikbaar
</td>
</tr>
<tr>
<td>
playerName
</td>
<td>
<b>playerName:</b> (Vereist) De naam van de mediaspeler die wordt gebruikt om de advertentie weer te geven.
</td>
<td>N.v.t.
</td>
<td>Niet beschikbaar
</td>
</tr>
<tr>
<td>
parentName
</td>
<td>
<b>parentName:</b> De naam of id van de primaire inhoud waarin de advertentie is ingesloten.
</td>
<td>N.v.t.
</td>
<td>Niet beschikbaar
</td>
</tr>
<tr>
<td>
parentPod
</td>
<td>
<b>parentPod:</b> De positie in de primaire inhoud waarop de advertentie is afgespeeld.
</td>
<td>N.v.t.
</td>
<td>Niet beschikbaar
</td>
</tr>
<tr>
<td>
parentPodPosition
</td>
<td>
<b>parentPodPosition:</b> De positie in de pod waar de advertentie wordt afgespeeld.
</td>
<td>N.v.t.
</td>
<td>Niet beschikbaar
</td>
</tr>
<tr>
<td>
CPM
</td>
<td>
<b>CPM:</b> CPM of gecodeerde CPM (vooraf bevestigd met "~") die op deze playback van toepassing is.
</td>
<td>N.v.t.
</td>
<td>Niet beschikbaar
</td>
</tr>
<tr>
<td>
Media.click
</td>
<td>
<pre>
s.Media.click(naam, verschuiving)
</pre>
</td>
<td>
<pre>
s.tl()
</pre>
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
s.Media.close(mediaName)
</pre>
</td>
<td>N.v.t.
</td>
<td>Niet beschikbaar
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
s.tl()
</td>
<td>
<pre>
s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar15, contextData.
       video.name, contextData.
       video.complete";
s.linkTrackEvents = 'event3';
s.prop10 = mediaName;
s.eVar10 = mediaName;
s.eVar12 = "video";
s.eVar15 = mediaPlayerName;
s.events = 'event3';
s.contextData['video.name'] = mediaName;
s.contextData['video.complete'] = 'true';
s.tl(this,'o','Video Complete');
</pre>
</td>
</tr>
<tr>
<td>
Media.play
</td>
<td>
<pre>
s.Media.play( naam, offset, segmentNum, segment, segmentlengte)
</pre>
</td>
<td>N.v.t.
</td>
<td>Niet beschikbaar
</td>
</tr>
<tr>
<td>
Media.stop
</td>
<td>
<pre>
s.Media.stop( mediaName, mediaOffset)
</pre>
</td>
<td>N.v.t. 
</td>
<td>Niet beschikbaar
</td>
</tr>
<tr>
<td>
Media.monitor
</td>
<td>
<pre>
s.Media.monitor(s, media)
</pre>
</td>
<td>
Variabele voor eVar- of contextgegevens instellen in koppelingsaanroep
</td>
<td>
<pre>
s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar15, contextData.
       video.name, contextData.
       video.view';
s.linkTrackEvents = 'event2';
</pre>
</td>
</tr>
<tr>
<td>
Media.track
</td>
<td>
<pre>
s.Media.track(mediaName)
</pre>
</td>
<td>N.v.t.
</td>
<td>Niet beschikbaar
</td>
</tr>
</tbody>
</table>

