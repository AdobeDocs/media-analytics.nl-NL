---
title: Meerdere spelerstatussen tegelijk bijwerken
description: Dit onderwerp beschrijft de Veelvoudige eigenschap van het Volgen van de Staat van de Speler.
exl-id: a77bc882-ac03-40b4-ac64-87f26a09707b
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 7a28674024739593431a942d5e0a498294bbe793
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Meerdere spelerstatussen bijhouden

Er zijn situaties waarin twee spelerstaten tegelijkertijd beginnen en eindigen of wanneer het einde van een status ook het begin van een andere status is. Kijk naar het volgende voorbeeld:

![Meerdere spelstatussen](assets/multiple-player-states.svg)

De huidige implementatie staat beide scenario&#39;s toe:
- `stateStart(pictureInPicture)` - t0
- `stateStart(mute)` - t0
- `stateEnd(mute)` - t1
- `stateEnd(pictureInPicture)` - t1
- `stateStart(fullScreen)` - t1
- `stateEnd(fullScreen)` - t2

De client moet echter veel `stateStart` en `stateEnd` gebeurtenissen om meerdere gelijktijdige statuswijzigingen aan te geven. Om dit algemene gedrag te optimaliseren, moet u een nieuwe `statesUpdate` gebeurtenistype is geïmplementeerd, dat een lijst met staten beëindigt en een lijst met nieuwe staten start.

De nieuwe `statesUpdate` wordt de bovenstaande lijst met gebeurtenissen:
- `statesUpdate(statesEnd=[], statesStart=[pictureInPicture, mute])` - t0
- `statesUpdate(statesEnd=[mute, pictureInPicture], statesStart=[fullScreen])` - t1
- `statesUpdate(statesEnd=[fullScreen], statesStart=[])` - t2

Het aantal vraag van staatsupdates is verminderd van 6 tot slechts 3 voor het zelfde gedrag. De laatste gebeurtenis had ook eenvoudig kunnen zijn `stateEnd(fullScreen)`.

## API-implementatie voor mediaverzameling

Voorbeelden:

```
// statesUpdate (ex: mute and pictureInPicture are switched on)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "statesUpdate",
  "params": {
    "statesStart": [
      {
        "media.state.name": "mute"
      },
      {
        "media.state.name": "pictureInPicture"
      }
    ]
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

```
// statesUpdate (ex: mute and pictureInPicture are switched off, fullScreen is switched on)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [
      {
        "media.state.name": "mute"
      },
      {
        "media.state.name": "pictureInPicture"
      }
    ],
    "statesStart": [
      {
        "media.state.name": "fullScreen"
      }
    ]
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

```
// statesUpdate (ex: fullScreen is switched off)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [
      {
        "media.state.name": "fullScreen"
      }
    ]
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

## Media SDK-implementatie

Er is geen Media SDK-implementatie.
