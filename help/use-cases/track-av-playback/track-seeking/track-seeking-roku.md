---
title: Leer hoe u zoekopdrachten kunt bijhouden op Roku
description: Leer hoe u de gebeurtenissen Start en Voltooid zoeken bijhoudt met de Media SDK op Roku.
uuid: 0572252b-397f-4aa2-b4b5-c5346b75244a
exl-id: cb0581f7-3ced-4d46-ac6a-a309a179c21e
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---

# Zoeken volgen op Roku{#track-seeking-on-roku}

De volgende instructies bieden richtlijnen voor implementatie voor alle 2.x SDK&#39;s.

>[!IMPORTANT]
>
>Als u een 1.x-versie van de SDK implementeert, kunt u de 1.x-handleidingen voor ontwikkelaars hier downloaden: [SDK&#39;s downloaden.](/help/getting-started/download-sdks.md)

## Constanten voor reeksspatiëring zoeken

| Naam van constante | Beschrijving     |
|---|---|
| `SeekStart` | Constante voor het bijhouden van de gebeurtenis Start van zoekopdracht. |
| `SeekComplete` | Constante voor het bijhouden van de gebeurtenis Seek Complete. |

## Zoeken implementeren

1. Luister naar de afspeelzoekgebeurtenissen van de mediaspeler en volg bij het zoeken de zoekgebeurtenis op zoek naar de zoekfunctie `SeekStart` gebeurtenis.

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

Zie het volgende scenario [VOD afspelen met zoeken in de hoofdinhoud](/help/use-cases/tracking-scenarios/vod-seeking.md) voor meer informatie .
