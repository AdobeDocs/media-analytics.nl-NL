---
title: Leer hoe u zoekopdrachten kunt bijhouden met JavaScript 3.x
description: Leer hoe u de gebeurtenissen Start en Voltooien zoeken bijhoudt met de Media SDK in browser-apps (JS 3.x).
exl-id: b7152436-520e-4f38-a8ad-1027ca3f1f6c
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---

# Zoeken bijhouden met JavaScript 3.x{#track-seeking-on-javascript}

De volgende instructies bieden richtlijnen voor implementatie voor alle 3.x SDK&#39;s.

>[!IMPORTANT]
>
>Als u eerdere versies van de SDK implementeert, kunt u de ontwikkelaarsgidsen hier downloaden: [SDK&#39;s downloaden.](/help/getting-started/download-sdks.md)

## Constanten voor reeksspatiëring zoeken

| Naam van constante | Beschrijving     |
|---|---|
| `SeekStart` | Constante voor het bijhouden van de gebeurtenis Start van zoekopdracht. |
| `SeekComplete` | Constante voor het bijhouden van de gebeurtenis Seek Complete. |

## Zoeken implementeren

1. Luister naar de afspeelzoekgebeurtenissen van de mediaspeler en volg bij het zoeken de zoekgebeurtenis op zoek naar de zoekfunctie `SeekStart` gebeurtenis:

   ```js
   _onSeekStart = function() {
       tracker.trackEvent(ADB.Media.Event.SeekStart);
   };
   ```

1. Volg bij het zoeken naar volledige meldingen van de mediaspeler het einde van het zoeken met de `SeekComplete` gebeurtenis:

   ```js
   _onSeekComplete = function() {
       tracker.trackEvent(ADB.Media.Event.SeekComplete);
   };
   ```

Zie het volgende scenario [VOD afspelen met zoeken in de hoofdinhoud](/help/use-cases/tracking-scenarios/vod-seeking.md) voor meer informatie .
