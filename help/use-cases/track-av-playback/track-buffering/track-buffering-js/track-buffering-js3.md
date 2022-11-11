---
title: Leer hoe u buffering kunt bijhouden met JavaScript 3.x
description: Leer hoe u buffergebeurtenissen kunt bijhouden in browser-apps (JS).
exl-id: c6941942-02f9-4f9c-99ad-0c52ed2f793b
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# buffering bijhouden met JavaScript 3.x{#track-buffering-on-javascript}

De volgende instructies bieden richtlijnen voor implementatie voor alle 3.x SDK&#39;s.

>[!IMPORTANT]
>
>Als u eerdere versies van de SDK implementeert, kunt u de ontwikkelaarsgidsen hier downloaden: [SDK&#39;s downloaden.](/help/getting-started/download-sdks.md)

## Constanten voor bufferspatiëring

| Naam van constante | Beschrijving     |
|---|---|
| `BufferStart` | Constante voor het bijhouden van de bufferstartgebeurtenis |
| `BufferComplete` | Constante voor het bijhouden van de gebeurtenis Buffer Complete |

## Buffering implementeren

1. Luister naar de buffergebeurtenissen voor het afspelen vanaf de mediaspeler en volg bij een melding van een bufferstart de buffering met de knop `BufferStart` gebeurtenis.

   ```js
   _onBufferStart = function() {
       tracker.trackEvent(ADB.Media.Event.BufferStart);
   };
   ```

1. Volg bij het verzenden van het volledige bericht over de buffer vanuit de mediaspeler het einde van de buffering met de `BufferComplete` gebeurtenis.

   ```js
   _onBufferComplete = function() {
       tracker.trackEvent(ADB.Media.Event.BufferComplete);
   };
   ```

Zie het volgende scenario [VOD afspelen met bufferen](/help/use-cases/tracking-scenarios/vod-buffering.md) voor meer informatie .
