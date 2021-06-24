---
title: Meer informatie over tijdslijnen voor mediatracering � gebruikerssessie wordt verlaten
description: Leer meer over de tijdlijn van de afspeelkop en de bijbehorende � als een videosessie wordt verlaten. Meer informatie over de details van elke actie en elk verzoek.
uuid: 74b89e8f-ef56-4e0c-b9a8-40739e15b4cf
exl-id: 0c6a89f4-7949-4623-8ed9-ce1d1547bdfa
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 5%

---

# Tijdlijn 2 - Gebruiker verlaat sessie {#timeline--2-user-abandons-session}

## VOD, Pre-roll en, mid-roll advertenties, gebruikers laten de inhoud vroeg achter

De volgende diagrammen illustreren de tijdlijn van de afspeelkop en de bijbehorende tijdlijn van de handelingen van een gebruiker. De bijzonderheden van elke actie en de bijbehorende verzoeken worden hieronder weergegeven.


![](assets/va_api_content_2.png)


![](assets/va_api_actions_2.png)


## Handelingsdetails

### Actie 1 - Starten van sessie {#Action-1}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Knop Automatisch afspelen of Afspelen ingedrukt | 0 | 0 | `/api/v1/sessions` |

**Implementatiedetails**

Deze vraag signaleert _het voornemen van de gebruiker om_ een video te spelen. Het keert een identiteitskaart van de Zitting ( `{sid}`) aan de cliënt terug die wordt gebruikt om alle volgende volgende volgende volgende volgende volgende het volgen vraag binnen de zitting te identificeren. De spelerstatus wordt nog niet afgespeeld, maar &#39;gestart&#39;.  [De verplichte ](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) parameters voor sessies moeten in de  `params` kaart in de aanvraaginstantie worden opgenomen.  Op de achtergrond, produceert deze vraag Adobe Analytics in werking stelt vraag in werking.

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
        "analytics.reportSuite": "[ _YOUR-RSID_ ]",
        "analytics.visitorId": "[ _YOUR-VISITOR-ID_ ]",
        "media.contentType": "VOD",
        "media.length": 60.3333333333333,
        "media.id": "VA API Sample Player",
        "visitor.marketingCloudOrgId": "[YOUR-MCID]",
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
| App start gebeurtenistimer | 0 | 0 |  |

**Implementatiedetails**

Start de pingtimer van uw app. De eerste pingel gebeurtenis zou dan 1 seconde binnen moeten in brand steken als er pre-roladvertenties zijn, anders 10 seconden.

### Actie 3 - Ad-break-start {#Action-3}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Begin vóór rol en einde track | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

Pre-roll advertenties moeten worden gevolgd. Advertenties kunnen alleen worden bijgehouden binnen een advertentie-einde.

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adBreakStart, params: {
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

**Implementatiedetails**

Een advertentie van 12 seconden begint.

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
        "media.ad.id": "002",
        "media.ad.length": 7,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "1",
        "media.ad.creativeId": "42",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz-creative.com",
        "media.ad.placementId": "sample-placement2"
    },
}
```

### Actie 5 - Advertentiepunten {#Action-5}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| App verzendt ping-gebeurtenis | 3 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

Pingel de achterkant om de 1 seconde. (Opeenvolgende pingels en pingels worden niet getoond om de korst te houden.)

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
| Volg de voorrol advertentie 1 voltooid | 12 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

De eerste pre-roll advertentie is voorbij.

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

### Actie 7: Ad-einde voltooid {#Action-7}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Track voor rol en break voltooid | 12 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

Het advertentiespoor is voorbij. Tijdens het hele advertentieseizoen is de speler in de &quot;speelstatus&quot; gebleven.

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

### Actie 8 - Inhoud afspelen {#Action-8}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Gebeurtenis track afspelen | 12 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

Verplaats de speler naar de afspeelstatus. begin het volgen van het begin van inhoudsplayback.

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:play,
    qoeData: { bitrate: 10000 }
}
```

### Actie 9 - Pingel {#Action-9}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| App verzendt ping-gebeurtenis | 20 | 8 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

Pingel het achterste eind om de 10 seconden.

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 8ß,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Actie 10 - Ping {#Action-10}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| App verzendt ping-gebeurtenis | 30 | 18 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

Pingel het achterste eind om de 10 seconden.

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 18,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Actie 11 - Fout {#Action-11}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Er treedt een fout op. App verzendt foutgegevens. | 32 | 20 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**


**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 20,
        ts: <timestamp>
    },
    eventType:error
}
```

### Actie 12 - Inhoud afspelen {#Action-12}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Toepassingen herstellen van een fout: de gebruiker drukt op Afspelen | 37 | 20 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**



**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 18,
        ts: <timestamp>
    },
    eventType:play, qoeData: { bitrate: 10000 }
}
```

### Actie 13 - Ping {#Action-13}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| App verzendt ping-gebeurtenis | 40 | 28 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

Pingel het achterste eind om de 10 seconden.

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 28,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Actie 14 - Ad break start {#Action-14}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Begin middelste rol en onderbreking volgen | 45 | 33 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

Midden rol en duur van 8 seconden: `adBreakStart` verzenden.

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 33,
        ts: <timestamp>
    },
    eventType:adBreakStart, params: {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.podIndex": 1,
        "media.ad.podSecond": 33
    }
}
```

### Actie 15 - Ad start {#Action-15}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| Start Midden rol advertentie 1 bijhouden | 45 | 33 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

Houd de middenrol advertentie bij.

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: { playhead: 33, ts: <timestamp>
    },
    eventType:adStart, params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 1",
        "media.ad.id": "002",
        "media.ad.length": 8,
        "media.ad.podPosition": 1,
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

### Handeling 16 - Toepassing sluiten {#Action-16}

| Handeling | Tijdlijn handeling (seconden) | Positie afspeelkop (seconden) | Aanvraag client |
| --- | :---: | :---: | --- |
| De gebruiker sluit de app. De app bepaalt dat de gebruiker de weergave heeft verlaten en niet terugkeert naar deze sessie. | 48 | 33 | `/api/v1/sessions/{sid}/events` |

**Implementatiedetails**

Verzend `sessionEnd` naar de VA-achtergrond om aan te geven dat de sessie onmiddellijk moet worden gesloten, zonder verdere verwerking.

**Voorbeeld van de aanvraaginstantie**

```
{
    playerTime: {
        playhead: 33,
        ts: <timestamp>
    },
    eventType:sessionEnd
}
```
