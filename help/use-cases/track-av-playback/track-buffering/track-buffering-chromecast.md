---
title: Leer hoe u buffering kunt bijhouden op Chromecast
description: Leer hoe u buffergebeurtenissen kunt bijhouden op Chromecast.
uuid: f6fa3a1a-d7de-4293-bd11-ebe9e130badd
exl-id: 26fd1e2a-4103-486f-be12-36b088d28cb6
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# Trackbuffering op chroecast{#track-buffering-on-chromecast}

De volgende instructies bieden richtlijnen voor implementatie voor alle 2.x SDK&#39;s.

>[!IMPORTANT]
>
>Als u een 1.x versie van SDK uitvoert, kunt u de 1.x Gidsen van Ontwikkelaars hier downloaden: [ Download SDKs.](/help/getting-started/download-sdks.md)

## Constanten voor bufferspatiëring


| Naam van constante | Beschrijving     |
|---|---|
| `BufferStart` | Constante voor het bijhouden van de bufferstartgebeurtenis |
| `BufferComplete` | Constante voor het bijhouden van de gebeurtenis Buffer Complete |

## Buffering implementeren

1. Luister naar de playback die gebeurtenissen van media speler als buffer optreden, en op gebeurtenisbericht van het bufferbegin, spoor die de `BufferStart` gebeurtenis gebruiken als buffer optreden: [ trackEvent ](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferStart);
   ```

1. Op buffer volledig bericht van de media speler, spoor het eind van het als buffer optreden voor gebruikend de `BufferComplete` gebeurtenis: [ trackEvent ](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferComplete);
   ```

Zie het volgende scenario [ playback van VOD met het als buffer optreden voor ](/help/use-cases/tracking-scenarios/vod-buffering.md) voor meer informatie.
