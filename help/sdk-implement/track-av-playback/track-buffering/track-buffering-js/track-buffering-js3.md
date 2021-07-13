---
title: Leer hoe u buffering kunt bijhouden met JavaScript 3.x
description: Leer hoe u buffergebeurtenissen kunt bijhouden in browser-apps (JS).
exl-id: c6941942-02f9-4f9c-99ad-0c52ed2f793b
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# buffering bijhouden met JavaScript 3.x{#track-buffering-on-javascript}

>[!IMPORTANT]
>
>De volgende instructies bieden richtlijnen voor implementatie voor alle 3.x SDK&#39;s. Als u eerdere versies van de SDK implementeert, kunt u de ontwikkelaarsgidsen hier downloaden: [SDK&#39;s downloaden.](/help/sdk-implement/download-sdks.md)

## Constanten voor bufferspatiëring

| Naam van constante | Beschrijving     |
|---|---|
| `BufferStart` | Constante voor het bijhouden van de bufferstartgebeurtenis |
| `BufferComplete` | Constante voor het bijhouden van de gebeurtenis Buffer Complete |

## Buffering implementeren

1. Luister naar de afspeelbuffergebeurtenissen van de mediaspeler en volg bij de melding van de gebeurtenis buffering van de buffer de buffering met de gebeurtenis `BufferStart`.

   ```js
   _onBufferStart = function() {
       tracker.trackEvent(ADB.Media.Event.BufferStart);
   };
   ```

1. Volg bij het verzenden van het volledige bericht over de buffer vanuit de mediaspeler het einde van de buffering met de gebeurtenis `BufferComplete`.

   ```js
   _onBufferComplete = function() {
       tracker.trackEvent(ADB.Media.Event.BufferComplete);
   };
   ```

Zie het volgende scenario [VOD playback met het als buffer optreden](/help/sdk-implement/tracking-scenarios/vod-buffering.md) voor meer informatie.
