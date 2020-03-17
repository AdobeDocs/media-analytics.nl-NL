---
title: Aanvraag voor sessies
description: null
uuid: 9609192d-4f7f-4fb5-844f-ea89d47c4e30
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Aanvraag voor sessies{#sessions-request}

```
POST 
https://{uri}/api/v1/sessions
```

## URI-parameters

Geen

## Verzoek

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

* `playerTime` (Verplicht)
   * `playhead` - Moet in seconden zijn, maar het kan een float zijn.
   * `ts` - Tijdstempel; moet in milliseconden zijn.
* `eventType` (Verplicht)

   **Geldige waarde:**`sessionStart`
* `params` (Verplicht)
* `customMetadata` (Optioneel)
* `qoeData` (Optioneel)

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

`Location:` header - Het `/api/v1/` onderdeel bevat de API-versie. Het deel na `[…]sessions/` is Zitting ID.

## Antwoordcodes

| HTTP-antwoordcode | Beschrijving |
|---|---|
| 201 | Sessie gemaakt |
| 400 | Ongeldig verzoek |
| 500 | Serverfout |
