---
title: Meerdere spelerstatussen tegelijk bijwerken
description: Dit onderwerp beschrijft de Veelvoudige eigenschap van het Volgen van de Staat van de Speler.
feature: Streaming Media
role: User, Admin, Developer
exl-id: 7a512a81-a6d1-4d0c-a4fe-91e9b11419db
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# Meerdere spelerstatussen bijhouden

Soms is het begin en einde van twee spelerstaten tegelijkertijd of is het einde van een status ook het begin van een andere status, zoals in de volgende afbeelding wordt getoond:

![&#x200B; Veelvoudige spelerstaten &#x200B;](assets/multiple-player-states.png)

De huidige implementatie staat beide scenario&#39;s toe:
- `stateStart(pictureInPicture)` - t0
- `stateStart(mute)` - t0
- `stateEnd(mute)` - t1
- `stateEnd(pictureInPicture)` - t1
- `stateStart(fullScreen)` - t1
- `stateEnd(fullScreen)` - t2

Dit vereist echter dat u meerdere `stateStart` - en `stateEnd` -gebeurtenissen opgeeft om meerdere gelijktijdige wijzigingen in de status aan te geven. In
om dit algemene gedrag te optimaliseren, is een nieuw `statesUpdate` gebeurtenistype geïmplementeerd, dat een lijst met staten beëindigt
en start een lijst met nieuwe staten.

Met de nieuwe `statesUpdate` -gebeurtenis wordt de bovenstaande lijst met gebeurtenissen:
- `statesUpdate(statesEnd=[], statesStart=[pictureInPicture, mute])` - t0
- `statesUpdate(statesEnd=[mute, pictureInPicture], statesStart=[fullScreen])` - t1
- `statesUpdate(statesEnd=[fullScreen], statesStart=[])` - t2

Het aantal vraag van staatsupdates is verminderd van zes tot drie voor het zelfde gedrag. De laatste gebeurtenis
had ook een eenvoudige `stateEnd(fullScreen)` kunnen zijn.

## API-implementatie voor mediaverzameling {#mpst-api}

U kunt de API voor mediagroep gebruiken om meerdere statussen van spelers te implementeren.

### Voorbeeld

In het volgende voorbeeld ziet u een voorbeeld van een API-implementatie voor Media Collection voor het bijhouden van meerdere spelerstatussen.

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
