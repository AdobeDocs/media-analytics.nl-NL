---
title: Leer hoe u buffering kunt bijhouden met JavaScript 2.x
description: Leer hoe u buffergebeurtenissen kunt bijhouden in browser-apps (JS).
uuid: c380cf2c-7729-4d4a-a4da-581bd94a5896
exl-id: 62c1d5b4-2717-42b3-8343-d41e895a9da3
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# buffering bijhouden met JavaScript 2.x{#track-buffering-on-javascript}

De volgende instructies bieden richtlijnen voor implementatie voor alle 2.x SDK&#39;s.

>[!IMPORTANT]
>
>Als u een 1.x-versie van de SDK implementeert, kunt u de 1.x-handleidingen voor ontwikkelaars hier downloaden: [SDK&#39;s downloaden.](/help/getting-started/download-sdks.md)

## Constanten voor bufferspatiëring

| Naam van constante | Beschrijving     |
|---|---|
| `BufferStart` | Constante voor het bijhouden van de bufferstartgebeurtenis |
| `BufferComplete` | Constante voor het bijhouden van de gebeurtenis Buffer Complete |

## Buffering implementeren

1. Luister naar de buffergebeurtenissen voor het afspelen vanaf de mediaspeler en volg bij een melding van een bufferstart de buffering met de knop `BufferStart` gebeurtenis.

   ```js
   _onBufferStart = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart);
   };
   ```

1. Volg bij het verzenden van het volledige bericht over de buffer vanuit de mediaspeler het einde van de buffering met de `BufferComplete` gebeurtenis.

   ```js
   _onBufferComplete = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete);
   };
   ```

Zie het volgende scenario [VOD afspelen met bufferen](/help/use-cases/tracking-scenarios/vod-buffering.md) voor meer informatie .
