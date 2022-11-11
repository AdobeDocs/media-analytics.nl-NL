---
title: Leer hoe u hoofdstukken en segmenten kunt bijhouden op iOS
description: Leer over het uitvoeren van hoofdstuk en segment het volgen gebruikend Media SDK op iOS.
uuid: ffc5ce9f-04ba-4059-92d4-4cb4180ac9ed
exl-id: ea8a1dd6-043f-41a4-9cef-845da92bfa32
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 2%

---

# Hoofdstukken en segmenten bijhouden op iOS{#track-chapters-and-segments-on-ios}

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

   Object Chapter:

   ```
   id chapterObject =  
     [ADBMediaHeartbeat createChapterObjectWithName:[CHAPTER_NAME]
                        position:[POSITION]
                        length:[LENGTH]
                        startTime:[START_TIME]];
   ```

1. Als u aangepaste metagegevens voor het hoofdstuk opneemt, maakt u de variabelen voor contextgegevens voor de metagegevens:

   ```
   NSMutableDictionary *chapterDictionary = [[NSMutableDictionary alloc] init];
   [chapterDictionary setObject:@"Sample segment type" forKey:@"segmentType"];
   [chapterDictionary setObject:@"Sample segment name" forKey:@"segmentName"];
   [chapterDictionary setObject:@"Sample segment info" forKey:@"segmentInfo"];
   ```

1. Als u wilt beginnen met het afspelen van het hoofdstuk, roept u de `ChapterStart` in de `MediaHeartbeat` instantie:

   ```
   - (void)onChapterStart:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterStart  
                        mediaObject:chapterObject     
                        data:chapterDictionary];
   }
   ```

1. Wanneer de playback de hoofdstukeindgrens bereikt, zoals die door uw douanecode wordt bepaald, roep `ChapterComplete` in de `MediaHeartbeat` instantie:

   ```
   - (void)onChapterComplete:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterComplete  
                        mediaObject:nil  
                        data:nil];
   }
   ```

1. Als het afspelen van het hoofdstuk niet is voltooid omdat de gebruiker het hoofdstuk heeft overgeslagen (bijvoorbeeld als de gebruiker buiten de hoofdstukgrens zoekt), roept u het dialoogvenster `ChapterSkip` -gebeurtenis in de MediaHeartbeat-instantie:

   ```
   - (void)onChapterSkip:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterSkip  
                        mediaObject:nil  
                        data:nil];
   }
   ```

1. Als er nog hoofdstukken zijn, herhaalt u stap 1 tot en met 5.
