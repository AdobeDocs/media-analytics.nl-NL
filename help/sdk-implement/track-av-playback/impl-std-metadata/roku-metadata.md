---
title: Verklaarde de Sleutels van Meta-gegevens van Roku
description: Leer meer over de beschikbare Roku-metagegevenssleutels en bekijk de volledige lijst met standaardmetagegevensconstanten.
uuid: 2ca6bb1d-c545-43d3-9c3e-63b890aa268d
exl-id: 687dbaa5-4723-4b3f-ab1e-4d5bf447cddf
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 1%

---

# Metagegevens roteren{#roku-metadata-keys}

Standaard video-, audio- en advertentiemetagegevens kunnen worden ingesteld voor respectievelijk media- en advertentie-info-objecten. Met de constantensleutels voor video- en metagegevens stelt u het woordenboek met standaardmetagegevens van het info-object in voordat u de track-API&#39;s oproept. Raadpleeg de onderstaande tabellen voor de volledige lijst met standaardmetagegevensconstanten, gevolgd door een voorbeeld.

## Constanten van videometagegevens {#video-metadata-constants}

| Naam metagegevens | Context Data Key | Naam van constante |
| --- | --- | --- |
| Tonen | `a.media.show` | `MEDIA_VideoMetadataKeySHOW` |
| Seizoen | `a.media.season` | `MEDIA_VideoMetadataKeySEASON` |
| Episode | `a.media.episode` | `MEDIA_VideoMetadataKeyEPISODE` |
| Element | `a.media.asset` | `MEDIA_VideoMetadataKeyASSET_ID` |
| Genre | `a.media.genre` | `MEDIA_VideoMetadataKeyGENRE` |
| Eerste luchtdatum | `a.media.airDate` | `MEDIA_VideoMetadataKeyFIRST_AIR_DATE` |
| Eerste digitale luchtdatum | `a.media.digitalDate` | `MEDIA_VideoMetadataKeyFIRST_DIGITAL_DATE` |
| Classificatie | `a.media.rating` | `MEDIA_VideoMetadataKeyRATING` |
| Maker | `a.media.originator` | `MEDIA_VideoMetadataKeyORIGINATOR` |
| Netwerk | `a.media.network` | `MEDIA_VideoMetadataKeyNETWORK` |
| Tekst tonen | `a.media.type` | `MEDIA_VideoMetadataKeySHOW_TYPE` |
| Advertentie laden | `a.media.adLoad` | `MEDIA_VideoMetadataKeyAD_LOAD` |
| MVPD | `a.media.pass.mvpd` | `MEDIA_VideoMetadataKeyMVPD` |
| Geautoriseerd | `a.media.pass.auth` | `MEDIA_VideoMetadataKeyAUTHORIZED` |
| Dagdeel | `a.media.dayPart` | `MEDIA_VideoMetadataKeyDAY_PART` |
| Feed | `a.media.feed` | `MEDIA_VideoMetadataKeyFEED` |
| Stroomindeling | `a.media.format` | `MEDIA_VideoMetadataKeySTREAM_FORMAT` |

## Constanten van audiometagegevens {#audio-metadata-constants}

| Naam metagegevens | Context Data Key | Naam van constante |
| --- | --- | --- |
| Artiest | `a.media.artist` | `MEDIA_AudioMetadataKeyARTIST` |
| Album | `a.media.album` | `MEDIA_AudioMetadataKeyALBUM` |
| Label | `a.media.label` | `MEDIA_AudioMetadataKeyLABEL` |
| Auteur | `a.media.author` | `MEDIA_AudioMetadataKeyAUTHOR` |
| Station | `a.media.station` | `MEDIA_AudioMetadataKeySTATION` |
| Uitgever | `a.media.publisher` | `MEDIA_AudioMetadataKeyPUBLISHER` |

## Metagegevensconstanten toevoegen {#ad-metadata-constants}

| Naam metagegevens | Context Data Key | Naam van constante |
| --- | --- | --- |
| Adverteerder | `a.media.ad.advertiser` | `MEDIA_AdMetadataKeyADVERTISER` |
| Campagne-id | `a.media.ad.campaign` | `MEDIA_AdMetadataKeyCAMPAIGN_ID` |
| Creative-id | `a.media.ad.creative` | `MEDIA_AdMetadataKeyCREATIVE_ID` |
| Plaatsing-id | `a.media.ad.placement` | `MEDIA_AdMetadataKeyPLACEMENT_ID` |
| Site-id | `a.media.ad.site` | `MEDIA_AdMetadataKeyPLACEMENT_ID` |
| Creative URL | `a.media.ad.creativeURL` | `MEDIA_AdMetadataKeyCREATIVE_URL` |

