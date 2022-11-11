---
title: Leer hoe te om Hoofdstuk en Segmenten op Roku te volgen
description: Leer over het uitvoeren van hoofdstuk en segment het volgen gebruikend Media SDK op Roku.
uuid: 15c07131-77d7-4a97-92c6-0a190c6b08d3
exl-id: b5eb8be7-4b85-4ba7-9216-dd691be7ba46
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 2%

---

# Hoofdstukken en segmenten bijhouden op Roku{#track-chapters-and-segments-on-roku}

De volgende instructies bieden richtlijnen voor implementatie met 2.x SDK&#39;s.

>[!IMPORTANT]
>
> Als u een 1.x-versie van de SDK implementeert, kunt u de Developers Guide hier downloaden: [SDK&#39;s downloaden.](/help/getting-started/download-sdks.md)

## Implementatiestandaard en metagegevens

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

1. Als u wilt beginnen met het afspelen van het hoofdstuk, roept u de `ChapterStart` in de `MediaHeartbeat` instantie:

   ```
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_START, chapterInfo, chapterContextData)
   ```

1. Wanneer de playback de hoofdstukeindgrens bereikt, zoals die door uw douanecode wordt bepaald, roep `ChapterComplete` in de `MediaHeartbeat` -instantie.

   ```
   chapterContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_COMPLETE, chapterInfo, chapterContextData)
   ```

1. Als het afspelen van het hoofdstuk niet is voltooid omdat de gebruiker het hoofdstuk heeft overgeslagen (bijvoorbeeld als de gebruiker buiten de hoofdstukgrens zoekt), roept u het dialoogvenster `ChapterSkip` in de MediaHeartbeat-instantie.

   ```
   chapterContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_SKIP, chapterInfo, chapterContextData)
   ```

1. Als er nog hoofdstukken zijn, herhaalt u stap 1 tot en met 5.
