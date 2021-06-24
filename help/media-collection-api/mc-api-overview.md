---
seo-title: Overzicht
title: API-overzicht voor streaming media
description: Leer over de API van de Inzameling van Media en hoe uw speler audio en videogebeurtenissen kan volgen gebruikend de vraag van HTTP RESTful.
uuid: c14bdbef-5846-4d31-8a14-8e9e0e9c9861
exl-id: 58430636-7fab-433a-8ead-52ccaa45d920
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---

# Overzicht{#overview}

De API van de Inzameling van Media is RESTful alternatief aan de cliënt-zijMedia SDK. Met de Media Collection API kan uw speler audio en videogebeurtenissen volgen gebruikend vraag RESTful van HTTP.

De API voor mediaverzamelingen is in wezen een adapter die fungeert als een serverversie van de SDK van Media. Dit betekent dat sommige aspecten van de documentatie van SDK van Media ook relevant voor de Inzameling API van Media zijn. Beide oplossingen gebruiken bijvoorbeeld dezelfde [Streaming Media Parameters](/help/metrics-and-metadata/audio-video-parameters.md), en de verzamelde gegevens voor het bijhouden van streaming media leiden tot dezelfde [Rapportage en Analyse.](/help/media-reports/media-reports-enable.md)

## Gegevensstromen voor het bijhouden van media {#media-tracking-data-flows}

Een mediaspeler die de Media Collection API implementeert, maakt RESTful API-traceringsaanroepen rechtstreeks naar de back-endserver voor mediatracering, terwijl een speler die de Media SDK implementeert, traceeraanroepen uitvoert naar de SDK API&#39;s in de speler-app. Één effect van het maken van vraag over het Web is dat de speler die de API van de Inzameling van Media uitvoert enkele verwerking moet behandelen die de Media SDK automatisch behandelt. (Details in [Implementatie van de Inzameling van Media.](mc-api-impl/mc-api-quick-start.md))

De volggegevens die met de Media Collection API worden gevangen worden verzonden en aanvankelijk verwerkt verschillend dan de volggegevens die in een speler van SDK van Media worden gevangen, maar de zelfde verwerkingsmotor op het achterste eind wordt gebruikt voor beide oplossingen.

![](assets/col_api_overview_simple.png)

## API-overzicht {#api-overview}

**URI:** Vraag dit aan bij uw Adobe-medewerker.

**HTTP-methode:** POST, met JSON-aanvraaginstantie.

### API-aanroepen {#mc-api-calls}

* **`sessions`-** Vestigt een zitting met de server, en keert een identiteitskaart van de Zitting terug die in verdere  `events` vraag wordt gebruikt. Uw app roept dit eenmaal aan het begin van een volgende sessie aan.

   ```
   {uri}/api/v1/sessions
   ```

* **`events`-** Hiermee worden gegevens voor het bijhouden van media verzonden.

   ```
   {uri}/api/v1/sessions/{session-id}/events
   ```

### Verzoek {#mc-api-request-body}

```
{
    "playerTime": {
        "playhead": {playhead position in seconds},
        "ts": {timestamp in milliseconds}
    },
    "eventType": {event-type},
    "params": {
        {parameter-name}: {parameter-value},
        ...
        {parameter-name}: {parameter-value}
    },
    "qoeData" : {
        {parameter-name}: {parameter-value},
        ...
        {parameter-name}: {parameter-value}
    },
    "customMetadata": {
        {parameter-name}: {parameter-value},
        ...
        {parameter-name}: {parameter-value}
    }
}
```

* `playerTime` - Verplicht voor alle verzoeken.
* `eventType` - Verplicht voor alle verzoeken.
* `params` - Verplicht voor bepaalde  `eventTypes`; controleert het  [JSON ](mc-api-ref/mc-api-json-validation.md) bevestigingsschema bepaalt welke eventTypes verplicht zijn, en die facultatief zijn.

* `qoeData` - Optioneel voor alle aanvragen.
* `customMetadata` - Optioneel voor alle aanvragen, maar alleen verzonden met  `sessionStart`,  `adStart`en  `chapterStart` gebeurtenistypen.

Voor elke `eventType`, is er openbaar beschikbaar [JSON bevestigingsschema](mc-api-ref/mc-api-json-validation.md) dat u zou moeten gebruiken om parametertypes te verifiëren en of een parameter facultatief of vereist voor een bepaalde gebeurtenis is.

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
