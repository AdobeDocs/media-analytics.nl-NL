---
title: Leer hoe u zoekopdrachten kunt bijhouden met JavaScript 2.x
description: Leer hoe u de gebeurtenissen Start en Voltooien zoeken bijhoudt met de Media SDK in browser-apps (JS 2.x).
uuid: 089947fb-8bae-4ae8-b215-53793620efd7
exl-id: 90f35376-24d8-405d-82b4-d6b737acf7b9
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# Zoeken bijhouden met JavaScript 2.x{#track-seeking-on-javascript}

De volgende instructies bieden richtlijnen voor implementatie voor alle 2.x SDK&#39;s.

>[!IMPORTANT]
>
>Als u een 1.x-versie van de SDK implementeert, kunt u de 1.x-handleidingen voor ontwikkelaars hier downloaden: [SDK&#39;s downloaden.](/help/sdk-implement/download-sdks.md)

## Constanten voor reeksspatiëring zoeken

| Naam van constante | Beschrijving     |
|---|---|
| `SeekStart` | Constante voor het bijhouden van de gebeurtenis Start van zoekopdracht. |
| `SeekComplete` | Constante voor het bijhouden van de gebeurtenis Seek Complete. |

## Zoeken implementeren

1. Luister naar het afspelen van zoekgebeurtenissen van de mediaspeler en volg het zoeken naar de gebeurtenis `SeekStart` bij het starten van de zoekgebeurtenis:

   ```js
   _onSeekStart = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart);
   };
   ```

1. Volg bij het zoeken naar volledige meldingen van de mediaspeler het einde van het zoeken met de gebeurtenis `SeekComplete`:

   ```js
   _onSeekComplete = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete);
   };
   ```

Zie het volgende scenario [VOD playback met het zoeken in de belangrijkste inhoud](/help/sdk-implement/tracking-scenarios/vod-seeking.md) voor meer informatie.
