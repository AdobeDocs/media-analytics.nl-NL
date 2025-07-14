---
title: Leer hoe te om Hoofdstuk en Segmenten op Chromecast te volgen
description: Leer over het uitvoeren van hoofdstuk en segment het volgen gebruikend Media SDK op Chromecast.
uuid: 5ea562b9-0e07-4fbb-9a3b-213d746304f5
exl-id: 26b71e4d-ced7-49cb-a838-2b1c8d4ee4de
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 2%

---

# De hoofdstukken van het spoor en de segmenten op Chromecast{#track-chapters-and-segments-on-chromecast}

De volgende instructies bieden richtlijnen voor implementatie met 2.x SDK&#39;s.

>[!IMPORTANT]
>
> Als u een versie 1.x van SDK uitvoert, kunt u de Gids van Ontwikkelaars hier downloaden: [ Download SDKs.](/help/getting-started/download-sdks.md)

1. Bepaal wanneer de hoofdstukstartgebeurtenis plaatsvindt en maak de `ChapterObject` -instantie met behulp van de hoofdstukinformatie.

   `ChapterObject` referentie voor het bijhouden van hoofdstukken:

   >[!NOTE]
   >
   >Deze variabelen zijn alleen vereist als u hoofdstukken wilt bijhouden.

   | Naam variabele | Beschrijving | Vereist |
   | --- | --- | :---: |
   | `name` | Hoofdstuknaam | Ja |
   | `position` | Hoofdstukpositie | Ja |
   | `length` | Lengte van hoofdstuk | Ja |
   | `startTime` | Begintijd van hoofdstuk | Ja |

   Hoofdstukvoorwerp: [ createChapterObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createChapterObject)

   ```js
   chapterInfo = ADBMobile.media.createChapterObject("First Chapter", 1, CHAPTER1_LENGTH, CHAPTER1_START_POS);
   ```

1. Als u aangepaste metagegevens voor het hoofdstuk opneemt, maakt u de variabelen voor contextgegevens voor de metagegevens:

   ```js
   var chapterContextData = {
       segmentType: "Sample segment type"
   };
   ```

1. Beginnen het hoofdstukplayback te volgen, volg de `ChapterStart` gebeurtenis: [ trackEvent ](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterStart, ChapterInfo, chapterContextData);
   ```

1. Wanneer de playback de hoofdstukeindgrens bereikt, zoals die door uw douanecode wordt bepaald, roep de `ChapterComplete` gebeurtenis in de `MediaHeartbeat` instantie: [ trackEvent ](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterComplete);
   ```

1. Als de hoofdstukplayback niet voltooide omdat de gebruiker verkoos om het hoofdstuk over te slaan (bijvoorbeeld, als de gebruiker uit de hoofdstukgrens) zoekt, spoor de `ChapterSkip` gebeurtenis: [ trackEvent ](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterSkip);
   ```

1. Als er nog hoofdstukken zijn, herhaalt u stap 1 tot en met 5.
