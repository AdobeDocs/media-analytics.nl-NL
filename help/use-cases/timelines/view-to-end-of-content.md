---
title: Meer informatie over tijdlijnen voor het bijhouden van media
description: Dig dieper in de playhead chronologie en overeenkomstige acties van de gebruiker. Meer informatie over de details van elke actie en de bijbehorende verzoeken.
uuid: 0ff591d3-fa99-4123-9e09-c4e71ea1060b
exl-id: 16b15e03-5581-471f-ab0c-077189dd32d6
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a1c3bdbec223ab0141d922dce07ba2128b52e794
workflow-type: tm+mt
source-wordcount: '1120'
ht-degree: 5%

---

# Tijdlijn 1 - Weergeven tot einde van inhoud{#timeline-view-to-end-of-content}

## VOD, pre-roll advertenties, pauzeren, bufferen, inhoud weergeven tot het einde

De volgende diagrammen illustreren de tijdlijn van de afspeelkop en de overeenkomstige tijdlijn van de handelingen van een gebruiker. De bijzonderheden van elke actie en de bijbehorende verzoeken worden hieronder weergegeven.

![ API inhoud ](assets/va_api_content.png)

![ API acties ](assets/va_api_actions.png)

## Handelingsdetails

### Actie 1 - Starten van sessie {#Action-1}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| De knop Automatisch afspelen of Afspelen is ingedrukt, de video wordt geladen. | 0 | 0 | `/api/v1/sessions` |

Deze vraag signaleert _de intentie van de gebruiker om_ een video te spelen.

Er wordt een sessie-id ( `{sid}` ) geretourneerd aan de client die wordt gebruikt om alle volgende opvolgende opvolgende aanroepen binnen de sessie te identificeren. De spelerstatus wordt nog niet afgespeeld, maar &#39;gestart&#39;.

Verplichte sessieparameters moeten in de `params` -kaart in de aanvraaginstantie worden opgenomen. Zie de documentatie van de API voor mediagroep voor informatie over sessies.

Op de achtergrond, produceert deze vraag Adobe Analytics in werking stelt vraag in werking.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType":"sessionStart, params" {
        "media.playerName": "sample-html5-api-player",
        "analytics.trackingServer": "[ _YOUR_TS_ ]",
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

### Handeling 2 - Start timer pingelen {#Action-2}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| App start gebeurtenistimer | 0 | 0 | `/api/v1/sessions/{sid}/events` | |

Start de pingtimer van uw app. De eerste pingel gebeurtenis zou dan 1 seconde binnen moeten in brand steken als er pre-roladvertenties zijn, anders 10 seconden.

### Actie 3 - Ad-break-start {#Action-3}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Begin vóór rol en einde track | 0 | 0 | `/api/v1/sessions/{sid}/events` |

Advertenties kunnen alleen worden bijgehouden binnen een advertentie-einde.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType":"adBreakStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.podIndex": 0,
        "media.ad.podSecond": 0
    }
}
```

### Actie 4 - Ad start {#Action-4}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Begin van advertentie 1 vóór de rol bijhouden | 0 | 0 | `/api/v1/sessions/{sid}/events` |

Volg de eerste advertentie voor de rol, die 15 seconden lang is. Aangepaste metagegevens opnemen met deze `adStart` .

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType":"adStart",
    "params": {
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
        "media.ad.creativeURL": "https://example.com",
        "media.ad.placementId": "sample_placement"
    },
    "customMetadata": {
        "myCustomData1": "CustomData1",
        "myCustomData2": "CustomData2"
    }
}
```

**NOTA: Tussen gebeurtenissen AdBreakStart en AdStart zouden er geen extra playbackgebeurtenissen moeten zijn.**

### Actie 5 - Advertentiepunten {#Action-5}

#### Actie 5.1 - Pingel 1 {#Action-5-1}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| App verzendt ping-gebeurtenis | 1 | 0 | `/api/v1/sessions/{sid}/events` |

Pingel de steun om de 1 seconde terwijl binnen een advertentie.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

#### Actie 5.2 - Pping 2 {#Action-5-2}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| App verzendt ping-gebeurtenis | 2 | 0 | `/api/v1/sessions/{sid}/events` |

Pingel de steun om de 1 seconde terwijl binnen een advertentie.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

#### Actie 5.3 - Pping 3 {#Action-5-3}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| App verzendt ping-gebeurtenis | 3 | 0 | `/api/v1/sessions/{sid}/events` |

Pingel de steun om de 1 seconde terwijl binnen een advertentie.

