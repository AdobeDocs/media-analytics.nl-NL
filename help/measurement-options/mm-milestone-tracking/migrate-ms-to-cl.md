---
title: Migreren van Milestone naar Custom Link
description: null
uuid: 1c8edde5-0ef1-4bc0-a62d-1747f4907f09
translation-type: tm+mt
source-git-commit: e25c4d0add969ad31393f2eeb33b1a12b7205586
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 17%

---


# Migreren van Milestone naar Custom Link{#migrating-from-milestone-to-custom-link}

## Overzicht {#overview}

De kernconcepten van videometing zijn het zelfde voor het volgen van de Verbinding van Milestone en van de Douane, die videospelergebeurtenissen neemt en hen in kaart brengt aan analysemethodes, terwijl ook het graven van spelermeta-gegevens en waarden en hen in kaart brengen aan analysevariabelen. De benadering van de Verbinding van de Douane zou als het slanken en het vereenvoudigen van zowel de implementatie als de verzamelde gegevens moeten worden beschouwd. Met de oplossing van de Verbinding van de Douane, zijn geen variabelen of de methodes vooraf bepaald voor videometing, vereist het een volledige douaneset. Het zou mogelijk moeten zijn om de code van de spelergebeurtenis bij te werken om aan de douaneverbinding te richten die vraag naar basisspelergebeurtenissen zoals begin en volledig volgt. Zie [Implementatiegids voor aangepaste koppeling](/help/measurement-options/cl-in-aa/cl-impl-guide.md) voor meer informatie .

De volgende lijsten verstrekken vertalingen tussen de oplossing van de Mijlpaal en de oplossing van de Verbinding van de Douane.

## Migratiehandleiding {#migration-guide}

### Verwijzing naar videovariabele

| Milestone Metric | Type variabele | Aangepaste koppeling |
| --- | --- | --- |
| Inhoud | eVar <br> Standaardvervaldatum: Bezoek | Bepaal je eigen eVar. |
| Inhoudstype | eVar <br> Standaardvervaldatum: Pagina-weergave | Bepaal je eigen eVar. |
| Inhoud Tijd besteed | Gebeurtenis <br> Type: Teller | Bepaal uw eigen gebeurtenis. |
| Video start | Gebeurtenis <br> Type: Teller | Bepaal uw eigen gebeurtenis. |
| Video voltooid | Gebeurtenis <br> Type: Teller | Bepaal uw eigen gebeurtenis. |

### Variabelen mediamodule

| Mijlsteen | Milestone Syntax | Aangepaste koppeling | Custom Link Syntax |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | linkTrackVars | `s.linkTrackVars` <br> `  = 'events,` <br> `  contextData.video.name’;` <br> `  s.contextData["video.name"]` <br> `  = mediaName;` |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | N.v.t. | De de contextgegevens van de afbeelding aan Vars, steunen, en gebeurtenissen worden nu voltooid door verwerkingsregels. |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | linkTrackVars | `s.linkTrackVars` <br> `  = 'events,` <br> `    prop10,` <br> `    eVar10,` <br> `    eVar12,` <br> `    eVar13,` <br> `    eVar15,` <br> `    contextData.` <br> `       video.name,` <br> `     contextData.` <br> `       video.view';` <br> |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | linkTrackEvents | `s.linkTrackEvents` <br> `  = 'event2';` |

### Facultatieve variabelen

| Mijlsteen | Milestone Syntax | Aangepaste koppeling | Custom Link Syntax |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | N.v.t. | Niet beschikbaar. |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | N.v.t. | Niet beschikbaar. |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | N.v.t. | Niet beschikbaar. |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | N.v.t. | Niet beschikbaar. |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | De vastgestelde variabele van eVar of van de contextgegevens in verbindingsvraag. | `s.contextData['video.player']` <br> `  = ”CustomPlayer Name”;` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | N.v.t. | Niet beschikbaar. |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | N.v.t. | Niet beschikbaar. |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | N.v.t. | Niet beschikbaar. |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | N.v.t. | Niet beschikbaar. |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | N.v.t. | Niet beschikbaar. |

### Volgvariabelen voor advertentie

| Mijlsteen | Milestone Syntax | Aangepaste koppeling | Custom Link Syntax |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | N.v.t. | Niet beschikbaar. |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | N.v.t. | Niet beschikbaar. |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | N.v.t. | Niet beschikbaar. |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | N.v.t. | Niet beschikbaar. |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | N.v.t. | Niet beschikbaar. |

