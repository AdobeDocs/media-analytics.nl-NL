---
title: Leer hoe u zoeken kunt bijhouden op Chromecast
description: Leer hoe u de gebeurtenissen Start en Voltooid zoeken kunt bijhouden met Media SDK on Chromecast.
uuid: 8018e6c4-fed9-4de7-9eae-c720da55ad8c
exl-id: 03be8ed3-ae3a-4e9a-b667-0d9280a844a1
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---

# Zoeken volgen op chroecast{#track-seeking-on-chromecast}

De volgende instructies bieden richtlijnen voor implementatie voor alle 2.x SDK&#39;s.

>[!IMPORTANT]
>
>Als u een 1.x versie van SDK uitvoert, kunt u de 1.x Gidsen van Ontwikkelaars hier downloaden: [ Download SDKs.](/help/getting-started/download-sdks.md)

## Constanten voor bijhouden zoeken

| Naam van constante | Beschrijving     |
|---|---|
| `SeekStart` | Constante voor het bijhouden van de gebeurtenis Start van zoekopdracht. |
| `SeekComplete` | Constante voor het bijhouden van de gebeurtenis Seek Complete. |

## Zoeken implementeren

1. Luister naar de playback die gebeurtenissen van de media speler zoeken, en op zoek begin gebeurtenis bericht, spoor die de `SeekStart` gebeurtenis gebruiken: [ trackEvent ](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.SeekStart);
   ```

1. Op zoek volledig bericht van de media speler, spoor het eind van het zoeken gebruikend de `SeekComplete` gebeurtenis: [ trackEvent ](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.SeekComplete);
   ```

Zie het volgende scenario [ de playback van VOD met het zoeken in de belangrijkste inhoud ](/help/use-cases/tracking-scenarios/vod-seeking.md) voor meer informatie.
