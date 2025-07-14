---
title: Leer hoe te hoofdstukken en segmenten te volgen Verklaarde
description: Hoe te om hoofdstuk en segment het volgen met de Media SDK uit te voeren.
uuid: 3fe32425-5e2a-4886-8fea-d91d15671bb0
exl-id: d213b633-be3b-4eb8-be71-0ef55e78a570
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 1%

---

# Overzicht{#overview}

De volgende instructies bieden richtlijnen voor implementatie met 2.x SDK&#39;s.

>[!IMPORTANT]
> 
> Als u een versie 1.x van SDK uitvoert, kunt u de Gids van Ontwikkelaars hier downloaden: [ Download SDKs.](/help/getting-started/download-sdks.md)

Het hoofdstuk en het segment volgen is beschikbaar voor douane-bepaalde media hoofdstukken of segmenten. Bij het bijhouden van hoofdstukken wordt vaak gebruik gemaakt van aangepaste segmenten die zijn gebaseerd op media-inhoud (zoals honkbal-waarschuwingen), of van het definiëren van inhoudssegmenten tussen ad-hocafbrekingen. Het volgen van het hoofdstuk wordt **niet** vereist voor kernmedia volgende implementaties.

Het volgen van het hoofdstuk omvat hoofdstukbegin, hoofdstuk voltooit, en hoofdstukoverslagen. U kunt de mediaspeler-API met aangepaste segmentatielogica gebruiken om hoofdstukgebeurtenissen te identificeren en de vereiste en optionele hoofdstukvariabelen te vullen.

## Gebeurtenissen van Player

### Bij starten van hoofdstuk

* Maak de instantie van het hoofdstukobject voor het hoofdstuk, `chapterObject`
* De hoofdstukmetagegevens vullen, `chapterCustomMetadata`
* Roep `trackEvent(MediaHeartbeat.Event.ChapterStart, chapterObject, chapterCustomMetadata);`

### Bij hoofdstuk voltooid

* Roep `trackEvent(MediaHeartbeat.Event.ChapterComplete);`

### Bij overslaan van hoofdstuk

* Roep `trackEvent(MediaHeartbeat.Event.ChapterSkip);`

## Hoofdstuk bijhouden implementeren {#implement-chapter-tracking}

1. Bepaal wanneer de hoofdstukstartgebeurtenis plaatsvindt en maak de `ChapterObject` -instantie met behulp van de hoofdstukinformatie.

   Hier volgt de naslaggids voor hoofdstuk `ChapterObject` :

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
1. Roep de gebeurtenis `ChapterStart` in de `MediaHeartbeat` -instantie aan om het afspelen van het hoofdstuk te starten.
1. Wanneer het afspelen de eindgrens van het hoofdstuk bereikt, zoals gedefinieerd door uw aangepaste code, roept u de gebeurtenis `ChapterComplete` in de instantie `MediaHeartbeat` aan.
1. Als het afspelen van het hoofdstuk niet is voltooid omdat de gebruiker het hoofdstuk heeft overgeslagen (bijvoorbeeld als de gebruiker buiten de hoofdstukgrens zoekt), roept u de gebeurtenis `ChapterSkip` in de MediaHeartbeat-instantie aan.
1. Als er nog hoofdstukken zijn, herhaalt u stap 1 tot en met 5.

In de volgende voorbeeldcode wordt de JavaScript 2.x SDK voor een HTML5-mediaspeler gebruikt. Gebruik deze code met de afspeelcode voor de kernmedia.

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
