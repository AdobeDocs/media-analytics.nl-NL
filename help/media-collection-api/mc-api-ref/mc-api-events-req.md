---
title: Verzoek om gebeurtenissen
description: null
uuid: b237f0a0-dc29-418b-89ee-04c596a27f39
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Verzoek om gebeurtenissen{#events-request}

```
POST 
https://{uri}/api/v1/sessions/{sid}/events 
```

## URI-parameter

`sid`: De sessie-id die door een [sessieverzoek is geretourneerd.](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)

## Verzoek

De aanvraaginstantie moet JSON zijn en dezelfde structuur hebben als deze instantie die het verzoek indient:

```
{ 
    "playerTime": { 
        "playhead": 0, 
        "ts": 1509045324153 
    }, 
    "eventType": "{event-type}", 
    "params": {}, 
    "qoeData": {}, 
    "customMetadata": {} 
}
```

* `playerTime` (Verplicht)
   * `playhead` - Moet in seconden zijn, maar het kan een float zijn.
   * `ts` - Tijdstempel; moet in milliseconden zijn.
* `eventType` (Verplicht)
* `params` (Optioneel)
* `customMetadata` (facultatief; alleen verzenden met `adStart` en `chapterStart` gebeurtenistypen)
* `qoeData` (Optioneel)

Zie [Gebeurtenistypen en beschrijvingen voor een lijst met geldige gebeurtenistypen voor deze release.](/help/media-collection-api/mc-api-ref/mc-api-event-types.md)

>[!IMPORTANT]
>
>***Advertenties bijhouden -**U kunt alleen advertenties in een`adBreak`*.
>
>Als er geen `adBreakStart` en `adBreakComplete` &quot;boekensteunen&quot; zijn rond advertenties, worden `adStart` en `adComplete` gebeurtenissen gewoon genegeerd en wordt de bijbehorende duur van de advertentie bijgehouden als de duur van de hoofdinhoud. Dit kan grote gevolgen hebben voor de geaggregeerde gegevens die beschikbaar zijn in Adobe Analytics.

## Antwoord

```
HTTP/1.1 204 No Content 
Server nginx/1.13.5 
Date Thu, 26 Oct 2017 19:15:24 GMT 
Connection keep-alive 
Access-Control-Allow-Origin * 
Access-Control-Allow-Methods OPTIONS,POST,PUT 
Access-Control-Allow-Headers Content-Type 
Access-Control-Expose-Headers Location
```

## HTTP-responscodes

| HTTP-antwoordcode | Beschrijving | Client-actiepunten |
|---|---|---|
| **204** | **Geen inhoud.** Aanroep <br/><br/>hartslag is gelukt. | N.v.t. |
| **400** | **Onjuist verzoek.** De <br/><br/>aanvraag had een onjuiste indeling. | Controleer de [JSON-validatieschema&#39;s](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) voor het type aanvraag. |
| **404** | **Niet gevonden.** <br/><br/>De sessie-id voor de mediasessie is niet gevonden in de back-endservice. | De clienttoepassing moet de [Sessieverzoek](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) -API gebruiken om een andere mediasessie te maken en er een rapport over te bijhouden. |
| **410** | **Kegel.** <br/><br/>De mediasessie is gevonden in de back-endservice, maar de client kan er geen activiteiten meer over rapporteren. | De clienttoepassing moet de [Sessieverzoek](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) -API gebruiken om een andere mediasessie te maken en er een rapport over te bijhouden. |
| **500** | **Serverfout** | N.v.t. |

