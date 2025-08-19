---
title: API voor streaming Media Services — Eindpunt verzoek sessies
description: Wat zijn de de zittingen van de Inzameling van Media verzoeken eindpuntparameters en reacties?
uuid: 9609192d-4f7f-4fb5-844f-ea89d47c4e30
exl-id: f55f5838-610f-4f82-b3c5-72165ea2c86b
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 3%

---

# Aanvraag voor sessies{#sessions-request}

```
POST 
https://{uri}/api/v1/sessions
```

## URI-parameters

Geen

## Indieningsinstantie

De aanvraaginstantie moet JSON zijn en dezelfde structuur hebben als deze instantie die het verzoek indient:

```
{ 
    "playerTime": { 
        "playhead": 0, 
        "ts": 1509045324153 
    }, 
    "eventType": "sessionStart", 
    "params": { 
        "media.playerName": "sample-html5-api-player", 
        "analytics.trackingServer": "<your-aa-tracking-server>", 
        "analytics.reportSuite": "<your-aa-rsid>", 
        "analytics.visitorId": "<your-userId>", 
        "media.contentType": "VOD", 
        "media.length": 60.39333333333333, 
        "media.id": "MA API Sample Player", 
        "visitor.marketingCloudOrgId": "<your-org-id>", 
        "media.name": "ClickMe", 
        "media.channel": "sample-channel", 
        "media.sdkVersion": "va-api-0.0.0", 
        "analytics.enableSSL": false 
    }, 
    "customMetadata": { 
        "myCustomData": "<your metadata>", 
        "myCustomData2": "<your metadata>", 
        ... 
    }, 
    "qoeData": { 
        "param1": "<your param-value>", 
        "param2": "<your param-value>", 
        ... 
    } 
}
```

* `playerTime` (verplicht)
   * `playhead` - Als de inhoud live is, moet de afspeelkop de huidige seconde van de dag zijn, 0 &lt;= playhead &lt; 86400. Als de inhoud wordt opgenomen, moet de afspeelkop de huidige seconde van de inhoud zijn, 0 &lt;= playhead &lt; lengte van de inhoud. De waarde kan een drijvende-kommagetal zijn.
   * `ts` - Tijdstempel; moet in milliseconden zijn; Coordinated Universal Time (UTC).
* `eventType` (verplicht)

  **Geldige waarde:** `sessionStart`
* `params` (verplicht)
* `customMetadata` (optioneel)
* `qoeData` (optioneel)

## Antwoord

```
HTTP/1.1 201 Created 
Server: nginx/1.13.5 
Date: Wed, 06 Dec 2017 19:14:51 GMT 
Content-Type: application/octet-stream 
Content-Length: 0 
Location: /api/v1/sessions/bfcca2ca597a3c71bc03b4ce357833ad02b3570d262ecd0c595fcf8f2ae4df58 
Access-Control-Allow-Origin: * 
Access-Control-Allow-Methods: OPTIONS,POST,PUT 
Access-Control-Allow-Headers: Content-Type 
Access-Control-Expose-Headers: Location 
Age: 0 
Via: 1.1 wsg.sanjose08
```

`Location:` header - Het `/api/v1/` -onderdeel biedt de API-versie. Het deel na `[…]sessions/` is de sessie-id.

## Antwoordcodes

| HTTP-antwoordcode | Beschrijving |
|---|---|
| 201 | Sessie gemaakt |
| 400 | Ongeldig verzoek |
| 500 | Serverfout |
