---
title: API voor streaming media Collection � Events Request Endpoint
description: '"Wat zijn de gebeurtenissen van de Inzameling van Media API verzoeken eindpuntparameters en reacties?"'
uuid: b237f0a0-dc29-418b-89ee-04c596a27f39
exl-id: ee0dd8a6-1529-4258-af12-0e2f5948ec38
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 4%

---

# Verzoek om gebeurtenissen{#events-request}

```
POST 
https://{uri}/api/v1/sessions/{sid}/events 
```

## URI-parameter

`sid`: De sessie-id die door een  [sessieverzoek is geretourneerd.](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)

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
* `customMetadata` (facultatief; alleen verzenden met  `adStart` en  `chapterStart` gebeurtenistypen)
* `qoeData` (Optioneel)

Zie [Gebeurtenistypen en beschrijvingen voor een lijst met geldige gebeurtenistypen voor deze release.](/help/media-collection-api/mc-api-ref/mc-api-event-types.md)

>[!IMPORTANT]
>
>***Advisering -**u kunt alleen advertenties in een`adBreak`*track volgen.
>
>Als de `adBreakStart` en `adBreakComplete` &quot;boekensteunen&quot;rond advertenties ontbreken, zullen `adStart` en `adComplete` eenvoudig worden genegeerd, en de overeenkomstige ad duur zal als belangrijkste inhoudsduur worden gevolgd. Dit kan een aanzienlijke invloed hebben op de geaggregeerde gegevens die in Adobe Analytics beschikbaar zullen zijn.

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
| **204** | **Geen inhoud.** <br/><br/>Aanroep hartslag is gelukt. | N.v.t. |
| **400** | **Onjuist verzoek.** <br/><br/>Verzoek had onjuiste indeling. | Controleer [JSON bevestigingsschema&#39;s](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) voor het verzoektype. |
| **404** | **Niet gevonden.** <br/><br/>De sessie-id voor de mediasessie is niet gevonden in de back-endservice. | De clienttoepassing moet de [Sessieaanvraag](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) API gebruiken om nog een mediasessie te maken en er een tekstspatiëring op toe te passen. |
| **410** | **Kegel.** <br/><br/>De mediasessie is gevonden in de back-endservice, maar de client kan er geen activiteiten meer over rapporteren. | De clienttoepassing moet de [Sessieaanvraag](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) API gebruiken om nog een mediasessie te maken en er een tekstspatiëring op toe te passen. |
| **500** | **Serverfout** | N.v.t. |