>[!NOTE]
>
>De volgende advertenties in de chronologie zullen overslaan die de reeks van één-tweede pingelt tonen
>in het belang van de beknoptheid...

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### Actie 6 - Toevoeging voltooid {#Action-6}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Volg de voorrol advertentie 1 voltooid | 15 | 0 | `/api/v1/sessions/{sid}/events` |

Volg het einde van de eerste pre-roll advertentie.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adComplete"
}
```

### Actie 7 - Ad start {#Action-7}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Begin van advertentie 2 vóór de rol bijhouden | 15 | 0 | `/api/v1/sessions/{sid}/events` |

Volg het begin van de tweede advertentie voor de rol, die 7 seconden lang is.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adStart",
    "params": {
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
        "media.ad.creativeURL": "https://example.com",
        "media.ad.placementId": "sample_placement2"
    },
}
```

### Actie 8 - Pingelen {#Action-8}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| App verzendt ping-gebeurtenis | 20 | 0 | `/api/v1/sessions/{sid}/events` |

Pingel de achterkant om de 1 seconde.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### Actie 9 - Toevoegen voltooid {#Action-9}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Volg de instructies voor de rol Advertentie 2 voltooid | 22 | 0 | `/api/v1/sessions/{sid}/events` |

Het einde van de tweede advertentie vóór de rol bijhouden.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adComplete"
}
```

### Actie 10 - Einde advertentie {#Action-10}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Track voor rol en break voltooid | 22 | 0 | `/api/v1/sessions/{sid}/events` |

Het advertentiespoor is voorbij.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adBreakComplete"
}
```

### Actie 11 - Inhoud afspelen {#Action-11}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Gebeurtenis track afspelen | 22 | 0 | `/api/v1/sessions/{sid}/events` |

