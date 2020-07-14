---
title: Gedownloade inhoud bijhouden
description: null
uuid: 0718689d-9602-4e3f-833c-8297aae1d909
translation-type: tm+mt
source-git-commit: be68a7abf7d5fd4cc725b040583801f2308ab066
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---


# Track downloaded content{#track-downloaded-content}

## Overzicht {#overview}

Met de functie Gedownloade inhoud kunt u het mediaconsumptie bijhouden terwijl een gebruiker offline is. Een gebruiker downloadt en installeert bijvoorbeeld een toepassing op een mobiel apparaat en gebruikt de toepassing vervolgens om inhoud te downloaden naar lokale opslag op het apparaat. Adobe heeft de functie Gedownloade inhoud ontwikkeld om de gedownloade gegevens bij te houden. Met deze functie, wanneer de gebruiker inhoud van de opslag van een apparaat speelt, worden het volgen gegevens opgeslagen op het apparaat ongeacht de connectiviteit van het apparaat. Wanneer de gebruiker de playbackzitting voltooit en het apparaat online terugkeert, wordt de opgeslagen het volgen informatie verzonden naar het achterste eind van de inzameling API van Media binnen één enkele lading. De opgeslagen het volgen informatie wordt dan verwerkt en zoals gebruikelijk gerapporteerd in de Inzameling API van Media.

Vergelijk de twee benaderingen:

* Online

   Met deze real-time aanpak verzendt de mediaspeler trackinggegevens voor elke spelergebeurtenis. Het verzendt elke tien seconden (elke seconde voor advertenties) een voor een naar de back-end.

* Off line (functie Gedownloade inhoud)

   Bij deze batchverwerkingsmethode moeten dezelfde sessiegebeurtenissen worden gegenereerd, maar deze worden op het apparaat opgeslagen totdat ze als één sessie naar de back-end worden verzonden (zie het onderstaande voorbeeld).

Elke aanpak heeft zijn voor- en nadelen:
* Het online scenario volgt in real time; dit vereist een connectiviteitscontrole vóór elke netwerkvraag.
* Het off-line scenario (de Gedownloade eigenschap van de Inhoud) vereist slechts één controle van de netwerkconnectiviteit, maar vereist ook een grotere geheugenvoetafdruk op het apparaat.

## Implementatie {#implementation}

### Ondersteunde platforms

Inhoud bijhouden wordt ondersteund op mobiele iOS- en Android-apparaten.

### Gebeurtenisschema&#39;s

De functie Gedownloade inhoud is de offlineversie van de (standaard) online API voor mediagroep. De gebeurtenisgegevens die de speler bijvoegt en naar de back-end verzendt, moeten dus dezelfde gebeurtenisschema&#39;s gebruiken als wanneer u online aanroepen maakt. Voor informatie over deze schema&#39;s, zie:
* [Overzicht;](/help/media-collection-api/mc-api-overview.md)
* [Gebeurtenisaanvragen valideren](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### Volgorde van de gebeurtenissen

* De eerste gebeurtenis in de batch-lading moet `sessionStart` zoals gebruikelijk zijn met de Media Collection API.
* **U moet`media.downloaded: true`**in de standaardmeta-gegevensparameters (sleutel) op de`params``sessionStart`gebeurtenis omvatten om aan het achtereind erop te wijzen dat u gedownloade inhoud verzendt. Als deze parameter niet aanwezig is of op vals wordt geplaatst wanneer u gedownloade gegevens verzendt, zal API een 400 antwoordcode (Onjuiste Verzoek) terugkeren. Deze parameter maakt onderscheid tussen gedownloade en live inhoud naar de back-end. Als deze optie`media.downloaded: true`is ingesteld op een live sessie, resulteert dit ook in een 400 reactie van de API.
* Het is de verantwoordelijkheid van de implementatie om spelergebeurtenissen correct op te slaan in de volgorde waarin ze worden weergegeven.

### Antwoordcodes

* 201 - Gemaakt: Aanvraag met succes; de gegevens zijn geldig en de sessie is gemaakt en wordt verwerkt.
* 400 - Ongeldig verzoek; schemavalidatie is mislukt, alle gegevens worden verwijderd, er worden geen sessiegegevens verwerkt.

## Integratie met Adobe Analtyics {#integration-with-adobe-analtyics}

Bij het berekenen van de Analytics start/close-aanroepen voor het gedownloade inhoudsscenario stelt de back-end een extra Analytics-veld in met de naam `ts.` Dit zijn tijdstempels voor de eerste en laatste ontvangen gebeurtenissen (start en voltooid). Dankzij dit mechanisme kan een voltooide mediasessie op het juiste tijdstip worden geplaatst (zelfs als de gebruiker enkele dagen niet online terugkomt, wordt gemeld dat de mediasessie heeft plaatsgevonden op het moment dat de inhoud daadwerkelijk werd bekeken). U moet dit mechanisme inschakelen op de zijde van Adobe Analytics door een optionele _tijdstempelrapportsuite te maken._ Als u een optionele rapportsuite met tijdstempels wilt inschakelen, raadpleegt u [Tijdstempels optioneel.](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/timestamp-optional.html)

## Samplesessievergelijking {#sample-session-comparison}

```
[url]/api/v1/sessions
```

### Online-inhoud

```
{
  eventType: "sessionStart",
  playerTime: {
    playhead: 0,  
    ts: 1529997923478},  
  params: { /* Standard metadata parameters as documented */ },  
  customMetadata: { /* Custom metadata parameters as documented */ },  
  qoeData: { /* QoE parameters as documented */ }
}
```

### Gedownloade inhoud

```
[{
    eventType: "sessionStart",
    playerTime:{
      playhead: 0,
      ts: 1529997923478},  
    params:{
        "media.downloaded": true
        ...
    },
    customMetadata:{},  
    qoeData:{}
},
    {eventType: "play", playerTime:
        {playhead: 0,  ts: 1529997928174}},
    {eventType: "ping", playerTime:
        {playhead: 10, ts: 1529997937503}},
    {eventType: "ping", playerTime:
        {playhead: 20, ts: 1529997947533}},
    {eventType: "ping", playerTime:
        {playhead: 30, ts: 1529997957545},},
    {eventType: "sessionComplete", playerTime:
        {playhead: 35, ts: 1529997960559}
}]
```

## Referentie voor API voor mediatracker

Zie de API-naslaggids voor [Media tracker voor informatie over het configureren van gedownloade inhoud](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#media-api-reference).
