---
title: Hoofdstukken en segmenten bijhouden met JavaScript 3.x
description: In dit onderwerp wordt beschreven hoe u hoofdstuk- en segmenttracering implementeert met de Media SDK in browser-apps (JS).
translation-type: tm+mt
source-git-commit: b14b56aea4a1821a2a160b9cd301cd181f1ba8dd
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# Hoofdstukken en segmenten bijhouden met JavaScript 3.x{#track-chapters-and-segments-on-javascript}

>[!IMPORTANT]
>
>De volgende instructies bieden richtlijnen voor implementatie met 3.x SDK&#39;s. Als u eerdere versies van de SDK implementeert, kunt u de Developers Guide hier downloaden: [SDK&#39;s downloaden.](/help/sdk-implement/download-sdks.md)

1. Identificeer wanneer de hoofdstukbegingebeurtenis voorkomt en creeer de `ChapterObject` instantie door de hoofdstukinformatie te gebruiken.

   `ChapterObject` hoofdstuk volgende verwijzing:

   >[!NOTE]
   >
   >Deze variabelen zijn alleen vereist als u hoofdstukken wilt bijhouden.

   | Naam variabele | Type | Beschrijving |
   | --- | --- | --- |
   | `name` | string | Niet-lege tekenreeks die hoofdstuknaam aangeeft. |
   | `position` | getal | De positie van het hoofdstuk binnen de inhoud, te beginnen met 1. |
   | `length` | getal | Positief getal dat de lengte van het hoofdstuk aangeeft. |
   | `startTime` | getal | Waarde afspeelkop aan begin van hoofdstuk. |

   Object Chapter:

   ```js
   var chapterObject =
     ADB.Media.createChapterObject.createChapterObject(<CHAPTER_NAME>,
                                        <POSITION>,
                                        <LENGTH>,
                                        <START_TIME>);
   ```

1. Als u aangepaste metagegevens voor het hoofdstuk opneemt, maakt u de variabelen voor contextgegevens voor de metagegevens:

   ```js
   var chapterMetadata = {};
   chapterMetadata["segmentType"] = "Sample segment type";
   ```

1. Als u wilt beginnen met het afspelen van het hoofdstuk, roept u de `ChapterStart` gebeurtenis in de `MediaHeartbeat` instantie aan:

   ```js
   _onChapterStart = function() {
     tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterObject, chapterMetadata);
   
   };
   ```

1. Wanneer de playback de hoofdstukeindgrens bereikt, zoals die door uw douanecode wordt bepaald, roep de `ChapterComplete` gebeurtenis in de `MediaHeartbeat` instantie:

   ```js
   _onChapterComplete = function() {
      tracker.trackEvent(ADB.Media.Event.ChapterComplete);
   };
   ```

1. Als het afspelen van het hoofdstuk niet is voltooid omdat de gebruiker het hoofdstuk heeft overgeslagen (bijvoorbeeld als de gebruiker buiten de hoofdstukgrens zoekt), roept u de `ChapterSkip` gebeurtenis op in de MediaHeartbeat-instantie:

   ```js
   _onChapterSkip = function() {
       tracker.trackEvent(ADB.Media.Event.ChapterSkip);
   };
   ```

1. Als er nog hoofdstukken zijn, herhaalt u stap 1 tot en met 5.
