---
title: Leer hoe te om Hoofdstuk en Segmenten op Roku te volgen
description: Leer over het uitvoeren van hoofdstuk en segment het volgen gebruikend Media SDK op Roku.
uuid: 15c07131-77d7-4a97-92c6-0a190c6b08d3
exl-id: b5eb8be7-4b85-4ba7-9216-dd691be7ba46
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 2%

---

# Hoofdstukken en segmenten bijhouden op Roku{#track-chapters-and-segments-on-roku}

De volgende instructies bieden richtlijnen voor implementatie met 2.x SDK&#39;s.

>[!IMPORTANT]
>
> Als u een versie 1.x van SDK uitvoert, kunt u de Gids van Ontwikkelaars hier downloaden: [&#x200B; Download SDKs.](/help/getting-started/download-sdks.md)

## Standaardinstellingen en metagegevens implementeren

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

   Object Chapter:

   ```
   chapterInfo =  
     adb_media_init_chapterinfo(<CHAPTER_NAME>,  
                                <POSITION>,  
                                <LENGTH>,  
                                <START_TIME>);)
   ```

1. Als u aangepaste metagegevens voor het hoofdstuk opneemt, maakt u de variabelen voor contextgegevens voor de metagegevens:

   ```
   chapterContextData = {}
   chapterContextData["seg_type"] = "seg_type"
   chapterContextData["seg_name"] = "seg_name"
   chapterContextData["seg_info"] = "seg_info"
   ```

1. Roep de gebeurtenis `ChapterStart` in de `MediaHeartbeat` -instantie aan om het afspelen van het hoofdstuk te starten:

   ```
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_START, chapterInfo, chapterContextData)
   ```

1. Wanneer het afspelen de eindgrens van het hoofdstuk bereikt, zoals gedefinieerd door uw aangepaste code, roept u de gebeurtenis `ChapterComplete` in de instantie `MediaHeartbeat` aan.

   ```
   chapterContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_COMPLETE, chapterInfo, chapterContextData)
   ```

1. Als het afspelen van het hoofdstuk niet is voltooid omdat de gebruiker het hoofdstuk heeft overgeslagen (bijvoorbeeld als de gebruiker buiten de hoofdstukgrens zoekt), roept u de gebeurtenis `ChapterSkip` in de MediaHeartbeat-instantie aan.

   ```
   chapterContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_SKIP, chapterInfo, chapterContextData)
   ```

1. Als er nog hoofdstukken zijn, herhaalt u stap 1 tot en met 5.
