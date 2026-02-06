---
title: Leer hoofdstukken en segmenten bij te houden met JavaScript 3.x
description: Leer hoe u hoofdstuk- en segmenttracering implementeert met de Media SDK in browser-apps (JS).
exl-id: 00ba11df-d226-45a2-a561-dc9f15dcf714
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# Hoofdstukken en segmenten bijhouden met JavaScript 3.x{#track-chapters-and-segments-on-javascript}

De volgende instructies bieden richtlijnen voor implementatie met 3.x SDK&#39;s.

>[!IMPORTANT]
>
> Als u om het even welke vorige versies van SDK uitvoert, kunt u de Gids van Ontwikkelaars hier downloaden: [ Download SDKs.](/help/getting-started/download-sdks.md)

1. Bepaal wanneer de hoofdstukstartgebeurtenis plaatsvindt en maak de `ChapterObject` -instantie met behulp van de hoofdstukinformatie.

   `ChapterObject` referentie voor het bijhouden van hoofdstukken:

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

1. Roep de gebeurtenis `ChapterStart` in de `MediaHeartbeat` -instantie aan om het afspelen van het hoofdstuk te starten:

   ```js
   _onChapterStart = function() {
     tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterObject, chapterMetadata);
   
   };
   ```

1. Wanneer het afspelen de eindgrens van het hoofdstuk bereikt, zoals gedefinieerd door uw aangepaste code, roept u de gebeurtenis `ChapterComplete` op in de instantie `MediaHeartbeat` :

   ```js
   _onChapterComplete = function() {
      tracker.trackEvent(ADB.Media.Event.ChapterComplete);
   };
   ```

1. Als het afspelen van het hoofdstuk niet is voltooid omdat de gebruiker het hoofdstuk heeft overgeslagen (bijvoorbeeld als de gebruiker buiten de hoofdstukgrens zoekt), roept u de gebeurtenis `ChapterSkip` in de MediaHeartbeat-instantie aan:

   ```js
   _onChapterSkip = function() {
       tracker.trackEvent(ADB.Media.Event.ChapterSkip);
   };
   ```

1. Als er nog hoofdstukken zijn, herhaalt u stap 1 tot en met 5.
