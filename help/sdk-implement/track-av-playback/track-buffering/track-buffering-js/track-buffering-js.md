---
title: buffering bijhouden met JavaScript 2.x
description: Beschrijft het bijhouden van buffergebeurtenissen in browser-apps (JS).
uuid: c380cf2c-7729-4d4a-a4da-581bd94a5896
translation-type: tm+mt
source-git-commit: 318bb60d9835d9a07fb7aa0a0a02162248410d09
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---


# buffering bijhouden met JavaScript 2.x{#track-buffering-on-javascript}

>[!IMPORTANT]
>
>De volgende instructies bieden richtlijnen voor implementatie voor alle 2.x SDK&#39;s. Als u een 1.x-versie van de SDK implementeert, kunt u de 1.x-handleidingen voor ontwikkelaars hier downloaden: [SDK&#39;s downloaden.](/help/sdk-implement/download-sdks.md)

## Constanten voor bufferspatiëring

| Naam van constante | Beschrijving     |
|---|---|
| `BufferStart` | Constante voor het bijhouden van de bufferstartgebeurtenis |
| `BufferComplete` | Constante voor het bijhouden van de gebeurtenis Buffer Complete |

## Buffering implementeren

1. Luister naar de buffergebeurtenissen voor het afspelen vanaf de mediaspeler en volg de buffering van de `BufferStart` gebeurtenis bij het melden van de buffergebeurtenis.

   ```js
   _onBufferStart = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart);
   };
   ```

1. Volg bij het verzenden van het volledige bericht over de buffer vanuit de mediaspeler het einde van de buffering met behulp van de `BufferComplete` gebeurtenis.

   ```js
   _onBufferComplete = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete);
   };
   ```

Zie het volgende scenario [VOD playback met het als buffer optreden](/help/sdk-implement/tracking-scenarios/vod-buffering.md) voor voor meer informatie.
