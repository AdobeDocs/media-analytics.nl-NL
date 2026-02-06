---
title: Versie 1.x naar 2.x API-conversie
description: Verken API-referenties en lijsten met vereiste en optionele API's voor bijhouden voor de 1.x- en 2.x-versie van Media SDK.
uuid: 6e619288-c082-4cb4-8685-e90823dadf4a
exl-id: 8d06b7df-f246-49e6-aa58-91a9d6fa889a
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 2%

---

# Verouderde API — 1.x tot 2.x-conversie {#one-x-to-two-x-conv}

## Referenties voor de Media SDK 2.x API

* [&#x200B; Android API Verwijzing &#x200B;](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/index.html)
* [&#x200B; iOS API Verwijzing &#x200B;](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/index.html)
* [&#x200B; JS API Verwijzing &#x200B;](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/index.html)
* [&#x200B; Chromecast API Verwijzing &#x200B;](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/index.html)

## Vereiste track*-API&#39;s:

|  VHL 1.x  | VHL 2.x |
|---|---|
| `videoPlayerPlugin.trackVideoLoad()` | N.v.t. |
| `videoPlayerPlugin.trackSessionStart()` | [&#x200B; mediaHeartbeat.trackSessionStart (mediaObject, mediaCustomMetadata) &#x200B;](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackSessionStart) |
| `videoPlayerPlugin.trackPlay()` | [&#x200B; mediaHeartbeat.trackPlay () &#x200B;](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackPlay) |
| `videoPlayerPlugin.trackPause()` | [&#x200B; mediaHeartbone.trackPause () &#x200B;](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackPause) |
| `videoPlayerPlugin.trackComplete()` | [&#x200B; mediaHeartbone.trackComplete () &#x200B;](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackComplete) |
| `videoPlayerPlugin.trackVideoUnload()` | [&#x200B; mediaHeartbeat.trackSessionEnd () &#x200B;](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackSessionEnd) |
| `videoPlayerPlugin.trackApplicationError()` | N.v.t. |
| `videoPlayerPlugin.trackVideoPlayerError()` | [&#x200B; mediaHeartbone.trackError () &#x200B;](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackError) |

Alle optionele API&#39;s voor reeksspatiëring, zoals advertenties, hoofdstukken, wijzigingen in bitsnelheid, zoeken en bufferen, maken nu deel uit van één `trackEvent` -API. [&#x200B; trackEvent &#x200B;](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackEvent) API ontvangt een constante parameter die het type van gebeurtenis vertegenwoordigt dat het aan spoor is bedoeld:

## Optionele trackEvent-API&#39;s:

| VHL 1.x | VHL 2.x |
|---|---|
| Een geldige `AdBreakInfo` in `VideoPlayerPlugin.getAdBreakInfo()` retourneren | `trackEvent(Event.AdBreakStart)` |
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
