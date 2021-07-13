---
title: Leer hoe u zoekopdrachten kunt bijhouden met JavaScript 3.x
description: Leer hoe u de gebeurtenissen Start en Voltooien zoeken bijhoudt met de Media SDK in browser-apps (JS 3.x).
exl-id: b7152436-520e-4f38-a8ad-1027ca3f1f6c
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '136'
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

1. Luister naar het afspelen van zoekgebeurtenissen van de mediaspeler en volg het zoeken naar de gebeurtenis `SeekStart` bij het starten van de zoekgebeurtenis:

   ```js
   _onSeekStart = function() {
       tracker.trackEvent(ADB.Media.Event.SeekStart);
   };
   ```

1. Volg bij het zoeken naar volledige meldingen van de mediaspeler het einde van het zoeken met de gebeurtenis `SeekComplete`:

   ```js
   _onSeekComplete = function() {
       tracker.trackEvent(ADB.Media.Event.SeekComplete);
   };
   ```

Zie het volgende scenario [VOD playback met het zoeken in de belangrijkste inhoud](/help/sdk-implement/tracking-scenarios/vod-seeking.md) voor meer informatie.
