---
title: Tijdlijn 3 - Hoofdstukken
description: null
uuid: 41b52072-e1cd-4dda-9253-31f3408924f6
translation-type: tm+mt
source-git-commit: 5107de22c2388e8ac5b15b8d28fa974e97363fdf

---


# Tijdlijn 3 - Hoofdstukken {#timeline-3-chapters}

## VOD, pre-roll advertenties, pauzeren, bufferen, inhoud weergeven tot het einde


De volgende diagrammen illustreren de tijdlijn van de afspeelkop en de bijbehorende tijdlijn van de handelingen van een gebruiker. De bijzonderheden van elke actie en de bijbehorende verzoeken worden hieronder weergegeven.


![](assets/va_api_content_3.png)


![](assets/va_api_actions_3.png)


## Handelingsdetails


### Actie 1 - Starten van sessie {#Action-1}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| De knop Automatisch afspelen of Afspelen is ingedrukt, de video wordt geladen. | 0 | 0 | `/api/v1/sessions` |

**Implementatiedetails**

Deze aanroep geeft _de intentie van de gebruiker om een video af te spelen_ . Het keert een identiteitskaart van de Zitting ( `{sid}` ) aan de cliënt terug die wordt gebruikt om alle volgende volgende volgende het volgen vraag binnen de zitting te identificeren. De spelerstatus wordt nog niet afgespeeld, maar &#39;gestart&#39;.  [Verplichte sessieparameters](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) moeten in de `params` kaart in de aanvraaginstantie worden opgenomen.  Op de achtergrond, leidt deze vraag tot een Analytics van Adobe vraag in werking stellen.

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:sessionStart, params: {
        "media.playerName": "sample-html5-api-player",
        "analytics.trackingServer": "[ _YOUR-TS_ ]",
        "analytics.reportSuite": "[ _YOUR_RSID_ ]",
        "analytics.visitorId": "[ _YOUR_VISITOR_ID_ ]",
        "media.contentType": "VOD",
        "media.length": 60.3333333333333,
        "media.id": "VA API Sample Player",
        "visitor.marketingCloudOrgId": "[YOUR_MCID]",
        "media.name": "ClickMe",
        "media.channel": "sample-channel",
        "media.sdkVersion": "va-api-0.0.0",
        "analytics.enableSSL": false
    }
}
```

### Handeling 2 - De timer pingelen wordt gestart {#Action-2}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| App start gebeurtenistimer | 0 | 0 |  |

**Implementatiedetails**

Begin pingelt tijdopnemer. De eerste pingel gebeurtenis zou dan 1 seconde binnen moeten in brand steken als er pre-roladvertenties zijn, anders 10 seconden.

### Actie 3 - Ad-break-start {#Action-3}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Begin vóór rol en einde track | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

Advertenties kunnen alleen worden bijgehouden binnen een advertentie-einde.

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adBreakStart, params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.podIndex": 0, "media.ad.podSecond": 0
    }
}
```

### Actie 4 - Ad start {#Action-4}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Begin van advertentie 1 vóór de rol bijhouden | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

Volg de eerste pre-roll advertentie, die 15 seconden lang is. Aangepaste metagegevens opnemen bij deze `adStart` .

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adStart, params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 1",
        "media.ad.id": "001",
        "media.ad.length": 15,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "1",
        "media.ad.creativeId": "42",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz_creative.com",
        "media.ad.placementId": "sample_placement"
    },
    customMetadata: {
        "myCustomData1": "CustomData1",
        "myCustomData2": "CustomData2"
    }
}
```

### Actie 5 - Advertentiepunten {#Action-5}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| App verzendt ping-gebeurtenis | 10 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

Pingel de achterkant om de 1 seconde. (Opeenvolgende en pingels die niet in het belang van de beknoptheid worden getoond.)

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Actie 6 - Toevoeging voltooid {#Action-6}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Volg de voorrol advertentie 1 voltooid | 15 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

Volg het einde van de eerste pre-roll advertentie.

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adComplete
}
```

