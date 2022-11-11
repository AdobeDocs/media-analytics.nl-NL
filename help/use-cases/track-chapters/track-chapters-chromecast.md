---
title: Leer hoe te om Hoofdstuk en Segmenten op Chromecast te volgen
description: Leer over het uitvoeren van hoofdstuk en segment het volgen gebruikend Media SDK op Chromecast.
uuid: 5ea562b9-0e07-4fbb-9a3b-213d746304f5
exl-id: 26b71e4d-ced7-49cb-a838-2b1c8d4ee4de
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 2%

---

# Hoofdstukken en segmenten bijhouden op Chromecast{#track-chapters-and-segments-on-chromecast}

De volgende instructies bieden richtlijnen voor implementatie met 2.x SDK&#39;s.

>[!IMPORTANT]
>
> Als u een 1.x-versie van de SDK implementeert, kunt u de Developers Guide hier downloaden: [SDK&#39;s downloaden.](/help/getting-started/download-sdks.md)

1. Identificeer wanneer de hoofdstukbegingebeurtenis voorkomt en creeer `ChapterObject` door de hoofdstukinformatie te gebruiken.

   `ChapterObject` hoofdstuk volgende verwijzing:

   >[!NOTE]
   >
   >Deze variabelen zijn alleen vereist als u hoofdstukken wilt bijhouden.

   | Naam variabele | Beschrijving | Vereist |
   | --- | --- | :---: |
   | `name` | Hoofdstuknaam | Ja |
   | `position` | Hoofdstukpositie | Ja |
   | `length` | Lengte van hoofdstuk | Ja |
   | `startTime` | Begintijd van hoofdstuk | Ja |

   Object Chapter: [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createChapterObject)

   ```js
   chapterInfo = ADBMobile.media.createChapterObject("First Chapter", 1, CHAPTER1_LENGTH, CHAPTER1_START_POS);
   ```

1. Als u aangepaste metagegevens voor het hoofdstuk opneemt, maakt u de variabelen voor contextgegevens voor de metagegevens:

   ```js
   var chapterContextData = {
       segmentType: "Sample segment type"
   };
   ```

1. Als u wilt beginnen met het afspelen van het hoofdstuk, volgt u de `ChapterStart` gebeurtenis: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterStart, ChapterInfo, chapterContextData);
   ```

1. Wanneer de playback de hoofdstukeindgrens bereikt, zoals die door uw douanecode wordt bepaald, roep `ChapterComplete` in de `MediaHeartbeat` instantie: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterComplete);
   ```

1. Als het afspelen van het hoofdstuk niet is voltooid omdat de gebruiker het hoofdstuk heeft overgeslagen (bijvoorbeeld als de gebruiker buiten de hoofdstukgrens zoekt), moet u het volgende bijhouden `ChapterSkip` gebeurtenis: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterSkip);
   ```

1. Als er nog hoofdstukken zijn, herhaalt u stap 1 tot en met 5.
