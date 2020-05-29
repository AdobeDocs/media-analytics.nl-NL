---
title: Uitvoering en verslaglegging
description: In dit onderwerp wordt beschreven hoe u de functie voor het bijhouden van de spelerstatus kunt implementeren, inclusief.
translation-type: tm+mt
source-git-commit: 614780a121eac6d5f822d439365fa59f85959ce2
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# Uitvoering en verslaglegging

Tijdens een afspeelsessie moet elke statusinstantie (begin tot eind) afzonderlijk worden bijgehouden. De Media SDK en de Media Collection API verstrekken nieuwe het volgen methodes voor dit vermogen.

De Media SDK bevat twee nieuwe methoden voor het bijhouden van aangepaste statussen:

`trackStateStart("state_name")`

`trackStateClose("state_name")`


De Media Collection API omvat twee nieuwe gebeurtenissen die `media.stateName` als vereiste parameter hebben:

`stateStart` en `stateEnd`

## Media SDK-implementatie

Status speler start

```
// StateStart (ex: Mute is switched on)
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
tracker.trackEvent(ADB.Media.Event.StateStart, stateObject);
```

Status van speler eindigt op

```
// StateEnd (ex: Mute is switched off)
tracker.trackEvent(ADB.Media.Event.StateEnd, stateObject);
```


## API-implementatie voor mediaverzameling

Status speler start

```
// StateStart (ex: Mute is switched on)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "stateStart",
  "params": {
    "media.state.name": "mute"
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

Status van speler eindigt op

```
// StateEnd (ex: Mute is switched off)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events

{
  "eventType": "stateEnd",
  "params": {
    "media.state.name": "mute"
  },
  "playerTime": {
    "playhead": 600,
    "ts": 1569999730638
  }
}
```

## Statusmetriek

De meetgegevens die voor elk afzonderlijk frame worden verstrekt, worden als Context Data-parameters berekend en doorgegeven aan Adobe Analytics en voor rapportagedoeleinden opgeslagen. Er zijn drie cijfers beschikbaar voor elk frame:

* `a.media.states.[state.name].set = true` — Ingesteld op true als de status ten minste eenmaal is ingesteld voor elke specifieke weergave van een stream.
* `a.media.states.[state.name].count = 4` — Identificeert het aantal instanties van een status tijdens elke afzonderlijke afspeelbewerking van een stream.
* `a.media.states.[state.name].time = 240` — Geeft de totale frameduur aan in seconden per afzonderlijke afspeelbewerking van een stream.

## Rapportage

Alle metriek van de spelerstaat kan voor om het even welke rapporteringsvisualisatie worden gebruikt beschikbaar in de Werkruimte van de Analyse of een component (segment, berekende metriek) zodra een rapportreeks voor het volgen van de spelerstaat wordt toegelaten. De nieuwe metriek zou van de Console Admin voor elk individueel rapport kunnen worden toegelaten gebruikend Media die Opstelling melden (geef Montages > Mediabeheer > Mediarapportering uit).

![](assets/report-setup.png)

In de werkruimte Analytics bevinden alle nieuwe eigenschappen zich in het deelvenster Metrics. U kunt bijvoorbeeld zoeken op `full screen` om de gegevens van het volledige scherm weer te geven in het deelvenster Metriek.

![](assets/full-screen-report.png)

## Door speler opgegeven meetgegevens importeren naar Adobe Experience Platform

De gegevens die zijn opgeslagen in Analytics kunnen voor elk doel worden gebruikt en de metriek van de spelerstatus kunnen in het Adobe Experience Platform worden geïmporteerd met XDM en worden gebruikt met Customer Journey Analytics. De eigenschappen van de standaardstatus hebben specifieke eigenschappen, terwijl de aangepaste statussen eigenschappen zijn die beschikbaar zijn via aangepaste gebeurtenissen. Zie de eigenschappenlijst voor XDM-identiteiten in ?LINK TO METRIC LIST? voor aanvullende informatie.
