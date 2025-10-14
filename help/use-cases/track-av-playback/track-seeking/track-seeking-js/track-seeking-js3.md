---
title: Leer hoe u zoekopdrachten kunt bijhouden met JavaScript 3.x
description: Leer hoe u de gebeurtenissen Start en Voltooien zoeken kunt bijhouden met Media SDK in browser-apps (JS 3.x).
exl-id: b7152436-520e-4f38-a8ad-1027ca3f1f6c
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---

# Zoeken bijhouden met JavaScript 3.x{#track-seeking-on-javascript}

De volgende instructies bieden richtlijnen voor implementatie voor alle 3.x SDK&#39;s.

>[!IMPORTANT]
>
>Als u om het even welke vorige versies van SDK uitvoert, kunt u de Gidsen van Ontwikkelaars hier downloaden: [&#x200B; Download SDKs.](/help/getting-started/download-sdks.md)

## Constanten voor bijhouden zoeken

| Naam van constante | Beschrijving     |
|---|---|
| `SeekStart` | Constante voor het bijhouden van de gebeurtenis Start van zoekopdracht. |
| `SeekComplete` | Constante voor het bijhouden van de gebeurtenis Seek Complete. |

## Zoeken implementeren

1. Luister naar het afspelen van zoekgebeurtenissen van de mediaspeler en volg zoekacties bij het zoeken naar gebeurtenissen via de gebeurtenis `SeekStart` :

   ```js
   _onSeekStart = function() {
       tracker.trackEvent(ADB.Media.Event.SeekStart);
   };
   ```

1. Volg bij het zoeken naar volledige meldingen van de mediaspeler het einde van het zoeken met de gebeurtenis `SeekComplete` :

   ```js
   _onSeekComplete = function() {
       tracker.trackEvent(ADB.Media.Event.SeekComplete);
   };
   ```

Zie het volgende scenario [&#x200B; de playback van VOD met het zoeken in de belangrijkste inhoud &#x200B;](/help/use-cases/tracking-scenarios/vod-seeking.md) voor meer informatie.
