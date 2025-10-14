---
title: Soorten publiek migreren naar het nieuwe Adobe Analytics-gegevenstype voor streaming media
description: Leer hoe u het publiek kunt migreren naar het nieuwe gegevenstype Adobe Analytics voor streaming media
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 3056a384535b3f5f2a9bc2d950bd5ee3410ec0a5
workflow-type: tm+mt
source-wordcount: '1346'
ht-degree: 0%

---

# Media Analytics-parameters voor Adobe Experience Platform en Customer Journey Analytics

Dit document bevat een uitgebreide lijst met alle parameters voor Media Analytics die in Adobe Experience Platform en Customer Journey Analytics worden gebruikt. Het is bedoeld om de integratie van gegevens te steunen die van Adobe Analytics aan Platform via de [&#x200B; Schakelaar van Source van Analytics &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-platform/sources/connectors/adobe-applications/analytics) of de [&#x200B; Verbinding van Source van Analytics voor Classificaties &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-platform/sources/connectors/adobe-applications/classifications) worden ingevoerd, in kaart brengend elke parameter aan zijn overeenkomstige XDM gebiedspad.

## Voor Media Analytics gereserveerde variabelen

Voor alle variabelen die voor Media Analytics zijn gereserveerd, zijn de gegevens die van Adobe Analytics tot (en met) mei 2025 in AEP zijn ingevoerd, te vinden onder het &#39;Huidige XDM-veldpad&#39; dat in de onderstaande tabellen wordt aangegeven.

Aangezien de teams van de Analytics van Media en ADC momenteel aan volledige migratie aan de &quot;Rapporterende Weg van het Gebied XDM&quot;werken, zal een officiële mededeling worden gedeeld zodra deze migratie volledig is en &quot;het Pad van het Gebied van XDM&quot;beschikbaar voor gebruik is.

## Streaming media-parameters

| Veldnaam | Huidig XDM-veldpad (afgekeurd) | XDM-veldpad rapporteren | Gegevenstype | Afgeleid veld | Notities |
|--------------------|---------------------------------------------------------------------------|---------------------------------------------------|-----------|-------------------|-----------------------------------------------------------------------|
| Type stream | media.mediaTimed.primaryAssetReference.streamType | mediaReporting.sessionDetails.streamType | Dimension | Type stream |                                                                       |
| Inhoud-id | media.mediaTimed.primaryAssetReference._id | mediaReporting.sessionDetails.name | Dimension | Inhoud-id |                                                                       |
| Lengte inhoud | media.mediaTimed.primaryAssetReference._xmpDM.duration | mediaReporting.sessionDetails.length | Dimension | Lengte inhoud |                                                                       |
| Inhoudstype | media.mediaTimed.primaryAssetViewDetails.broadcastContentType | mediaReporting.sessionDetails.contentType | Dimension | Inhoudstype |                                                                       |
| Mediasessie-id | media.mediaTimed.primaryAssetViewDetails._id | mediaReporting.sessionDetails.ID | Dimension | Mediasessie-id |                                                                       |
| Naam van inhoudspeler | media.mediaTimed.primaryAssetViewDetails.playerName | mediaReporting.sessionDetails.playerName | Dimension | Naam van inhoudspeler |                                                                       |
| Content Channel | media.mediaTimed.primaryAssetViewDetails.broadcastChannel | mediaReporting.sessionDetails.channel | Dimension | Content Channel |                                                                       |
| Segment Inhoud | media.mediaTimed.primaryAssetViewDetails.videoSegment | mediaReporting.sessionDetails.segment | Dimension | Segment Inhoud |                                                                       |
| Inhoudsnaam | media.mediaTimed.primaryAssetReference._dc.title | mediaReporting.sessionDetails.friendlyName | Dimension | Inhoudsnaam |                                                                       |
| Videopad | *niet gebruikt in AEP/CJA* |                                                   |           |                   | Specifieke Adobe Analytics-eigenschap |
| Tonen | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Series._iptc4xmpExt.Name | mediaReporting.sessionDetails.show | Dimension | Tonen |                                                                       |
| Seizoen | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Season._iptc4xmpExt.Name | mediaReporting.sessionDetails.season | Dimension | Seizoen |                                                                       |
| Episode | media.mediaTimed.primaryAssetReference._iptc4xmpExt.episode._iptc4xmpExt.Name | mediaReporting.sessionDetails.episode | Dimension | Episode |                                                                       |
| Genre | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Genre | mediaReporting.sessionDetails.genreList | Dimension | niet ondersteund | Het veld MediaReporting gebruiken |
| Netwerk | media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | mediaReporting.sessionDetails.network | Dimension | Netwerk |                                                                       |
| Tekst tonen | media.mediaTimed.primaryAssetReference.showType | mediaReporting.sessionDetails.showType | Dimension | Tekst tonen |                                                                       |
| MVPD | media.mediaTimed.idp | mediaReporting.sessionDetails.mvpd | Dimension | MVPD |                                                                       |
| Geautoriseerd | Niet ondersteund | mediaReporting.sessionDetails.authorized | Dimension | Geautoriseerd |                                                                       |
| Dagdeel | Niet ondersteund | mediaReporting.sessionDetails.dayPart | Dimension | Dagdeel |                                                                       |
| Type mediafeed | media.mediaTimed.primaryAssetViewDetails.sourceFeed | mediaReporting.sessionDetails.feed | Dimension | Type mediafeed |                                                                       |
| Artiest | media.mediaTimed.primaryAssetReference._xmpDM.artist | mediaReporting.sessionDetails.artist | Dimension | Artiest |                                                                       |
| Album | media.mediaTimed.primaryAssetReference._xmpDM.album | mediaReporting.sessionDetails.album | Dimension | Album |                                                                       |
| Label | Niet ondersteund | mediaReporting.sessionDetails.label | Dimension | Label |                                                                       |
| Auteur | Niet ondersteund | mediaReporting.sessionDetails.author | Dimension | Auteur |                                                                       |
| Station | media.mediaTimed.primaryAssetReference._id3.Audio._id3.TRSN | mediaReporting.sessionDetails.station | Dimension | Station |                                                                       |
| Uitgever | media.mediaTimed.primaryAssetReference._id3.Audio._id3.TPUB | mediaReporting.sessionDetails.publisher | Dimension | Uitgever |                                                                       |
| Start media | media.mediaTimed.impressions.value | mediaReporting.sessionDetails.isViewed | Metrisch | Start media |                                                                       |
| Inhoud start | media.mediaTimed.starts.value | mediaReporting.sessionDetails.isPlayed | Metrisch | Inhoud start |                                                                       |
| Inhoud voltooid | media.mediaTimed.completes.value | mediaReporting.sessionDetails.isCompleted | Metrisch | Inhoud voltooid |                                                                       |
| Tijd van inhoud besteed | media.mediaTimed.timePlayed.value | mediaReporting.sessionDetails.timePlayed | Metrisch | Tijd van inhoud besteed |                                                                       |
| Tijd besteed aan media | media.mediaTimed.totalTimePlayed.value | mediaReporting.sessionDetails.totalTimePlayed | Metrisch | Tijd besteed aan media |                                                                       |
| Unieke afgespeelde tijd | Niet ondersteund | mediaReporting.sessionDetails.uniqueTimePlayed | Metrisch | Unieke afgespeelde tijd |                                                                       |
| Voortgangsmarkering 10% | media.mediaTimed.progress10.value | mediaReporting.sessionDetails.hasProgress10 | Metrisch | Voortgangsmarkering 10% |                                                                       |
| Voortgangsmarkering van 25% | media.mediaTimed.progress25.value | mediaReporting.sessionDetails.hasProgress25 | Metrisch | Voortgangsmarkering van 25% |                                                                       |
| 50% voortgangsmarkering | media.mediaTimed.progress50.value | mediaReporting.sessionDetails.hasProgress50 | Metrisch | 50% voortgangsmarkering |                                                                       |
| 75% voortgangsmarkering | media.mediaTimed.progress75.value | mediaReporting.sessionDetails.hasProgress75 | Metrisch | 75% voortgangsmarkering |                                                                       |
| 95% voortgangsmarkering | media.mediaTimed.progress95.value | mediaReporting.sessionDetails.hasProgress95 | Metrisch | 95% voortgangsmarkering |                                                                       |
| Gemiddeld aantal minuten publiek | Niet ondersteund | mediaReporting.sessionDetails.averageMinuteAudience | Metrisch | Gemiddeld aantal minuten publiek |                                                                  |
| Seconden sinds laatste Vraag | media.mediaTimed.primaryAssetViewDetails.sessionTimeout | mediaReporting.sessionDetails.secondsSinceLastCall | Metrisch | Seconden sinds laatste Vraag |                                                              |
| Gepauzeerde beïnvloede stromen | Niet ondersteund | mediaReporting.sessionDetails.hasPauseImpactedStreams | Metrisch | Gepauzeerde beïnvloede stromen | wij behandelen mediaTimed door deze waarde van andere gebeurtenissen te berekenen |
| Gebeurtenissen pauzeren | media.mediaTimed.pauses.value | mediaReporting.sessionDetails.pauseCount | Metrisch | Gebeurtenissen pauzeren |                                                                       |
| Totale pauzeduur | media.mediaTimed.pauseTime.value | mediaReporting.sessionDetails.pauseTime | Metrisch | Totale pauzeduur |                                                                       |
| Inhoudshervattingen | media.mediaTimed.resumes.value | mediaReporting.sessionDetails.hasResume | Metrisch | Inhoudshervattingen |                                                                       |
| Weergaven van inhoudssegmenten | media.mediaTimed.mediaSegmentViews.value | mediaReporting.sessionDetails.hasSegmentView | Metrisch | Weergaven van inhoudssegmenten |                                                                     |

{style="table-layout:auto"}

## Update voor parameters van Player-statussen

| Veldnaam | Huidig XDM-veldpad (afgekeurd) | XDM-veldpad rapporteren | Gegevenstype | Afgeleid veld | Notities |
|----------------------------|-------------------------------------|----------------------------------|-----------|----------------|--------------------------------------|
| Streams die worden beïnvloed door Player-statussen | Niet ondersteund | mediaReporting.states.isSet | Metrisch | niet ondersteund | gebruik mediaReporting, veld |
| Aantal spelersstatussen | Niet ondersteund | mediaReporting.states.count | Metrisch | niet ondersteund | gebruik mediaReporting, veld |
| Totale duur spelersstatussen | Niet ondersteund | mediaReporting.states.time | Metrisch | niet ondersteund | gebruik mediaReporting, veld |
| Framenaam van speler | Niet ondersteund | mediaReporting.states.name | Dimension | niet ondersteund | gebruik mediaReporting, veld |

{style="table-layout:auto"}

## Hoofdstukparameters

| Veldnaam | Huidig XDM-veldpad (afgekeurd) | XDM-veldpad rapporteren | Gegevenstype | Afgeleid veld | Notities |
|------------------|--------------------------------------------------------------|-------------------------------------------|-----------|----------------|-----------|
| Hoofdstuk | media.mediaTimed.mediaChapter.chapterAssetReference._id | mediaReporting.chapterDetails.ID | Dimension | Hoofdstuk |           |
| Begin hoofdstuk | media.mediaTimed.mediaChapter.impressions.value | mediaReporting.chapterDetails.isStarted | Metrisch | Begin hoofdstuk |           |
| Hoofdstuk voltooid | media.mediaTimed.mediaChapter.completes.value | mediaReporting.chapterDetails.isCompleted | Metrisch | Hoofdstuk voltooid |          |
| Tijd besteed aan hoofdstuk | media.mediaTimed.mediaChapter.timePlayed.value | mediaReporting.chapterDetails.timePlayed | Metrisch | Tijd besteed aan hoofdstuk |        |

{style="table-layout:auto"}

## Ad-parameters

| Veldnaam | Huidig XDM-veldpad (afgekeurd) | XDM-veldpad rapporteren | Gegevenstype | Afgeleid veld | Notities |
|------------------|--------------------------------------------------------------|------------------------------------------------|-----------|----------------|-----------|
| ID advertentie | advertising.adAssetReference._id | mediaReporting.advertisingDetails.name | Dimension | ID advertentie |           |
| Positie advertentie in pod | advertising.adAssetViewDetails.index | mediaReporting.advertisingDetails.podPosition | Dimension | Positie advertentie in pod |     |
| Advertentieduur | advertising.adAssetReference._xmpDM.duration | mediaReporting.advertisingDetails.length | Metrisch | Advertentieduur |           |
| Naam van advertentiespeler | advertising.adAssetViewDetails.playerName | mediaReporting.advertisingDetails.playerName | Dimension | Naam van advertentiespeler |           |
| ID Advertentie-einde | advertising.adAssetViewDetails.adBreak._id | mediaReporting.advertisingPodDetails.ID | Dimension | ID Advertentie-einde |           |
| Advertentienaam | advertising.adAssetReference._dc.title | mediaReporting.advertisingDetails.friendlyName | Dimension | Advertentienaam |           |
| Adverteerder | advertising.adAssetReference.advertiser | mediaReporting.advertisingDetails.advertiser | Dimension | Adverteerder |           |
| Campagne-id | advertising.adAssetReference.campaign | mediaReporting.advertisingDetails.campaignID | Dimension | Campagne-id |           |
| Ad Start | advertising.impressions.value | mediaReporting.advertisingDetails.isStarted | Metrisch | Ad Start |           |
| Toevoegen voltooid | advertising.completes.value | mediaReporting.advertisingDetails.isCompleted | Metrisch | Toevoegen voltooid |           |
| Toegevoegde tijd | advertising.timePlayed.value | mediaReporting.advertisingDetails.timePlayed | Metrisch | Toegevoegde tijd |           |

{style="table-layout:auto"}

## Parameters voor kwaliteit

| Veldnaam | Huidig XDM-veldpad (afgekeurd) | XDM-veldpad rapporteren | Gegevenstype | Afgeleide velden | Notities |
|------------------------|--------------------------------------------------------------|------------------------------------------------|-----------|----------------|-----------|
| Gemiddelde bitsnelheid | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverage.value | mediaReporting.qoeDataDetails.bitrateAverage | Beide | Gemiddelde bitsnelheid |           |
| Te starten tijd | media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart.value | mediaReporting.qoeDataDetails.timeToStart | Beide | Te starten tijd |           |
| Gedropte frames | media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames.value | mediaReporting.qoeDataDetails.droppedFrames | Beide | Gedropte frames |           |
| Buffergebeurtenissen | media.mediaTimed.primaryAssetViewDetails.qoe.buffers.value | mediaReporting.qoeDataDetails.bufferCount | Beide | Buffergebeurtenissen |           |
| Totale bufferduur | media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime.value | mediaReporting.qoeDataDetails.bufferTime | Beide | Totale bufferduur |     |
| Wijzigingen in bitsnelheid | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges.value | mediaReporting.qoeDataDetails.bitrateChangeCount | Beide | Wijzigingen in bitsnelheid |         |
| Fouten/foutgebeurtenissen | media.mediaTimed.primaryAssetViewDetails.qoe.errors.value | mediaReporting.qoeDataDetails.errorCount | Beide | Fouten/foutgebeurtenissen |  |
| SDK-fout-id&#39;s van speler | media.mediaTimed.primaryAssetViewDetails.qoe.playerSdkErrors | mediaReporting.qoeDataDetails.playerSdkErrors | Dimension | niet ondersteund | gebruik mediaReporting, veld |
| Externe fout-id&#39;s | media.mediaTimed.primaryAssetViewDetails.qoe.externalSdkErrors | mediaReporting.qoeDataDetails.externalErrors | Dimension | niet ondersteund | gebruik mediaReporting, veld |
| Druppels voor starten | media.mediaTimed.dropBeforeStarts.value | mediaReporting.qoeDataDetails.isDroppedBeforeStart | Metrisch | Druppels voor starten |     |
| Door buffer beïnvloede stromen | Niet ondersteund | mediaReporting.qoeDataDetails.hasBufferImpactedStreams | Metrisch | Door buffer beïnvloede stromen | berekend uit andere gebeurtenissen |
| Door bitsnelheidwijziging beïnvloede stromen | Niet ondersteund | mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams | Metrisch | Door bitsnelheidwijziging beïnvloede stromen | berekend uit andere gebeurtenissen |
| Fout beïnvloede stromen | Niet ondersteund | mediaReporting.qoeDataDetails.hasErrorImpactedStreams | Metrisch | Fout beïnvloede stromen | berekend uit andere gebeurtenissen |
| Gedropte framestromen | Niet ondersteund | mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams | Metrisch | Gedropte framestromen | berekend uit andere gebeurtenissen |

{style="table-layout:auto"}

## Classificaties van media-analyses

De classificaties van Media Analytics worden opgenomen in AEP via een aparte flow die bekend staat als ACDC. Elke classificatiegroep die in de onderstaande tabel wordt vermeld, komt overeen met een unieke dataset in AEP. In CJA moet een verbinding tot stand worden gebracht tussen de gegevensset van de Media Analytics-gebeurtenis en elk van de gegevenssets voor de classificatie.

### Gegevenssets verbinden in Customer Journey Analytics

De verbinding instellen in Customer Journey Analytics:

- Navigeer aan het **lusje van Verbindingen** en selecteer **creeer nieuwe verbinding**.
- In de interface van Verbindingen, kies **datasets** toevoegen en van de de gebeurtenisdataset van de Analyse van Media de plaats bepalen (die voor het invoeren van media gegevens via ADC), samen met de vier relevante classificatiedatasets wordt gebruikt.

### Configuratiedetails

Voor elke raadplegingsdataset (classificatiedataset), vorm als volgt:

- **videodataset**:
   - Sleutel: `_sandbox.key`
   - Overeenkomende toets: `Asset ID (media.mediaTimed.primaryAssetReference._id)`
   - Type gegevensbron: `Web Data`

- **videodataset**:
   - Sleutel: `_sandbox.key`
   - Overeenkomende toets: `Ad ID (advertising.adAssetReference._id)`
   - Type gegevensbron: `Web Data`

- **videoadpod dataset**:
   - Sleutel: `_sandbox.key`
   - Overeenkomende toets: `Ad Pod ID (advertising.adAssetViewDetails.adBreak._id)`
   - Type gegevensbron: `Web Data`

- **dataset van het videohoofdstuk**:
   - Sleutel: `_sandbox.key`
   - Overeenkomende toets: `Chapter identity (media.mediaTimed.mediaChapter.chapterAssetReference._id)`
   - Type gegevensbron: `Web Data`

### Rapporteringsoverwegingen

Wanneer het werken met de classificatiedatasets tijdens het melden, zorg ervoor dat u classificatiespecifieke gebiedspaden (`ACDC XDM Path`) in plaats van de standaardMedia Analytics XDM gebieden van Media van verwijzingen voorziet.

## Classificatietabel

| Indelingsnaam (groep) | Veldnaam | ACDC XDM Path |
|------------|----------|-------------|
| video | Sleutel-/element-id | `<_sandbox>.key` |
| video | Videolengte | `<_sandbox>.video_length` |
| video | Videonaam | `<_sandbox>.video_name` |
| video | Element-id | `<_sandbox>.asset_id` |
| video | Eerste luchtdatum | `<_sandbox>.first_air_date` |
| video | Eerste digitale datum | `<_sandbox>.first_digital_date` |
| video | Classificatie van inhoud | `<_sandbox>.content_rating` |
| video | Maker | `<_sandbox>.originator` |
| video | Sleutel-/advertentie-id | `<_sandbox>.key` |
| video | Advertentieduur | `<_sandbox>.ad_length` |
| video | Advertentienaam | `<_sandbox>.ad_name` |
| video | Creative-id | `<_sandbox>.creative_id` |
| videoadpod | Sleutel-/advertentiepod-id | `<_sandbox>.key` |
| videoadpod | Podpositie | `<_sandbox>.pod_position` |
| videoadpod | Podnaam | `<_sandbox>.pod_name` |
| videohoofdstuk | Sleutel/Hoofdstuk | `<_sandbox>.key` |
| videohoofdstuk | Hoofdstuklengte | `<_sandbox>.chapter_length` |
| videohoofdstuk | Verschuiving hoofdstuk | `<_sandbox>.chapter_offset` |
| videohoofdstuk | Hoofdstukpositie | `<_sandbox>.chapter_position` |
| videohoofdstuk | Hoofdstuknaam | `<_sandbox>.chapter_name` |

{style="table-layout:auto"}

## Aangepaste variabelen voor media-analyse

In Adobe Analytics, worden de douanevariabelen toegewezen aan verschillende gebeurtenissen of eVars afhankelijk van de implementatieregels die binnen elke rapportreeks worden bepaald. Als deze aangepaste variabelen in Adobe Experience Platform (AEP) worden geïmporteerd, worden ze daarom toegewezen aan verschillende XDM-paden.

- Gebeurtenissen worden opgeslagen onder het pad:

  `_experience.analytics.event<x>to<y>.event<number>.value`

- Vars worden opgeslagen onder het pad:

  `_experience.analytics.customDimensions.eVars.eVar<number>`

In beide gevallen komt `<number>` overeen met de specifieke gebeurtenis of het eVar-nummer dat wordt gebruikt in de oorspronkelijke configuratie van de Adobe Analytics-rapportsuite.

### Aangepaste variabelen

| Veldnaam | XDM-pad | Gegevenstype |
|-------------|-------------|-----------|
| Markering voor gedownloade media | `_experience.analytics.event<x>to<y>.event<number>.value` | Metrisch |
| SDK-versie | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| VHL-versie | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| Stroomindeling | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| Eerste luchtdatum | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| Eerste digitale datum | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| Federale gegevens | `_experience.analytics.customDimensions.eVars.eVar<number>` en `_experience.analytics.event<x>to<y>.event<number>.value` | Beide |
| Geschatte stromen | `_experience.analytics.event<x>to<y>.event<number>.value` | Metrisch |
| Aantal advertenties | `_experience.analytics.event<x>to<y>.event<number>.value` | Metrisch |
| Hoofdstuk tellen | `_experience.analytics.event<x>to<y>.event<number>.value` | Metrisch |
| Creative-id | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| Site-id | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| CREATIVE URL | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| Plaatsing-id | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| Frames per seconde | `_experience.analytics.customDimensions.eVars.eVar<number>` en `_experience.analytics.event<x>to<y>.event<number>.value` | Beide |
| Media SDK-fout-id&#39;s | `_experience.analytics.event<x>to<y>.event<number>.value` | Metrisch |
| Betrokken stromen stoppen | `_experience.analytics.event<x>to<y>.event<number>.value` | Metrisch |
| Stalling Events | `_experience.analytics.event<x>to<y>.event<number>.value` | Metrisch |
| Totale stapelduur | `_experience.analytics.event<x>to<y>.event<number>.value` | Metrisch |

{style="table-layout:auto"}






