---
title: Details testoproep
description: Onderzoek de vraag u moet maken om uw implementatie te bevestigen.
uuid: d3a0e62f-2fc3-413d-ac56-adbbc9b3e983
exl-id: 5e167714-3f0c-4afa-b171-7d51cff6522e
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 11%

---

# Details van de telefoongesprek testen{#test-call-details}

## De mediaspeler starten {#start-the-media-player}

### Aanroep Adobe Analytics (AppMeasurement) starten {#aa-start-call}

| Parameter |  Waarde (monster)  |
|---|---|
| `pev2` | ms_s |
| `a.media.friendlyName` | Episodetitel |
| _**`a.media.name`**_ | _**123456**_ |
| _**`a.media.length`**_ | _**120**_ |
| `a.media.playerName` | HTML5 |
| _**`a.media.view`**_ | _**true**_ |
| `a.contentType` | vod |
| _**`custom.[value]`**_ | _**Aangepaste metagegevensvelden**_ |
| _**`a.media.[value]`**_ | _**Standaardmetagegevensvelden**_ |

**Opmerkingen:**

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
| _**`l:event:playhead`**_ | _**0**_ |
| `l:event:duration` | 4 |
| `s:asset:name` | Episodetitel |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | hoofd |
| _**`s:meta:custom.[value]`**_ | _**Aangepaste metagegevensvelden**_ |
| _**`s:meta:a.media.[value]`**_ | _**Standaardmetagegevensvelden**_ |

**Opmerkingen:**

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
| `s:meta:a.media.ad_load` | 3 |
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
| _**`s:event:type`**_ | _**aa_start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | Episodetitel |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | hoofd |

**Opmerkingen:**

* Deze aanroep geeft aan dat de Media SDK heeft verzocht dat een Adobe Analytics `pev2=ms_s`-aanroep naar de Adobe Analytics-server (AppMeasurement) wordt verzonden.
* Deze aanroep bevat geen aangepaste metagegevens.

## Weergeven en afspelen {#view-ad-playback}

### Aanroep Adobe Analytics (AppMeasurement) en Start {#aa-ad-start-call}

| Parameter |  Waarde (monster)  |
|---|---|
| _**`pev2`**_ | _**msa_s**_ |
| `a.media.name` | 123456 |
| _**`a.media.ad.name`**_ | _**9378**_ |
| `a.media.ad.friendlyName` | Video_VPAID_DFA |
| `a.media.ad.podFriendlyName` | preroll |
| _**`a.media.ad.length`**_ | _**15**_ |
| `a.media.ad.playerName` | HTML5 |
| `a.media.ad.pod` | c27aaf3ff8224bb6b9ebfe1b2e79073d_1 |
| `a.media.ad.podPosition` | 3 |
| `a.media.ad.podSecond` | 0,0 |
| _**`a.media.ad.view`**_ | _**Waar**_ |
| _**`custom.[value]`**_ | _**Metagegevensvelden**_ |
| _**`a.media.[value]`**_ | _**Standaardmetagegevensvelden**_ |

**Opmerkingen:**

* Er moeten extra contextgegevensvariabelen aanwezig zijn die metagegevens bevatten. Zie de metagegevens hieronder.
* De lengte van de advertentie kan worden ingesteld op -1 als deze niet beschikbaar is bij het starten van de advertentie.

### Standaardmetagegevens in Adobe Analytics (AppMeasurement) en aanroep starten {#std-metadata-aa-ad-start}

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

### Aangepaste metagegevens in Adobe Analytics (AppMeasurement) en aanroep starten {#custom-metadata-aa-ad-start}

| Parameter |  Waarde (monster)  |
|---|---|
| `custom.metadata` | value |
| `custom.metadata` | value |

### Media Analytics (hartslagen) en de vraag van het Begin {#ma-ad-start-call}

| Parameter |  Waarde (monster)  |
|---|---|
| _**`s:event:type`**_ | _**start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:ad_id` | 9378 |
| _**`l:asset:length`**_ | _**120**_ |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**advertentie**_ |
| _**`s:meta:custom.[value]`**_ | _**Aangepaste metagegevensvelden**_ |
| _**`s:meta:a.media.[value]`**_ | _**Standaardmetagegevensvelden**_ |

**Opmerkingen:**

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
| `s:meta:a.media.ad_load` | 3 |
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
| _**`s:event:type`**_ | _**aa_ad_start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| `s:asset:type` | advertentie |

### Media Analytics (heartbeats) en Play call {#ma-ad-play-call}

| Parameter |  Waarde (monster)  |
|---|---|
| _**`s:event:type`**_ | _**play**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**advertentie**_ |

### Media Analytics (hartslagen) en Pauze vraag {#ma-ad-pause-call}

| Parameter |  Waarde (monster)  |
|---|---|
| _**`s:event:type`**_ | _**pauzeren**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**advertentie**_ |

### Media Analytics (heartbeats) Adobe Analytics Ad Complete call {#ma-aa-ad-complete-call}

| Parameter |  Waarde (monster)  |
|---|---|
| _**`s:event:type`**_ | _**complete**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**advertentie**_ |

## Hoofdinhoud afspelen {#play-main-content}

### Media Analytics (heartbeats) Play call {#ma-play-call}

| Parameter |  Waarde (monster)  |
|---|---|
| `s:event:type` | play |
| _**`l:event:playhead`**_ | _**29**_ |
| _**`l:event:duration`**_ | _**10189**_ |
| `s:asset:name` | Episodetitel |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | hoofd |

**Opmerkingen:**

* De positie van de afspeelkop moet met 10 seconden toenemen bij elke afspeelaanroep.
* De `l:event:duration` waarde vertegenwoordigt het aantal milliseconden sinds de laatste het volgen vraag en zou ruwweg de zelfde waarde op elke 10 tweede vraag moeten zijn.

## Hoofdinhoud pauzeren {#pause-main-content}

### Media Analytics (heartbeats) Aanroep pauzeren {#ma-pause-call}

| Parameter |  Waarde (monster)  |
|---|---|
| _**`s:event:type`**_ | _**pauzeren**_ |
| _**`l:event:playhead`**_ | _**29**_ |
| `l:event:duration` | 10189 |
| `s:asset:name` | Episodetitel |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | hoofd |