## Constanten {#constants}

U kunt de volgende constanten gebruiken om mediagebeurtenissen bij te houden:

### Andere constanten

| Constante | Beschrijving   |
|---|---|
| `ERROR_SOURCE_PLAYER` | Constante voor Flash Player-foutbron |

### MediaObjectKey-constanten (gebruikt als sleutels binnen MediaObject-instanties)

| Constante | Beschrijving   |
| --- | --- |
| `MEDIA_STANDARD_MEDIA_METADATA` | Constante voor het instellen van metagegevens op `MediaInfo` `trackLoad` |
| `MEDIA_STANDARD_AD_METADATA` | Constante om de advertentiemetagegevens op `EventData` `trackEvent` te plaatsen |
| `MEDIA_RESUMED` | Constante voor het verzenden van een video-hervat hartslag. Om video het volgen van eerder tegengehouden inhoud te hervatten, moet u `MEDIA_RESUMED` bezit op `mediaInfo` voorwerp plaatsen wanneer u `mediaTrackLoad` roept. (`MEDIA_RESUMED` is geen gebeurtenis die u kunt volgen gebruikend `mediaTrackEvent` API.) `MEDIA_RESUMED` moet worden ingesteld op true wanneer een toepassing inhoud wil blijven bijhouden die een gebruiker niet meer bekijkt, maar nu opnieuw wil kijken. <br/><br/>Stel dat een gebruiker 30% van de inhoud controleert en de app vervolgens sluit. Hierdoor wordt de sessie beëindigd. Later, als de zelfde gebruiker aan de zelfde inhoud terugkeert, en de toepassing die gebruiker toestaat om van het zelfde punt te hervatten waar zij weggingen, dan zou de toepassing `MEDIA_RESUMED` aan &quot;waar&quot;moeten plaatsen terwijl het roepen van `mediaTrackLoad` API. Het resultaat is dat deze twee verschillende mediasessies voor dezelfde video-inhoud aan elkaar kunnen worden gekoppeld. Hier volgt het implementatievoorbeeld: <br/><br/> `mediaInfo =` <br/>   `adb_media_init_mediainfo(` <br/>     `"test_media_name",` <br/>     `"test_media_id",`<br/>      `10,` <br/>     `"vod"` <br/> `)` <br/> `mediaInfo[ADBMobile().MEDIA_RESUMED] = true` <br/> `mediaContextData = {}` <br/>  `ADBMobile().mediaTrackLoad(mediaInfo, mediaContextData)` <br/><br/>Hierdoor wordt een nieuwe sessie voor de video gemaakt, maar de SDK verzendt ook een hartslagverzoek met het gebeurtenistype &quot;resume&quot;, dat in de rapportage kan worden gebruikt om twee verschillende mediasessies aan elkaar te koppelen. |

### Constanten van inhoudstypen

| Constante | Beschrijving   |
|---|---|
| `MEDIA_STREAM_TYPE_LIVE` | Constante voor stroomtype LIVE |
| `MEDIA_STREAM_TYPE_VOD` | Constante voor het stroomtype VOD |

### Constanten voor gebeurtenistype (gebruikt voor de aanroep van trackEvent)

| Constante | Beschrijving   |
|---|---|
| `MEDIA_BUFFER_START` | Type gebeurtenis voor Start buffer |
| `MEDIA_BUFFER_COMPLETE` | Gebeurtenistype voor buffer voltooid |
| `MEDIA_SEEK_START` | Type gebeurtenis voor begin van zoekopdracht |
| `MEDIA_SEEK_COMPLETE` | Gebeurtenistype voor zoekopdracht voltooid |
| `MEDIA_BITRATE_CHANGE` | Gebeurtenistype voor wijziging van bitsnelheid |
| `MEDIA_CHAPTER_START` | Gebeurtenistype voor Start van hoofdstuk |
| `MEDIA_CHAPTER_COMPLETE` | Type gebeurtenis voor hoofdstuk voltooid |
| `MEDIA_CHAPTER_SKIP` | Gebeurtenistype voor begin advertentie |
| `MEDIA_AD_BREAK_START` | Gebeurtenistype voor begin advertentie |
| `MEDIA_AD_BREAK_COMPLETE` | Gebeurtenistype voor AdBreak voltooid |
| `MEDIA_AD_BREAK_SKIP` | Type gebeurtenis voor AdBreak-overslaan |
| `MEDIA_AD_START` | Gebeurtenistype voor begin advertentie |
| `MEDIA_AD_COMPLETE` | Gebeurtenistype voor advertentie voltooid |
| `MEDIA_AD_SKIP` | Gebeurtenistype voor overslaan van advertentie |
