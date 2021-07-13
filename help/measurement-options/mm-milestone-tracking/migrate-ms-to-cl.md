---
title: Meer informatie over migreren van Mijlsteen naar aangepaste koppeling
description: Leer hoe te om de variabelen van Milestone in de modulemethodes van de Verbinding van de Douane en van de Mijl in de syntaxis van de Verbinding van de Douane te veranderen.
uuid: 1c8edde5-0ef1-4bc0-a62d-1747f4907f09
exl-id: 732079f4-3eb8-4b9a-892b-25a1c9332be4
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 15%

---

# Migreren van Milestone naar Custom Link{#migrating-from-milestone-to-custom-link}

## Overzicht {#overview}

De kernconcepten van videometing zijn hetzelfde voor bijhouden van mijlpaal en aangepaste koppeling. Deze houdt gebeurtenissen van videospelers in en wijst deze toe aan analysemethoden, terwijl de metagegevens en waarden van de speler ook worden opgehaald en aan analytische variabelen worden toegewezen. De benadering van de Verbinding van de Douane zou als afslanking en vereenvoudiging van zowel de implementatie als de verzamelde gegevens moeten worden beschouwd. Met de oplossing van de Verbinding van de Douane, zijn geen variabelen of methodes vooraf bepaald voor videometing, vereist het een volledige douaneopstelling. Het zou mogelijk moeten zijn om de spelergebeurteniscode bij te werken zodat deze naar de aangepaste link tracking-aanroepen voor basisspelergebeurtenissen zoals start en complete verwijst. Zie [Custom Link Implementation guide](/help/measurement-options/cl-in-aa/cl-impl-guide.md) voor meer informatie.

De volgende lijsten verstrekken vertalingen tussen de oplossing van Milestone en de oplossing van de Verbinding van de Douane.

## Migratiehandleiding {#migration-guide}

### Referentie videovariabele

| Mijlsteen, metrisch | Type variabele | Aangepaste koppeling |
| --- | --- | --- |
| Inhoud | eVar <br> Standaardvervaldatum: Bezoek | Definieer uw eigen eVar. |
| Inhoudstype | eVar <br> Standaardvervaldatum: Paginaweergave | Definieer uw eigen eVar. |
| Tijd van inhoud besteed | Type gebeurtenis <br>: Teller | Definieer uw eigen gebeurtenis. |
| Video wordt gestart | Type gebeurtenis <br>: Teller | Definieer uw eigen gebeurtenis. |
| Video voltooid | Type gebeurtenis <br>: Teller | Definieer uw eigen gebeurtenis. |

### Variabelen van de mediamodule

| Mijlsteen | Mijlsteensyntaxis | Aangepaste koppeling | Syntaxis aangepaste koppeling |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | linkTrackVars | `s.linkTrackVars` <br> `  = 'events,` <br> `  contextData.video.name’;` <br> `  s.contextData["video.name"]` <br> `  = mediaName;` |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | N.v.t. | Contextgegevens toewijzen aan variabelen, profielen en gebeurtenissen is nu voltooid met verwerkingsregels. |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | linkTrackVars | `s.linkTrackVars` <br> `  = 'events,` <br> `    prop10,` <br> `    eVar10,` <br> `    eVar12,` <br> `    eVar13,` <br> `    eVar15,` <br> `    contextData.` <br> `       video.name,` <br> `     contextData.` <br> `       video.view';` <br> |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | linkTrackEvents | `s.linkTrackEvents` <br> `  = 'event2';` |

### Optionele variabelen

| Mijlsteen | Mijlsteensyntaxis | Aangepaste koppeling | Syntaxis aangepaste koppeling |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | N.v.t. | Niet beschikbaar. |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | N.v.t. | Niet beschikbaar. |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | N.v.t. | Niet beschikbaar. |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | N.v.t. | Niet beschikbaar. |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | Stel de eVar- of contextgegevensvariabele in de koppelingsaanroep in. | `s.contextData['video.player']` <br> `  = ”CustomPlayer Name”;` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | N.v.t. | Niet beschikbaar. |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | N.v.t. | Niet beschikbaar. |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | N.v.t. | Niet beschikbaar. |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | N.v.t. | Niet beschikbaar. |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | N.v.t. | Niet beschikbaar. |

### Variabelen voor bijhouden toevoegen

| Mijlsteen | Mijlsteensyntaxis | Aangepaste koppeling | Syntaxis aangepaste koppeling |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | N.v.t. | Niet beschikbaar. |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | N.v.t. | Niet beschikbaar. |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | N.v.t. | Niet beschikbaar. |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | N.v.t. | Niet beschikbaar. |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | N.v.t. | Niet beschikbaar. |

