---
title: Zoeken bijhouden met JavaScript 3.x
description: In dit onderwerp wordt het implementeren van 'seek tracking' beschreven met behulp van de Media SDK in browser-apps (JS).
translation-type: tm+mt
source-git-commit: 318bb60d9835d9a07fb7aa0a0a02162248410d09
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# Zoeken bijhouden met JavaScript 3.x{#track-seeking-on-javascript}

>[!IMPORTANT]
>
>De volgende instructies bieden richtlijnen voor implementatie voor alle 3.x SDK&#39;s. Als u eerdere versies van de SDK implementeert, kunt u de ontwikkelaarsgidsen hier downloaden: [SDK&#39;s downloaden.](/help/sdk-implement/download-sdks.md)

## Constanten voor reeksspatiëring zoeken

| Naam van constante | Beschrijving     |
|---|---|
| `SeekStart` | Constante voor het bijhouden van de gebeurtenis Start van zoekopdracht. |
| `SeekComplete` | Constante voor het bijhouden van de gebeurtenis Seek Complete. |

## Zoeken implementeren

1. Luister naar het afspelen en zoeken van gebeurtenissen van de mediaspeler en volg zoekacties bij het starten van de gebeurtenis via de `SeekStart` gebeurtenis:

   ```js
   _onSeekStart = function() {
       tracker.trackEvent(ADB.Media.Event.SeekStart);
   };
   ```

1. Volg bij het zoeken naar volledige meldingen van de mediaspeler het einde van het zoeken met behulp van de `SeekComplete` gebeurtenis:

   ```js
   _onSeekComplete = function() {
       tracker.trackEvent(ADB.Media.Event.SeekComplete);
   };
   ```

Zie het volgende scenario [VOD playback met het zoeken in de belangrijkste inhoud](/help/sdk-implement/tracking-scenarios/vod-seeking.md) voor meer informatie.
