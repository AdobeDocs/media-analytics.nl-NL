---
seo-title: Overview
title: API-overzicht voor streaming media
description: Leer over de API van de Inzameling van Media en hoe uw speler audio en videogebeurtenissen kan volgen gebruikend de vraag van HTTP RESTful.
uuid: c14bdbef-5846-4d31-8a14-8e9e0e9c9861
exl-id: 58430636-7fab-433a-8ead-52ccaa45d920
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---

# API-overzicht van mediagroep {#overview}

De Media Collection API is Adobe RESTful alternatief aan cliënt-kant Media SDK. Met de Media Collection API kan uw speler audio en videogebeurtenissen volgen gebruikend vraag RESTful van HTTP.

De Media Collection API is hoofdzakelijk een adapter, handelend als server-zijversie van Media SDK. Dit betekent dat sommige aspecten van de documentatie van Media SDK ook relevant zijn voor de API van de Inzameling van Media. Bijvoorbeeld, gebruiken beide oplossingen de zelfde [&#x200B; Streaming Parameters van Media &#x200B;](../variables/audio-video-parameters.md), en de verzamelde het stromen media volgende gegevens leiden tot het zelfde [&#x200B; Melden en Analyse.](/help/reporting/media-reports-enable.md)

## Gegevensstromen voor het bijhouden van media {#media-tracking-data-flows}

Een mediaspeler die de Media Collection API implementeert, maakt RESTful API-tracking-aanroepen rechtstreeks naar de back-endserver voor het bijhouden van media, terwijl een speler die de Media SDK implementeert, traceeraanroepen uitvoert naar de SDK API&#39;s in de speler-app. Één effect van het maken van vraag over het Web is dat de speler die de inzameling API van Media uitvoert enkele verwerking moet behandelen die de Media SDK automatisch behandelt. (Details in [&#x200B; Implementatie van de Inzameling van Media.](mc-api-impl/mc-api-quick-start.md))

De volggegevens die met de Media Collection API worden gevangen worden verzonden en aanvankelijk verwerkt verschillend dan de volggegevens die in een speler van Media SDK worden gevangen, maar de zelfde verwerkingsmotor op het achterste eind wordt gebruikt voor beide oplossingen.

![](assets/col_api_overview_simple.png)

## API-overzicht {#api-overview}

**URI:** verkrijg dit van uw vertegenwoordiger van Adobe.

**Methode van HTTP:** POST, met JSON- verzoeklichaam.

### API-aanroepen {#mc-api-calls}

* **`sessions`-** vestigt een zitting met de server, en keert een Zitting ID terug die in verdere `events` vraag wordt gebruikt. Uw app roept dit eenmaal aan het begin van een volgende sessie aan.

  `{uri}/api/v1/sessions`

* **`events`-** verzendt gegevens voor het bijhouden van media.

  `{uri}/api/v1/sessions/{session-id}/events`

### Indieningsinstantie {#mc-api-request-body}

```json
{
    "playerTime": {
        "playhead": "{playhead position in seconds}",
        "ts": "{timestamp in milliseconds}"
    },
    "eventType": "{event-type}",
    "params": {
        "{parameter-name}": "{parameter-value}",
        "{parameter-name}": "{parameter-value}"
    },
    "qoeData" : {
        "{parameter-name}": "{parameter-value}",
        "{parameter-name}": "{parameter-value}"
    },
    "customMetadata": {
        "{parameter-name}": "{parameter-value}",
        "{parameter-name}": "{parameter-value}"
    }
}
```

* `playerTime` - Verplicht voor alle verzoeken.
* `eventType` - Verplicht voor alle verzoeken.
* `params` - Verplicht voor bepaalde `eventTypes`; controleer het [&#x200B; JSON bevestigingsschema &#x200B;](mc-api-ref/mc-api-json-validation.md) om te bepalen welke eventTypes verplicht zijn, en die facultatief zijn.

* `qoeData` - Optioneel voor alle aanvragen.
* `customMetadata` - Optioneel voor alle aanvragen, maar alleen verzonden met de gebeurtenistypen `sessionStart` , `adStart` en `chapterStart` .

Voor elk `eventType`, is er openbaar beschikbaar [&#x200B; JSON bevestigingsschema &#x200B;](mc-api-ref/mc-api-json-validation.md) dat u zou moeten gebruiken om parametertypes te verifiëren en of een parameter voor een bepaalde gebeurtenis facultatief of vereist is.

### Gebeurtenistypen {#mc-api-event-types}

* `sessionStart`
* `play`
* `ping`
* `pauseStart`
* `bufferStart`
* `adStart`
* `adComplete`
* `adSkip`
* `adBreakStart`
* `adBreakComplete`
* `chapterStart`
* `chapterSkip`
* `chapterComplete`
* `sessionEnd`
* `sessionComplete`
* `stateStart`
* `stateEnd`
