---
title: API voor streaming media Collection � Events Request Endpoint
description: Wat zijn de gebeurtenissen van de Inzameling van Media API verzoeken eindpuntparameters en reacties?
uuid: b237f0a0-dc29-418b-89ee-04c596a27f39
exl-id: ee0dd8a6-1529-4258-af12-0e2f5948ec38
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 1%

---

# Verzoek om gebeurtenissen{#events-request}

`POST https://{uri}/api/v1/sessions/{sid}/events`

## URI-parameter

`sid`: Sessieidentiteitskaart die van het verzoek van a [ Sessies ](mc-api-sessions-req.md) is teruggekeerd.

## Indieningsinstantie

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

* `playerTime` (verplicht)
   * `playhead` - Moet in seconden zijn, maar het kan een zwevende waarde zijn.
   * `ts` - Tijdstempel; moet in milliseconden zijn.
* `eventType` (verplicht)
* `params` (optioneel)
* `customMetadata` (Optioneel; alleen verzenden met gebeurtenistypen `adStart` en `chapterStart` )
* `qoeData` (optioneel)

Voor een lijst van geldige gebeurtenistypen voor deze versie, zie {de types en de beschrijvingen van 0} Gebeurtenis.[&#128279;](mc-api-event-types.md)

>[!IMPORTANT]
>
>***Advertentie die -**&#x200B;volgt kunt slechts advertenties binnen een`adBreak`* volgen.
>
>Als de gebeurtenissen `adBreakStart` en `adBreakComplete` &quot;bookends&quot; rondom advertenties ontbreken, worden `adStart` en `adComplete` gewoon genegeerd en wordt de bijbehorende duur van de advertentie bijgehouden als de duur van de hoofdinhoud. Dit kan een aanzienlijke invloed hebben op de geaggregeerde gegevens die in Adobe Analytics beschikbaar zullen zijn.

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
| **204** | **Geen inhoud.** <br/><br/> De hartslagvraag was succesvol. | N.v.t. |
| **400** | **Onjuist Verzoek.** <br/><br/> Verzoek had onjuist formaat. | Controleer de [ JSON bevestigingsschema&#39;s ](mc-api-json-validation.md) voor het verzoektype. |
| **404** | **niet gevonden.** <br/><br/> Sessie-id voor de mediasessie is niet gevonden in de back-end service. | De cliënttoepassing zou het [ verzoek van Sessies ](mc-api-sessions-req.md) API moeten gebruiken om een andere media zitting tot stand te brengen en het volgen op het te melden. |
| **410** | **Gone.** <br/><br/> de media zitting werd gevonden in de achterste-einddienst maar de cliënt kan activiteit niet meer op het melden. | De cliënttoepassing zou het [ verzoek van Sessies ](mc-api-sessions-req.md) API moeten gebruiken om een andere media zitting tot stand te brengen en het volgen op het te melden. |
| **500** | **fout van de Server** | N.v.t. |