Na de gebeurtenis `adBreakComplete` plaatst u de speler in de afspeelstatus met de gebeurtenis `play` .

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "play"
}
```

### Actie 12 - Ping {#Action-12}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| App verzendt ping-gebeurtenis | 30 | 8 | `/api/v1/sessions/{sid}/events` |

Pingel het achterste eind om de 10 seconden.

```json
{
    "playerTime": {
        "playhead": 8,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### Actie 13 - Begin buffer {#Action-13}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Gebeurtenis bufferbegin opgetreden | 33 | 11 | `/api/v1/sessions/{sid}/events` |

Houd de beweging van de speler naar de bufferstatus bij.

```json
{
    "playerTime": {
        "playhead": 11,
        "ts": "<timestamp>"
    }, "eventType": "bufferStart"
}
```

### Actie 14 - Bufferuiteinde {#Action-14}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Buffering beëindigd, de app volgt hervatting van inhoud | 36 | 11 | `/api/v1/sessions/{sid}/events` |

Bufferbewerkingen worden na 3 seconden beëindigd. Zet de speler dus terug naar de afspeelstatus. U moet een andere gebeurtenis voor het afspelen van tracks verzenden die buiten de buffering valt.  **de `play` vraag na a `bufferStart` leidt tot een &quot;bufferEnd&quot;vraag aan het achtereind,** zodat is er geen behoefte aan een `bufferEnd` gebeurtenis.

```json
{
    "playerTime": {
        "playhead": 11,
        "ts": "<timestamp>"
    },
    "eventType": "play"
}
```

### Actie 15 - Ping {#Action-15}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| App verzendt ping-gebeurtenis | 40 | 15 | `/api/v1/sessions/{sid}/events` |

Pingel het achterste eind om de 10 seconden.

```json
{
    "playerTime": {
        "playhead": 15,
        "ts": "<timestamp>"
    }, "eventType": "ping"
}
```

### Actie 16 - Ad break start {#Action-16}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Begin middelste rol en onderbreking volgen | 46 | 21 | `/api/v1/sessions/{sid}/events` |

Midden rol en duur van 8 seconden: verzenden `adBreakStart` .

```json
{
    "playerTime": {
        "playhead": 21,
        "ts": "<timestamp>"
    },
    "eventType": "adBreakStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.podIndex": 1,
        "media.ad.podSecond": 21
    }
}
```

### Actie 17 - Ad start {#Action-17}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Begin middelste rol #3 | 46 | 21 | `/api/v1/sessions/{sid}/events` |

Houd de middenrol advertentie bij.

```json
{
    "playerTime": {
        "playhead": 21,
        "ts": "<timestamp>"
    },
    "eventType": "adStart",
    "params": {
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
        "media.ad.creativeURL": "https://example.com",
        "media.ad.placementId": "sample_placement2"
    },
}
```

### Actie 18 - Pingel toevoegen {#Action-18}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| App verzendt ping-gebeurtenis | 50 | 21 | `/api/v1/sessions/{sid}/events` |

Pingel het achterste eind om de 10 seconden.

```json
{
    "playerTime": {
        "playhead": 21,
        "ts": "<timestamp>"
    }, "eventType": "ping"
}
```

### Actie 19 - Toevoeging voltooid {#Action-19}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Track mid-roll advertentie 1 voltooid | 54 | 21 | `/api/v1/sessions/{sid}/events` |

De mid-roll advertentie is compleet.

```json
{
    "playerTime": {
        "playhead": 21,
        "ts": "<timestamp>"
    },
    "eventType": "adComplete"
}
```

### Actie 20 - Einde advertentie {#Action-20}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Halverrol en break bijhouden voltooid | 54 | 21 | `/api/v1/sessions/{sid}/events` |

Het advertentieeinde is voltooid.

```json
{
    "playerTime": {
        "playhead": 21,
        "ts": "<timestamp>"
    },
    "eventType": "adBreakComplete"
}
```

### Actie 21 - Ping {#Action-21}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| App verzendt ping-gebeurtenis | 60 | 27 | `/api/v1/sessions/{sid}/events` |

Pingel het achterste eind om de 10 seconden.

```json
{
    "playerTime": {
        "playhead": 27,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### Actie 22 - Pauze {#Action-22}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Door gebruiker gepauzeerd | 64 | 31 | `/api/v1/sessions/{sid}/events` |

Met de actie van de gebruiker wordt de afspeelstatus verplaatst naar &quot;gepauzeerd&quot;.

```json
{
    "playerTime": {
        "playhead": 31,
        "ts": "<timestamp>"
    },
    "eventType": "pauseStart"
}
```

### Actie 23 - Ping {#Action-23}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| App verzendt ping-gebeurtenis | 70 | 31 | `/api/v1/sessions/{sid}/events` |

Pingel het achterste eind om de 10 seconden. Player bevindt zich nog steeds in de bufferstatus. De gebruiker blijft 20 seconden aan inhoud vastzitten. Fuming...

```json
{
    "playerTime": {
        "playhead": 31,
        "ts": "<timestamp>"
    }, "eventType": "ping"
}
```

### Actie 24 - Afspelen {#Action-24}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Gebruiker heeft op Afspelen gedrukt om de hoofdinhoud te hervatten | 74 | 31 | `/api/v1/sessions/{sid}/events` |

De afspeelstatus verplaatsen naar Afspelen.  **de `play` vraag na a `pauseStart` trekt een &quot;hervattingsvraag&quot;aan het achtereind af,** zodat is er geen behoefte aan een `resume` gebeurtenis.

```json
{
    "playerTime": {
        "playhead": 31,
        "ts": "<timestamp>"
    }, "eventType": "play"
}
```

### Actie 25 - Ping {#Action-25}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| App verzendt ping-gebeurtenis | 80 | 37 | `/api/v1/sessions/{sid}/events` |

Pingel het achterste eind om de 10 seconden.

```json
{
    "playerTime": {
        "playhead": 37,
        "ts": "<timestamp>"
    }, "eventType": "ping"
}
```

### Actie 26 - Sessie voltooid {#Action-26}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| De gebruiker heeft de inhoud tot het einde bekeken. | 88 | 45 | `/api/v1/sessions/{sid}/events` |

Verzend `sessionComplete` naar de achtergrond om aan te geven dat de gebruiker klaar is met het bekijken van de volledige inhoud.

```json
{
    "playerTime": {
        "playhead": 45,
        "ts": "<timestamp>"
    }, "eventType": "sessionComplete"
}
```

>[!NOTE]
>
>**Geen de Gebeurtenissen van het Onderzoek? -** Er is geen expliciete ondersteuning voor `seekStart` - of `seekComplete` -gebeurtenissen in de Media Collection API. Dit is omdat bepaalde spelers een zeer groot aantal dergelijke gebeurtenissen produceren wanneer de eindgebruiker schrobt, en verscheidene honderden gebruikers de netwerkbandbreedte van een backenddienst gemakkelijk konden knelpen. Adobe biedt expliciete ondersteuning voor zoekgebeurtenissen door de hartslagduur te berekenen op basis van de tijdstempel van het apparaat in plaats van de positie van de afspeelkop.
