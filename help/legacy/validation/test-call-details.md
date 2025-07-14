---
title: Gegevens van testoproep
description: Onderzoek de vraag u moet maken om uw implementatie te bevestigen.
uuid: d3a0e62f-2fc3-413d-ac56-adbbc9b3e983
exl-id: 5e167714-3f0c-4afa-b171-7d51cff6522e
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 8%

---

# Details van de telefoongesprek testen{#test-call-details}

## De mediaspeler starten {#start-the-media-player}

### Adobe Analytics (AppMeasurement) Aanroep starten {#aa-start-call}

| Parameter |  Waarde (monster)  |
|---|---|
| `pev2` | ms_s |
| `a.media.friendlyName` | Episodetitel |
| _&#x200B;**`a.media.name`**&#x200B;_ | _&#x200B;**123456**&#x200B;_ |
| _&#x200B;**`a.media.length`**&#x200B;_ | _&#x200B;**120**&#x200B;_ |
| `a.media.playerName` | HTML5 |
| _&#x200B;**`a.media.view`**&#x200B;_ | _&#x200B;**waar**&#x200B;_ |
| `a.contentType` | vod |
| _&#x200B;**`custom.[value]`**&#x200B;_ | _&#x200B;**de meta-gegevensgebieden van de Douane**&#x200B;_ |
| _&#x200B;**`a.media.[value]`**&#x200B;_ | _&#x200B;**Standaard meta-gegevensgebieden**&#x200B;_ |

**Nota&#39;s:**

* Er moeten extra contextgegevensvariabelen aanwezig zijn die metagegevens bevatten. Zie de metagegevens hieronder.
* De lengte voor lineaire stromen zou aan de beste schatting voor de huidige show moeten worden geplaatst.

### Standaardmetagegevens in Adobe Analytics (AppMeasurement) Aanroep starten {#std-metadata-aa}

| Parameter |  Waarde (monster)  |
|---|---|
| `a.media.show` | Titel tonen |
| `a.media.season` | 6 |
| `a.media.episode` | Episodetitel |
| `a.media.asset_id` | 123456 |
| `a.media.genre` | komedie |
| `a.media.first_air_date` | 2016-07-04 |
| `a.media.rating` | TV-14 |
| `a.media.originator` | productiehuis |
| `a.media.network` | netwerk |
| `a.media.ad_load` | 1 |
| `a.media.mvpd` | mvpd |
| `a.media.authorized` | ontgrendeld |
| `a.media.feed` | geen diervoeder |
| `a.media.stream_format` | 0 |

### Aangepaste metagegevens in Adobe Analytics (AppMeasurement) Aanroep starten {#custom-metadata-aa}

| Parameter |  Waarde (monster)  |
|---|---|
| `custom.metadataA` | value |
| `custom.metadataB` | value |

### Media Analytics (heartbeats) De vraag van het Begin {#ma-start-call}

| Parameter |  Waarde (monster)  |
|---|---|
| `s:event:type` | start |
| _&#x200B;**`l:event:playhead`**&#x200B;_ | _&#x200B;**0**&#x200B;_ |
| `l:event:duration` | 4 |
| `s:asset:name` | Episodetitel |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | hoofd |
| _&#x200B;**`s:meta:custom.[value]`**&#x200B;_ | _&#x200B;**de meta-gegevensgebieden van de Douane**&#x200B;_ |
| _&#x200B;**`s:meta:a.media.[value]`**&#x200B;_ | _&#x200B;**Standaard meta-gegevensgebieden**&#x200B;_ |

**Nota&#39;s:**

* Er moeten extra contextgegevensvariabelen aanwezig zijn die metagegevens bevatten. Zie de metagegevens hieronder.
* De positie van de afspeelkop voor lineaire streams bij het starten van de video moet worden ingesteld op de seconden die zijn verstreken sinds het begin van de huidige show, niet op 0.

### Standaardmetagegevens in Media Analytics (heartbeats) Aanroep starten {#std-metadata-ma}

