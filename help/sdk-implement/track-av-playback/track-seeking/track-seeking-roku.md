---
title: Zoeken volgen op Roku
description: In dit onderwerp wordt het implementeren van 'seek tracking' beschreven met de Media SDK op Roku.
uuid: 0572252b-397f-4aa2-b4b5-c5346b75244a
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Zoeken volgen op Roku{#track-seeking-on-roku}

>[!IMPORTANT]
>
>De volgende instructies bieden richtlijnen voor implementatie voor alle 2.x SDK&#39;s. Als u een 1.x-versie van de SDK implementeert, kunt u de 1.x-handleidingen voor ontwikkelaars hier downloaden: SDK&#39;s [downloaden.](/help/sdk-implement/download-sdks.md)

## Constanten voor reeksspatiëring zoeken

| Naam van constante | Beschrijving |
|---|---|
| `SeekStart` | Constante voor het bijhouden van de gebeurtenis Start van zoekopdracht. |
| `SeekComplete` | Constante voor het bijhouden van de gebeurtenis Seek Complete. |

## Zoeken implementeren

1. Luister naar het afspelen van zoekgebeurtenissen van de mediaspeler en volg zoekacties bij het zoeken naar gebeurtenissen via de `SeekStart` gebeurtenis.

   ```
   seekContextData = {}
   seekContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_SEEK_START, seekInfo, seekContextData)
   ```

1. Volg bij het zoeken naar volledige meldingen van de mediaspeler het einde van het zoeken met de `SeekComplete` gebeurtenis.

   ```
   seekContextData = {}
   seekContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_SEEK_COMPLETE, seekInfo, seekContextData)
   ```

Zie het volgende scenario [VOD playback met het zoeken in de belangrijkste inhoud](/help/sdk-implement/tracking-scenarios/vod-seeking.md) voor meer informatie.