### Methoden van Media Module

| Mijlsteen | Mijlsteensyntaxis | Aangepaste koppeling | Syntaxis aangepaste koppeling |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | `s.tl()` | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.video.name,` <br> `     contextData.video.view';` <br> `s.linkTrackEvents ` <br> `  = 'event2';` <br> `s.prop10` <br> `   = mediaName;` <br> `s.eVar10` <br> `  = mediaName;` <br> `s.eVar12` <br> `  = "video";` <br> `s.eVar15` <br> `  = mediaPlayerName;` <br> `s.events` <br> `  = 'event2';` <br> `s.contextData['video.name']` <br> `  = mediaName;` <br> `s.contextData['video.view']` <br> `  = 'true';` <br> `s.tl(this,'o','Video Start');` |
| mediaName | `mediaName`: (Vereist) De naam van de video zoals u deze wilt weergeven in videoverslagen. | Stel de eVar- of contextgegevensvariabele in de koppelingsaanroep in. | `s.prop10 = mediaName;` <br> `s.eVar10 = mediaName;` <br> `s.contextData['video.name']` <br> `  = mediaName;` |
| mediaLength | `mediaLength`: (Vereist) De lengte van de video in seconden. | Stel de eVar- of contextgegevensvariabele in de koppelingsaanroep in. | `s.contextData['video.length']` <br> `  = ”90”;` |
| mediaPlayerName | `mediaPlayerName`: (Vereist) De naam van de mediaspeler die wordt gebruikt om de video weer te geven, zoals u deze wilt weergeven in videoverslagen. | Stel de eVar- of contextgegevensvariabele in de koppelingsaanroep in. | `s.contextData['video.player']` <br> `  = ”CustomPlayer Name”;` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | N.v.t. | Niet beschikbaar. |
| name | `name`: (Vereist) De naam of id van de advertentie. | N.v.t. | Niet beschikbaar. |
| length | `length`: (vereist) De lengte van de advertentie. | N.v.t. | Niet beschikbaar. |
| playerName | `playerName`: (Vereist) De naam van de mediaspeler die wordt gebruikt om de advertentie weer te geven. | N.v.t. | Niet beschikbaar. |
| parentName | `parentName`: De naam of id van de primaire inhoud waarin de advertentie is ingesloten. | N.v.t. | Niet beschikbaar. |
| parentPod | `parentPod`: De positie in de primaire inhoud waarop de advertentie is afgespeeld. | N.v.t. | Niet beschikbaar. |
| parentPodPosition | `parentPodPosition`: De positie in de pod waar de advertentie wordt afgespeeld. | N.v.t. | Niet beschikbaar. |
| CPM | `CPM`: CPM of gecodeerde CPM (vooraf bevestigd met &quot;~&quot;) die op deze playback van toepassing is. | N.v.t. | Niet beschikbaar. |
| Media.click | `s.Media.click(name, offset)` | `s.tl()` | Gebruik een aanroep van een aangepaste koppelingsanalyse om kliks bij te houden. |
| Media.close | `s.Media.close(mediaName)` | N.v.t. | Niet beschikbaar. |
| Media.complete | `s.Media.complete(` <br> `  name,` <br> `  offset)` | `s.tl()` | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.video.name,` <br> `     contextData.video.complete';` <br> `s.linkTrackEvents ` <br> `  = 'event3';` <br> `s.prop10` <br> `   = mediaName;` <br> `s.eVar10` <br> `  = mediaName;` <br> `s.eVar12` <br> `  = "video";` <br> `s.eVar15` <br> `  = mediaPlayerName;` <br> `s.events` <br> `  = 'event3';` <br> `s.contextData['video.name']` <br> `  = mediaName;` <br> `s.contextData['video.complete']` <br> `  = 'true';` <br> `s.tl(this,'o','Video Complete');` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | N.v.t. | Niet beschikbaar. |
| Media.stop | `s.Media.stop(` <br> `  mediaName,` <br> `  mediaOffset)` | N.v.t. | Niet beschikbaar. |
| Media.monitor | `s.Media.monitor(s, media)` | Stel de eVar- of contextgegevensvariabele in de koppelingsaanroep in. | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.` <br> `       video.name,` <br> `     contextData.` <br> `       video.view';` <br> `s.linkTrackEvents = 'event2';` |
| Media.track | `s.Media.track(` <br> `  mediaName)` | N.v.t. | Niet beschikbaar. |
