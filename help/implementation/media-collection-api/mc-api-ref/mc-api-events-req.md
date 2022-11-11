---
title: API voor streaming media Collection � Events Request Endpoint
description: "Wat zijn de gebeurtenissen van de Inzameling van Media API verzoeken eindpuntparameters en reacties?"
uuid: b237f0a0-dc29-418b-89ee-04c596a27f39
exl-id: ee0dd8a6-1529-4258-af12-0e2f5948ec38
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 4%

---

# Verzoek om gebeurtenissen{#events-request}

`POST https://{uri}/api/v1/sessions/{sid}/events`

## URI-parameter

`sid`: De sessie-id die door een [Aanvraag voor sessies](mc-api-sessions-req.md).

## Verzoek

De aanvraaginstantie moet JSON zijn en dezelfde structuur hebben als deze instantie die het verzoek indient:

```json
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

Zie voor een lijst met geldige gebeurtenistypen voor deze release [Gebeurtenistypen en beschrijvingen.](mc-api-event-types.md)

>[!IMPORTANT]
>
>***Advertentie bijhouden -**U kunt alleen advertenties bijhouden in een`adBreak`*.
>
>Bij gebrek aan `adBreakStart` en `adBreakComplete` &quot;bookends&quot; rondom advertenties, `adStart` en `adComplete` gebeurtenissen worden gewoon genegeerd en de corresponderende duur van de advertentie wordt bijgehouden als de duur van de hoofdinhoud. Dit kan een aanzienlijke invloed hebben op de geaggregeerde gegevens die in Adobe Analytics beschikbaar zullen zijn.

## Antwoord

```text
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
| **204** | **Geen inhoud.** <br/><br/>Aanroep hartslag is gelukt. | N.v.t. |
| **400** | **Onjuist verzoek.** <br/><br/>Verzoek had onjuiste indeling. | Controleer de [JSON-validatieschema&#39;s](mc-api-json-validation.md) voor het type aanvraag. |
| **404** | **Niet gevonden.** <br/><br/>De sessie-id voor de mediasessie is niet gevonden in de back-endservice. | De clienttoepassing moet de opdracht [Aanvraag voor sessies](mc-api-sessions-req.md) API om een andere mediasessie te maken en rapport bijhouden. |
| **410** | **Kegel.** <br/><br/>De mediasessie is gevonden in de back-endservice, maar de client kan er geen activiteiten meer over rapporteren. | De clienttoepassing moet de opdracht [Aanvraag voor sessies](mc-api-sessions-req.md) API om een andere mediasessie te maken en rapport bijhouden. |
| **500** | **Serverfout** | N.v.t. |
