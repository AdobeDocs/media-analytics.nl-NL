---
title: Uitgevoerde chroecast-metagegevenssleutels
description: Leer hoe te om standaardvideo en admeta-gegevens te plaatsen die met het volgen vraag op Chromecast moeten worden verzonden.
uuid: c446ad41-51b8-46d6-9bc1-abfae866023f
exl-id: ccc717ae-d846-4349-8282-5e3511ddeb9b
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 9b2d64e856af6a975b371d7c794197a5541997f1
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 2%

---

# Chromecast-metagegevenssleutels{#chromecast-metadata-keys}

Standaard video- en advertentiemetagegevens kunnen worden ingesteld voor respectievelijk media- en advertentievideo-objecten. Met de constantensleutels voor video- en metagegevens stelt u het woordenboek met standaardmetagegevens van het info-object in voordat u de track-API&#39;s oproept. Raadpleeg de onderstaande tabellen voor de volledige lijst met standaardmetagegevensconstanten, gevolgd door een voorbeeld.

## Metagegevensconstanten {#video-metadata-constants}

| Naam metagegevens | Context Data Key | Naam van constante |
| --- | --- | --- |
| Tonen | `a.media.show` | `ADBMobile.media.VideoMetadataKeys.SHOW` |
| Seizoen | `a.media.season` | `ADBMobile.media.VideoMetadataKeys.SEASON` |
| Episode | `a.media.episode` | `ADBMobile.media.VideoMetadataKeys.EPISODE` |
| Element | `a.media.asset` | `ADBMobile.media.VideoMetadataKeys.TMS_ID` |
| Genre | `a.media.genre` | `ADBMobile.media.VideoMetadataKeys.GENRE` |
| Eerste luchtdatum | `a.media.airDate` | `ADBMobile.media.VideoMetadataKeys.FIRST_AIR_DATE` |
| Eerste digitale luchtdatum | `a.media.digitalDate` | `ADBMobile.media.VideoMetadataKeys.FIRST_DIGITAL_DATE` |
| Classificatie | `a.media.rating` | `ADBMobile.media.VideoMetadataKeys.RATING` |
| Maker | `a.media.originator` | `ADBMobile.media.VideoMetadataKeys.ORIGINATOR` |
| Netwerk | `a.media.network` | `ADBMobile.media.VideoMetadataKeys.NETWORK` |
| Tekst tonen | `a.media.type` | `ADBMobile.media.VideoMetadataKeys.SHOW_TYPE` |
| Advertentie laden | `a.media.adLoad` | `ADBMobile.media.VideoMetadataKeys.AD_LOAD` |
| MVPD | `a.media.pass.mvpd` | `ADBMobile.media.VideoMetadataKeys.MVPD` |
| Geautoriseerd | `a.media.pass.auth` | `ADBMobile.media.VideoMetadataKeys.AUTHORIZED` |
| Dagdeel | `a.media.dayPart` | `ADBMobile.media.VideoMetadataKeys.DAY_PART` |
| Feed | `a.media.feed` | `ADBMobile.media.VideoMetadataKeys.FEED` |
| Stroomindeling | `a.media.format` | `ADBMobile.media.VideoMetadataKeys.STREAM_FORMAT` |

## Metagegevensconstanten toevoegen {#ad-metadata-constants}

| Naam metagegevens | Context Data Key | Naam van constante |
| --- | --- | --- |
| Adverteerder | `a.media.ad.advertiser` | `ADBMobile.media.AdMetadataKeys.ADVERTISER` |
| Campagne-id | `a.media.ad.campaign` | `ADBMobile.media.AdMetadataKeys.CAMPAIGN_ID` |
| Creative-id | `a.media.ad.creative` | `ADBMobile.media.AdMetadataKeys.CREATIVE_ID` |
| Plaatsing-id | `a.media.ad.placement` | `ADBMobile.media.AdMetadataKeys.PLACEMENT_ID` |
| Site-id | `a.media.ad.site` | `ADBMobile.media.AdMetadataKeys.SITE_ID` |
| CREATIVE URL | `a.media.ad.creativeURL` | `ADBMobile.media.AdMetadataKeys.CREATIVE_URL` |

## Voorbeeldimplementaties voor Chromecast {#sample-implementations-for-chromecast}

### Video

```js
// setting Standard Video Metadata as context data on trackLoad API mediaContextData = { } 
mediaMetadata["videotype"] = "episode"; 
 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.SHOW] = "sample show"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.SEASON] = "sample season"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.EPISODE] = "sample episode"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.TMS_ID] = "sample tms_id"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.GENRE] = "sample genre"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.FIRST_AIR_DATE] = "sample first_air_date"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.FIRST_DIGITAL_DATE] = "sample first_digital_date"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.RATING] = "sample rating"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.ORIGINATOR] = "sample originator"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.NETWORK] = "sample network"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.SHOW_TYPE] = "sample show type"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.AD_LOAD] = "sample ad load"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.MVPD] = "sample mvpd"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.AUTHORIZED] = "sample authorized"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.DAY_PART] = "sample day_part"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.FEED] = "sample feed"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.STREAM_FORMAT] = "sample format"; 
 
var mediaObject = ADBMobile.media.createMediaObject(content.name, content.id, content.length, content.streamType); 
mediaObject[ADBMobile.media.MediaObjectKey.StandardVideoMetadata] = standardVideoMetadata; 
ADBMobile.media.trackSessionStart(mediaObject, mediaMetadata); 
```

### Audio

```js
// setting Standard Audio Metadata as context data on trackLoad API mediaContextData = { } 
mediaMetadata["audiotype"] = "podcast"; 
var standardAudioMetadata = {}; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.ARTIST] = "sample artist"; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.ALBUM] = "sample album" ; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.LABEL] = "sample label"; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.AUTHOR] = "sample author" ; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.STATION] = "sample station " ; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.PUBLISHER] = "sample publisher"; 
 
var mediaObject = ADBMobile.media.createMediaObject(content.name, content.id, content.length, content.streamType, content.mediaType); 
mediaObject[ADBMobile.media.MediaObjectKey.StandardAudiooMetadata] = standardAudiooMetadata; 
ADBMobile.media.trackSessionStart(mediaObject, mediaMetadata); 
```

### Adds

```js
// setting Standard Ad Metadata as context data on ad start event 
var standardAdMetadata = {}; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.CAMPAIGN_ID] = "sample campaign"; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.ADVERTISER] = "sample advertiser" ; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.CREATIVE_ID] = "sample creativeid"; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.PLACEMENT_ID] = "sample placement id" ; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.SITE_ID] = "sample site id" ; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.CREATIVE_URL] = "sample creative url"; 
 
var adObject = ADBMobile.media.createAdObject(ad.name, ad.id, ad.position, ad.length); 
adObject[ADBMobile.media.MediaObjectKey.StandardAdMetadata] = standardVideoMetadata; 
 
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, this._player.getAdInfo(), adContextData);
```
