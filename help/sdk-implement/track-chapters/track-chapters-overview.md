---
title: Leer hoe te hoofdstukken en segmenten te volgen Verklaarde
description: Hoe te om hoofdstuk uit te voeren en segment het volgen met Media SDK.
uuid: 3fe32425-5e2a-4886-8fea-d91d15671bb0
exl-id: d213b633-be3b-4eb8-be71-0ef55e78a570
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 1%

---

# Overzicht{#overview}

De volgende instructies bieden richtlijnen voor implementatie met 2.x SDK&#39;s.

>[!IMPORTANT]
> 
> Als u een 1.x-versie van de SDK implementeert, kunt u de Developers Guide hier downloaden: [SDK&#39;s downloaden.](/help/sdk-implement/download-sdks.md)

Het hoofdstuk en het segment volgen is beschikbaar voor douane-bepaalde media hoofdstukken of segmenten. Bij het bijhouden van hoofdstukken wordt vaak gebruik gemaakt van aangepaste segmenten die zijn gebaseerd op media-inhoud (zoals honkbal-waarschuwingen), of van het definiëren van inhoudssegmenten tussen ad-hocafbrekingen. Het volgen van het hoofdstuk is **niet** vereist voor kernmedia het volgen implementaties.

Het volgen van het hoofdstuk omvat hoofdstukbegin, hoofdstuk voltooit, en hoofdstukoverslagen. U kunt de mediaspeler-API met aangepaste segmentatielogica gebruiken om hoofdstukgebeurtenissen te identificeren en de vereiste en optionele hoofdstukvariabelen te vullen.

## Gebeurtenissen van Player

### Bij starten van hoofdstuk

* Maak de instantie van het hoofdstukobject voor het hoofdstuk, `chapterObject`
* De hoofdstukmetagegevens invullen `chapterCustomMetadata`
* `trackEvent(MediaHeartbeat.Event.ChapterStart, chapterObject, chapterCustomMetadata);` aanroepen

### Bij hoofdstuk voltooid

* `trackEvent(MediaHeartbeat.Event.ChapterComplete);` aanroepen

### Bij overslaan van hoofdstuk

* `trackEvent(MediaHeartbeat.Event.ChapterSkip);` aanroepen

## Hoofdstuk bijhouden implementeren {#implement-chapter-tracking}

1. Identificeer wanneer de hoofdstukbegingebeurtenis voorkomt en creeer de `ChapterObject` instantie door de hoofdstukinformatie te gebruiken.

   Hier volgt de `ChapterObject` referentie voor hoofdstuktracking:

   >[!NOTE]
   >
   >Deze variabelen zijn alleen vereist als u hoofdstukken wilt bijhouden.

   | Naam variabele | Beschrijving | Vereist |
   | --- | --- | :---: |
   | `name` | Hoofdstuknaam | Ja |
   | `position` | Hoofdstukpositie | Ja |
   | `length` | Lengte van hoofdstuk | Ja |
   | `startTime` | Begintijd van hoofdstuk | Ja |

1. Als u aangepaste metagegevens voor het hoofdstuk opneemt, maakt u de variabelen voor contextgegevens voor de metagegevens.
1. Als u wilt beginnen met het afspelen van het hoofdstuk, roept u de gebeurtenis `ChapterStart` in de instantie `MediaHeartbeat` aan.
1. Wanneer de playback de hoofdstukeindgrens, zoals die door uw douanecode wordt bepaald bereikt, roep de `ChapterComplete` gebeurtenis in `MediaHeartbeat` instantie.
1. Als het afspelen van het hoofdstuk niet is voltooid omdat de gebruiker het hoofdstuk heeft overgeslagen (bijvoorbeeld als de gebruiker buiten de hoofdstukgrens zoekt), roept u de gebeurtenis `ChapterSkip` in de MediaHeartbeat-instantie aan.
1. Als er nog hoofdstukken zijn, herhaalt u stap 1 tot en met 5.

In de volgende voorbeeldcode wordt de JavaScript 2.x SDK gebruikt voor een HTML5-mediaspeler. Gebruik deze code met de afspeelcode voor de kernmedia.

```js
/* Call on chapter start */
if (e.type == "chapter start") {
    var chapterObject = MediaHeartbeat.createChapterObject("Inning 5",5,500,2500);
    /* Set custom context data*/
    var chapterCustomMetadata = {
        segmentType:"Baseball Innings",
        segmentName:"Inning 5",
        segmentInfo:"Game Six"
    }
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                                   chapterObject,  
                                   chapterCustomMetadata);
};

/* Call on chapter complete */
if (e.type == "chapter complete") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete);
};

/* Call on chapter skip */
if (e.type == "chapter skip") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip);
};
```
