---
title: Leer hoe te om Hoofdstuk en Segmenten op Chromecast te volgen
description: Leer over het uitvoeren van hoofdstuk en segment het volgen gebruikend Media SDK op Chromecast.
uuid: 5ea562b9-0e07-4fbb-9a3b-213d746304f5
exl-id: 26b71e4d-ced7-49cb-a838-2b1c8d4ee4de
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 2%

---

# Hoofdstukken en segmenten bijhouden op Chromecast{#track-chapters-and-segments-on-chromecast}

>[!IMPORTANT]
>
>De volgende instructies bieden richtlijnen voor implementatie met 2.x SDK&#39;s. Als u een 1.x-versie van de SDK implementeert, kunt u de Developers Guide hier downloaden: [SDK&#39;s downloaden.](/help/sdk-implement/download-sdks.md)

1. Identificeer wanneer de hoofdstukbegingebeurtenis voorkomt en creeer de `ChapterObject` instantie door de hoofdstukinformatie te gebruiken.

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

1. Volg de gebeurtenis `ChapterStart` om het afspelen van het hoofdstuk te starten: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterStart, ChapterInfo, chapterContextData); 
   ```

1. Wanneer de playback de hoofdstukeindgrens, zoals die door uw douanecode wordt bepaald bereikt, roep de `ChapterComplete` gebeurtenis in `MediaHeartbeat` instantie: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterComplete);
   ```

1. Als het afspelen van het hoofdstuk niet is voltooid omdat de gebruiker het hoofdstuk heeft overgeslagen (bijvoorbeeld als de gebruiker buiten de hoofdstukgrens zoekt), moet u de gebeurtenis `ChapterSkip` volgen: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterSkip); 
   ```

1. Als er nog hoofdstukken zijn, herhaalt u stap 1 tot en met 5.