### Actie 7 - Ad start {#Action-7}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Begin van advertentie 2 vóór de rol bijhouden | 15 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

Volg het begin van de tweede advertentie voor de rol, die 7 seconden lang is.

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adStart, params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 2",
        "media.ad.id": "002",
        "media.ad.length": 7,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "2",
        "media.ad.creativeId": "44",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz_creative.com",
        "media.ad.placementId": "sample_placement2"
    },
}
```

### Actie 8 - Pingelen {#Action-8}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| App verzendt ping-gebeurtenis | 16 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

Pingel de achterkant om de 1 seconde. (Opeenvolgende en pingels die niet in het belang van de beknoptheid worden getoond.)

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Actie 9 - Toevoegen voltooid {#Action-9}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Volg de voorrol advertentie 2 voltooid | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

Het einde van de tweede advertentie vóór de rol bijhouden.

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adComplete
}
```

### Actie 10 - Einde advertentie {#Action-10}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Track voor rol en break voltooid | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

Het advertentiespoor is voorbij. Tijdens de hele advertentiesessie is de spelstatus blijven spelen.

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adBreakComplete
}
```

### Actie 11 - Inhoud afspelen {#Action-11}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Gebeurtenis track afspelen | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

Na de `adBreakComplete` gebeurtenis plaatst u de speler in de afspeelstatus met de `play` gebeurtenis.

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:play
}
```

### Actie 12 - Begin hoofdstuk {#Action-12}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| De gebeurtenis Start van hoofdstuk bijhouden | 23 | 1 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

Volg na de afspeelgebeurtenis het begin van het eerste hoofdstuk.

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:chapterStart, params: {
        "media.chapter.index": 1,
        "media.chapter.offset": 0, "media.chapter.length": 20, "media.chapter.friendlyName": "Chapter Uno"
    },
}
```

### Actie 13 - Ping {#Action-13}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| App verzendt ping-gebeurtenis | 30 | 8 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

Pingel het achterste eind om de 10 seconden.

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 8,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Actie 14 - Begin buffer {#Action-14}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Gebeurtenis bufferbegin opgetreden | 33 | 11 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

Houd de verplaatsing naar de bufferstatus bij.

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 11,
        ts: <timestamp>
    },
    eventType:bufferStart
}
```

### Actie 15 - Buffereinde (afspelen) {#Action-15}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Buffering beëindigd, de app volgt hervatting van inhoud | 36 | 11 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

Bufferbewerkingen worden na 3 seconden beëindigd. Zet de speler dus terug naar de afspeelstatus. U moet een andere gebeurtenis voor het afspelen van tracks verzenden die buiten de buffering valt.  **De`play`vraag na een`bufferStart`&quot;bufferEnd&quot;vraag aan het achtereind,** zodat is er geen behoefte aan een `bufferEnd` gebeurtenis.

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 11,
        ts: <timestamp>
    },
    eventType:play
}
```

### Actie 16 - Ping {#Action-16}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| App verzendt ping-gebeurtenis | 40 | 15 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

Pingel het achterste eind om de 10 seconden.

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 15,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Actie 17 - Einde hoofdstuk {#Action-17}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Hoofdstukeinde van app-tracks | 45 | 20 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

Het eerste hoofdstuk eindigt, vlak voor het tweede en het tweede einde.

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 20,
        ts: <timestamp>
    },
    eventType:chapterComplete
}
```

### Actie 18 - Ad break start {#Action-18}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Begin middelste rol en onderbreking volgen | 46 | 21 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

Midden rol en duur van 8 seconden: verzenden `adBreakStart` .

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adBreakStart, params: {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.podIndex": 1, "media.ad.podSecond": 21
    }
}
```

### Actie 19 - Ad start {#Action-19}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Begin middelste rol #3 | 46 | 21 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

Houd de middenrol advertentie bij.

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adStart, params: {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.name": "Ad 3",
        "media.ad.id": "003",
        "media.ad.length": 8,
        "media.ad.podPosition": 2,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "7",
        "media.ad.creativeId": "40",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz_creative.com",
        "media.ad.placementId": "sample_placement2"
    },
}
```

