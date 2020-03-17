---
title: 1.x naar 2.x API-conversie
description: Dit onderwerp bevat koppelingen naar API-verwijzingen en lijsten met vereiste en optionele API's voor bijhouden voor 1.x- en 2.x-versie van de Media SDK.
uuid: 6e619288-c082-4cb4-8685-e90823dadf4a
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# API 1.x naar 2.x-conversie {#one-x-to-two-x-conv}

## Referenties voor de Media SDK 2.x API

* [Referentie voor Android API](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/index.html)
* [Referentie voor iOS API](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/index.html)
* [JS API-naslaggids](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/index.html)
* [Referentie voor Chromecast API](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/index.html)

## Vereiste track*-API&#39;s:

|  VHL 1.x | VHL 2.x |
|---|---|
| `videoPlayerPlugin.trackVideoLoad()` | N.v.t. |
| `videoPlayerPlugin.trackSessionStart()` | [mediaHeartbone.trackSessionStart(mediaObject, mediaCustomMetadata)](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackSessionStart) |
| `videoPlayerPlugin.trackPlay()` | [mediaHartslag.trackPlay()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackPlay) |
| `videoPlayerPlugin.trackPause()` | [mediaHartslag.trackPause()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackPause) |
| `videoPlayerPlugin.trackComplete()` | [mediaHartslag.trackComplete()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackComplete) |
| `videoPlayerPlugin.trackVideoUnload()` | [mediaHartslag.trackSessionEnd()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackSessionEnd) |
| `videoPlayerPlugin.trackApplicationError()` | N.v.t. |
| `videoPlayerPlugin.trackVideoPlayerError()` | [mediaHeartbone.trackError()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackError) |

Alle optionele API&#39;s voor reeksspatiëring, zoals advertenties, hoofdstukken, wijzigingen in bitsnelheid, zoeken en bufferen, maken nu deel uit van één `trackEvent` API. De [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackEvent) -API ontvangt een constante parameter die het type gebeurtenis vertegenwoordigt dat moet worden bijgehouden:

## Optionele trackEvent-API&#39;s:

| VHL 1.x | VHL 2.x |
|---|---|
| Een geldige `AdBreakInfo` waarde retourneren in `VideoPlayerPlugin.getAdBreakInfo()` | `trackEvent(Event.AdBreakStart)` |
| null retourneren in `VideoPlayerPlugin.getAdBreakInfo()` | `trackEvent(Event.AdBreakComplete)` |
| `playerPlugin.trackAdStart()` | `trackEvent(Event.AdStart, adObject, adCustomMetadata)` |
| `playerPlugin.trackAdComplete()` | `trackEvent(Event.AdComplete)` |
| null retourneren in `VideoPlayerPlugin.getAdInfo()` | `trackEvent(Event.AdSkip)` |
| `playerPlugin.trackChapterStart()` | `trackEvent(Event.ChapterStart, chapterObject, chapterCustomMetadata)` |
| `playerPlugin.trackChapterComplete()` | `trackEvent(Event.ChapterComplete)` |
| null retourneren in `VideoPlayerPlugin.getChapterInfo()` | `trackEvent(Event.ChapterSkip)` |
| `playerPlugin.trackSeekStart()` | `trackEvent(Event.SeekStart)` |
| `playerPlugin.trackSeekComplete()` | `trackEvent(Event.SeekComplete)` |
| `playerPlugin.trackBufferStart()` | `trackEvent(Event.BufferStart)` |
| `playerPlugin.trackBufferComplete()` | `trackEvent(Event.BufferComplete)` |
| `playerPlugin.trackBitrateChange()` | `trackEvent(Event.BitrateChange)` |
| `playerPlugin.trackTimedMetadata()` | `trackEvent(Event.TimedMetadataUpdate)` |

