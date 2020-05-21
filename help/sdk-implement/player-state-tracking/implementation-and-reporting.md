---
title: Uitvoering en verslaglegging
description: In dit onderwerp wordt beschreven hoe u de functie voor het bijhouden van de spelerstatus kunt implementeren, inclusief.
translation-type: tm+mt
source-git-commit: b0bfe74d1f6083e700dbf98f504a17518bd19ecb
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# Uitvoering en verslaglegging

Tijdens een afspeelsessie moet elke statusinstantie (begin tot eind) afzonderlijk worden bijgehouden. De Media SDK en de Media Collection API verstrekken nieuwe het volgen methodes voor dit vermogen.

De Media SDK bevat twee nieuwe methoden voor het bijhouden van aangepaste statussen:

`trackStateStart("state_name")`

`trackStateClose("state_name")`


De Media Collection API omvat twee nieuwe gebeurtenissen die &quot;media.stateName&quot;als vereiste parameter hebben:

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

* `a.media.states.(media.state.name).set = true` — Ingesteld op true als de status ten minste eenmaal is ingesteld voor elke specifieke weergave van een stream.
* `a.media.states.(media.state.name).count = 4` — Identificeert het aantal instanties van een status tijdens elke afzonderlijke afspeelbewerking van een stream.
* `a.media.states.(media.state.name).time = 240` — Geeft de totale frameduur aan in seconden per afzonderlijke afspeelbewerking van een stream.

## Rapportage

Alle staatsmetriek kan voor om het even welke rapporteringsvisualisatie of component (segment, berekende metriek) worden gebruikt.
TBD - controleer bron/wiki voor bijgewerkte informatie - voor het schermschot van AW

## Door speler opgegeven meetgegevens importeren naar Adobe Experience Platform

De gegevens die zijn opgeslagen in Analytics kunnen voor elk doel worden gebruikt en de metriek van de spelerstatus kunnen in het Adobe Experience Platform worden geïmporteerd met XDM en worden gebruikt met Customer Journey Analytics. De eigenschappen van de standaardstatus hebben specifieke eigenschappen, terwijl de aangepaste statussen eigenschappen zijn die beschikbaar zijn via aangepaste gebeurtenissen. Zie de eigenschappenlijst voor XDM-identiteiten in ?LINK TO METRIC LIST? voor aanvullende informatie.
