---
title: Leer hoe u buffering kunt bijhouden met JavaScript 3.x
description: Leer hoe u buffergebeurtenissen kunt bijhouden in browser-apps (JS).
exl-id: c6941942-02f9-4f9c-99ad-0c52ed2f793b
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# buffering bijhouden met JavaScript 3.x{#track-buffering-on-javascript}

De volgende instructies bieden richtlijnen voor implementatie voor alle 3.x SDK&#39;s.

>[!IMPORTANT]
>
>Als u om het even welke vorige versies van SDK uitvoert, kunt u de Gidsen van Ontwikkelaars hier downloaden: [ Download SDKs.](/help/getting-started/download-sdks.md)

## Constanten voor bufferspatiëring

| Naam van constante | Beschrijving     |
|---|---|
| `BufferStart` | Constante voor het bijhouden van de bufferstartgebeurtenis |
| `BufferComplete` | Constante voor het bijhouden van de gebeurtenis Buffer Complete |

## Buffering implementeren

1. Luister naar de buffergebeurtenissen voor het afspelen vanaf de mediaspeler en volg de buffering met de gebeurtenis `BufferStart` bij het melden van de buffergebeurtenis.

   ```js
   _onBufferStart = function() {
       tracker.trackEvent(ADB.Media.Event.BufferStart);
   };
   ```

1. Volg bij het verzenden van het volledige bericht over de buffer vanuit de mediaspeler het einde van de buffering met de gebeurtenis `BufferComplete` .

   ```js
   _onBufferComplete = function() {
       tracker.trackEvent(ADB.Media.Event.BufferComplete);
   };
   ```

Zie het volgende scenario [ playback van VOD met het als buffer optreden voor ](/help/use-cases/tracking-scenarios/vod-buffering.md) voor meer informatie.