| Parameter |  Waarde (monster)  |
|---|---|
| `s:meta:a.media.show` | Tonen |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | Episodetitel |
| `s:meta:a.media.asset_id` | 123456 |
| `s:meta:a.media.genre` | komedie |
| `s:meta:a.media.first_air_date` | 2018-07-04 |
| `s:meta:a.media.rating` | TV-14 |
| `s:meta:a.media.originator` | productiehuis |
| `s:meta:a.media.network` | netwerk |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | ontgrendeld |
| `s:meta:a.media.feed` | geen diervoeder |
| `s:meta:a.media.stream_format` | 0 |

### Aangepaste metagegevens in Media Analytics (heartbeats) Aanroep starten {#custom-metadata-ma}

| Parameter |  Waarde (monster)  |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Media Analytics (heartbeats) Adobe Analytics Start call {#ma-aa-start}

| Parameter |  Waarde (monster)  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**aa_start**&#x200B;_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | Episodetitel |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | hoofd |

**Nota&#39;s:**

* Deze aanroep geeft aan dat de Media SDK heeft verzocht dat een Adobe Analytics `pev2=ms_s` -aanroep naar de Adobe Analytics (AppMeasurement)-server wordt verzonden.
* Deze aanroep bevat geen aangepaste metagegevens.

## Weergeven en afspelen {#view-ad-playback}

### Adobe Analytics (AppMeasurement) Aanroep starten {#aa-ad-start-call}

| Parameter |  Waarde (monster)  |
|---|---|
| _&#x200B;**`pev2`**&#x200B;_ | _&#x200B;**msa_s**&#x200B;_ |
| `a.media.name` | 123456 |
| _&#x200B;**`a.media.ad.name`**&#x200B;_ | _&#x200B;**9378**&#x200B;_ |
| `a.media.ad.friendlyName` | Video_VPAID_DFA |
| `a.media.ad.podFriendlyName` | preroll |
| _&#x200B;**`a.media.ad.length`**&#x200B;_ | _&#x200B;**15**&#x200B;_ |
| `a.media.ad.playerName` | HTML5 |
| `a.media.ad.pod` | c27aaf3ff8224bb6b9ebfe1b2e79073d_1 |
| `a.media.ad.podPosition` | 1 |
| `a.media.ad.podSecond` | 0,0 |
| _&#x200B;**`a.media.ad.view`**&#x200B;_ | _&#x200B;**Waar**&#x200B;_ |
| _&#x200B;**`custom.[value]`**&#x200B;_ | _&#x200B;**de gebieden van Meta-gegevens**&#x200B;_ |
| _&#x200B;**`a.media.[value]`**&#x200B;_ | _&#x200B;**Standaard meta-gegevensgebieden**&#x200B;_ |

**Nota&#39;s:**

* Er moeten extra contextgegevensvariabelen aanwezig zijn die metagegevens bevatten. Zie de metagegevens hieronder.
* De lengte van de advertentie kan worden ingesteld op -1 als deze niet beschikbaar is bij het starten van de advertentie.

### Standaardmetagegevens in Adobe Analytics (AppMeasurement) en Aanroep starten {#std-metadata-aa-ad-start}

| Parameter |  Waarde (monster)  |
|---|---|
| `a.media.show` | Titel tonen |
| `a.media.season` | 6 |
| `a.media.episode` | Episodetitel |
| `a.media.asset_id` | 123456 |
| `a.media.genre` | komedie |
| `a.media.first_air_date` | 2016-07-04 |
| `a.media.rating` | TV-14 |
| `a.media.originator` | productiehuis |
| `a.media.network` | netwerk |
| `a.media.ad_load` | 1 |
| `a.media.mvpd` | mvpd |
| `a.media.authorized` | ontgrendeld |
| `a.media.feed` | geen diervoeder |
| `a.media.stream_format` | 0 |

### Aangepaste metagegevens in Adobe Analytics (AppMeasurement) en Aanroep starten {#custom-metadata-aa-ad-start}

| Parameter |  Waarde (monster)  |
|---|---|
| `custom.metadata` | value |
| `custom.metadata` | value |

### Media Analytics (hartslagen) en de vraag van het Begin {#ma-ad-start-call}

| Parameter |  Waarde (monster)  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**begin**&#x200B;_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:ad_id` | 9378 |
| _&#x200B;**`l:asset:length`**&#x200B;_ | _&#x200B;**120**&#x200B;_ |
| `s:stream:type` | vod |
| _&#x200B;**`s:asset:type`**&#x200B;_ | _&#x200B;**ad**&#x200B;_ |
| _&#x200B;**`s:meta:custom.[value]`**&#x200B;_ | _&#x200B;**de meta-gegevensgebieden van de Douane**&#x200B;_ |
| _&#x200B;**`s:meta:a.media.[value]`**&#x200B;_ | _&#x200B;**Standaard meta-gegevensgebieden**&#x200B;_ |

**Nota&#39;s:**

* Er moeten extra contextgegevensvariabelen aanwezig zijn die metagegevens bevatten. Zie de metagegevens hieronder.
* De lengte van de advertentie kan worden ingesteld op -1 als deze niet beschikbaar is bij het starten van de advertentie.

### Standaardmetagegevens in Media Analytics (heartbeats) en Aanroep starten {#std-metadata-ma-ad-start}

| Parameter |  Waarde (monster)  |
|---|---|
| `s:meta:a.media.show` | Tonen |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | Episodetitel |
| `s:meta:a.media.asset_id` | 123456 |
| `s:meta:a.media.genre` | komedie |
| `s:meta:a.media.first_air_date` | 2018-07-04 |
| `s:meta:a.media.rating` | TV-14 |
| `s:meta:a.media.originator` | productiehuis |
| `s:meta:a.media.network` | netwerk |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | ontgrendeld |
| `s:meta:a.media.feed` | geen diervoeder |
| `s:meta:a.media.stream_format` | 0 |

### Aangepaste metagegevens in Media Analytics (hartslagen) en Aanroep starten {#custom-metadata-ma-ad-start}

| Parameter |  Waarde (monster)  |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Media Analytics (heartbeats) Aanroep Adobe Analytics en Start {#ma-aa-ad-start-call}

| Parameter |  Waarde (monster)  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**aa_ad_start**&#x200B;_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| `s:asset:type` | advertentie |

### Media Analytics (heartbeats) en Play call {#ma-ad-play-call}

| Parameter |  Waarde (monster)  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**spel**&#x200B;_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _&#x200B;**`s:asset:type`**&#x200B;_ | _&#x200B;**ad**&#x200B;_ |

### Media Analytics (hartslagen) en Pauze vraag {#ma-ad-pause-call}

| Parameter |  Waarde (monster)  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**pauze**&#x200B;_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _&#x200B;**`s:asset:type`**&#x200B;_ | _&#x200B;**ad**&#x200B;_ |

### Media Analytics (heartbeats) Adobe Analytics Ad Complete call {#ma-aa-ad-complete-call}

| Parameter |  Waarde (monster)  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**volledig**&#x200B;_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _&#x200B;**`s:asset:type`**&#x200B;_ | _&#x200B;**ad**&#x200B;_ |

## Hoofdinhoud afspelen {#play-main-content}

### Media Analytics (heartbeats) Play call {#ma-play-call}

| Parameter |  Waarde (monster)  |
|---|---|
| `s:event:type` | play |
| _&#x200B;**`l:event:playhead`**&#x200B;_ | _&#x200B;**29**&#x200B;_ |
| _&#x200B;**`l:event:duration`**&#x200B;_ | _&#x200B;**10189**&#x200B;_ |
| `s:asset:name` | Episodetitel |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | hoofd |

**Nota&#39;s:**

* De positie van de afspeelkop moet met 10 seconden toenemen bij elke afspeelaanroep.
* De `l:event:duration` waarde vertegenwoordigt het aantal milliseconden sinds de laatste het volgen vraag en zou ruwweg de zelfde waarde op elke 10 tweede vraag moeten zijn.

## Hoofdinhoud pauzeren {#pause-main-content}

### Media Analytics (hartslagen) Aanroep pauzeren {#ma-pause-call}

| Parameter |  Waarde (monster)  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**pauze**&#x200B;_ |
| _&#x200B;**`l:event:playhead`**&#x200B;_ | _&#x200B;**29**&#x200B;_ |
| `l:event:duration` | 10189 |
| `s:asset:name` | Episodetitel |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | hoofd |