### Methoden voor mediamodule

| Mijlsteen | Milestone Syntax | Aangepaste koppeling | Custom Link Syntax |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | `s.tl()` | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.video.name,` <br> `     contextData.video.view';` <br> `s.linkTrackEvents ` <br> `  = 'event2';` <br> `s.prop10` <br> `   = mediaName;` <br> `s.eVar10` <br> `  = mediaName;` <br> `s.eVar12` <br> `  = "video";` <br> `s.eVar15` <br> `  = mediaPlayerName;` <br> `s.events` <br> `  = 'event2';` <br> `s.contextData['video.name']` <br> `  = mediaName;` <br> `s.contextData['video.view']` <br> `  = 'true';` <br> `s.tl(this,'o','Video Start');` |
| mediaName | `mediaName`: (vereist) de naam van de video aangezien u het in videorapporten wilt verschijnen. | De vastgestelde variabele van eVar of van de contextgegevens in verbindingsvraag. | `s.prop10 = mediaName;` <br> `s.eVar10 = mediaName;` <br> `s.contextData['video.name']` <br> `  = mediaName;` |
| mediaLength | `mediaLength`: (vereist) de lengte van de video in seconden. | De vastgestelde variabele van eVar of van de contextgegevens in verbindingsvraag. | `s.contextData['video.length']` <br> `  = ”90”;` |
| mediaPlayerName | `mediaPlayerName`: (vereist) de naam van de media speler die wordt gebruikt om de video te bekijken, aangezien u het in videorapporten wilt verschijnen. | De vastgestelde variabele van eVar of van de contextgegevens in verbindingsvraag. | `s.contextData['video.player']` <br> `  = ”CustomPlayer Name”;` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | N.v.t. | Niet beschikbaar. |
| name | `name`: (vereist) de naam of het identificatienummer van de advertentie. | N.v.t. | Niet beschikbaar. |
| length | `length`: (vereist) De lengte van de advertentie. | N.v.t. | Niet beschikbaar. |
| playerName | `playerName`: (vereist) de naam van de media speler die wordt gebruikt om de advertentie te bekijken. | N.v.t. | Niet beschikbaar. |
| parentName | `parentName`: De naam of identiteitskaart van de primaire inhoud waar de advertentie wordt ingebed. | N.v.t. | Niet beschikbaar. |
| parentPod | `parentPod`: De positie in de primaire inhoud de advertentie werd gespeeld. | N.v.t. | Niet beschikbaar. |
| parentPodPosition | `parentPodPosition`: De positie in de peul waar de advertentie wordt gespeeld. | N.v.t. | Niet beschikbaar. |
| CPM | `CPM`: CPM of gecodeerde CPM (vooraf bepaald met &quot;~&quot;) die op deze playback van toepassing is. | N.v.t. | Niet beschikbaar. |
| Media.click | `s.Media.click(name, offset)` | `s.tl()` | Gebruik een vraag van de de verbindingsanalyse van de douane om kliks te volgen. |
| Media.close | `s.Media.close(mediaName)` | N.v.t. | Niet beschikbaar. |
| Media.complete | `s.Media.complete(` <br> `  name,` <br> `  offset)` | `s.tl()` | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.video.name,` <br> `     contextData.video.complete';` <br> `s.linkTrackEvents ` <br> `  = 'event3';` <br> `s.prop10` <br> `   = mediaName;` <br> `s.eVar10` <br> `  = mediaName;` <br> `s.eVar12` <br> `  = "video";` <br> `s.eVar15` <br> `  = mediaPlayerName;` <br> `s.events` <br> `  = 'event3';` <br> `s.contextData['video.name']` <br> `  = mediaName;` <br> `s.contextData['video.complete']` <br> `  = 'true';` <br> `s.tl(this,'o','Video Complete');` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | N.v.t. | Niet beschikbaar. |
| Media.stop | `s.Media.stop(` <br> `  mediaName,` <br> `  mediaOffset)` | N.v.t. | Niet beschikbaar. |
| Media.monitor | `s.Media.monitor(s, media)` | De vastgestelde variabele van eVar of van de contextgegevens in verbindingsvraag. | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.` <br> `       video.name,` <br> `     contextData.` <br> `       video.view';` <br> `s.linkTrackEvents = 'event2';` |
| Media.track | `s.Media.track(` <br> `  mediaName)` | N.v.t. | Niet beschikbaar. |