### Actie 20 - Pings {#Action-20}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| App verzendt ping-gebeurtenis | 47 | 21 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

Pingel de achterkant om de 1 seconde. (Opeenvolgende en pingels die niet in het belang van de beknoptheid worden getoond.)

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Actie 21 - Toevoeging voltooid {#Action-21}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Track mid-roll advertentie 1 voltooid | 54 | 21 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

De mid-roll advertentie is compleet.

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adComplete
}
```

### Actie 22 - Einde advertentie {#Action-22}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Halverrol en break bijhouden voltooid | 54 | 21 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

Het advertentieeinde is voltooid.

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adBreakComplete
}
```

### Actie 23 - Begin hoofdstuk {#Action-23}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Begin van hoofdstuk 2 volgen | 55 | 22 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**



**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 22,
        ts: <timestamp>
    },
    eventType:chapterStart, params: {
        "media.chapter.index": 2,
        "media.chapter.offset": 22, "media.chapter.length": 22, "media.chapter.friendlyName": "Chapter Dos"
    },
}
```

### Actie 24 - Ping {#Action-24}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| App verzendt ping-gebeurtenis | 60 | 27 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

Pingel het achterste eind om de 10 seconden.

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 27,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Actie 25 - Pauze {#Action-25}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Door gebruiker gepauzeerd | 64 | 31 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

De handeling van de gebruiker verplaatst de afspeelstatus naar &quot;gepauzeerd&quot;.

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    },
    eventType:pauseStart
}
```

### Actie 26 - Ping {#Action-26}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| App verzendt ping-gebeurtenis | 70 | 31 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

Pingel het achterste eind om de 10 seconden. Player bevindt zich nog steeds in de bufferstatus; de gebruiker zit vast op 20 seconden inhoud . Fuming...

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Actie 27 - Inhoud afspelen {#Action-27}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Gebruiker heeft op Afspelen gedrukt om de hoofdinhoud te hervatten | 74 | 31 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

De afspeelstatus verplaatsen naar Afspelen.  **De`play`vraag na een`pauseStart`infers een &quot;hervattingsvraag&quot;aan het achtereind**, zodat is er geen behoefte aan een `resume` gebeurtenis.

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    },
    eventType:play
}
```

### Actie 28 - Ping {#Action-28}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| App verzendt ping-gebeurtenis | 80 | 37 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

Pingel het achterste eind om de 10 seconden.

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 37,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Actie 29 - Einde hoofdstuk {#Action-29}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Hoofdstuk 2 | 87 | 44 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

Het einde van het tweede en laatste hoofdstuk bijhouden.

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:chapterComplete
}
```

### Actie 30 - Sessie voltooid {#Action-30}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| De gebruiker heeft de inhoud tot het einde bekeken. | 88 | 45 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

Naar `sessionComplete` de achtergrond sturen om aan te geven dat de gebruiker klaar is met het bekijken van de volledige inhoud.

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 45,
        ts: <timestamp>
    },
    eventType:sessionComplete
}
```


>[!NOTE]
>
>**Geen zoekgebeurtenissen? -** Er is geen expliciete ondersteuning voor gebeurtenissen `seekStart` `seekComplete` of gebeurtenissen in de Media Collection API. Dit is omdat bepaalde spelers een zeer groot aantal dergelijke gebeurtenissen produceren wanneer de eindgebruiker schrobt, en verscheidene honderden gebruikers de netwerkbandbreedte van een backenddienst gemakkelijk konden knelpen. Adobe biedt expliciete ondersteuning voor zoekgebeurtenissen door de hartslagduur te berekenen op basis van de tijdstempel van het apparaat in plaats van de positie van de afspeelkop.

