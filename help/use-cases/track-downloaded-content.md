---
title: Offline gedownloade inhoud bijhouden in Adobe Streaming Media
description: Leer hoe u de functie Gedownloade inhoud kunt gebruiken om het mediaconsumptie bij te houden wanneer een gebruiker offline is.
uuid: 0718689d-9602-4e3f-833c-8297aae1d909
exl-id: 82d3e5d7-4f88-425c-8bdb-e9101fc1db92
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: cdc5ea361829c749dfbb457288ac5ba51a530961
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 0%

---

# Gedownloade inhoud bijhouden{#track-downloaded-content}

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
* [Overzicht;](/help/implementation/media-collection-api/mc-api-overview.md)
* [Gebeurtenisaanvragen valideren](/help/implementation/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### Volgorde van de gebeurtenissen

* De eerste gebeurtenis in de batch-lading moet `sessionStart` zoals gebruikelijk met de API van de Inzameling van Media.
* **U moet`media.downloaded: true`** in de standaardmetagegevensparameters (`params` key) op de `sessionStart` om aan de achterkant aan te geven dat u gedownloade inhoud verzendt. Als deze parameter niet aanwezig is of op vals wordt geplaatst wanneer u gedownloade gegevens verzendt, zal API een 400 antwoordcode (Onjuiste Verzoek) terugkeren. Deze parameter maakt onderscheid tussen gedownloade en live inhoud naar de back-end. Indien `media.downloaded: true` is ingesteld op een live sessie, resulteert dit ook in een 400-respons van de API.
* Het is de verantwoordelijkheid van de implementatie om spelergebeurtenissen correct op te slaan in de volgorde waarin ze worden weergegeven.

### Antwoordcodes

* 201 - Gemaakt: Aanvraag met succes; de gegevens zijn geldig en de sessie is gemaakt en wordt verwerkt.
* 400 - Ongeldig verzoek; schemavalidatie is mislukt, alle gegevens worden verwijderd, er worden geen sessiegegevens verwerkt.

## Integratie met Adobe Analtyics {#integration-with-adobe-analtyics}

Bij het berekenen van het begin/de dichte vraag van Analytics voor het gedownloade inhoudsscenario, plaatst het achterste eind een extra gebied van Analytics genoemd `ts.` Dit zijn tijdstempels voor de eerste en laatste ontvangen gebeurtenissen (begin en volledig). Dankzij dit mechanisme kan een voltooide mediasessie op het juiste tijdstip worden geplaatst (zelfs als de gebruiker enkele dagen niet online terugkomt, wordt gemeld dat de mediasessie heeft plaatsgevonden op het moment dat de inhoud daadwerkelijk werd bekeken). U moet dit mechanisme aan Adobe Analytics-zijde inschakelen door een _optionele rapportsuite met tijdstempel._ Als u een optionele rapportsuite met tijdstempels wilt inschakelen, raadpleegt u [Tijdstempels optioneel.](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/timestamp-optional.html)

## Samplesessievergelijking {#sample-session-comparison}

### Online-inhoud

```
POST /api/v1/sessions HTTP/1.1

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
POST /api/v1/downloaded HTTP/1.1

[{
    eventType: "sessionStart",
    playerTime:{
      playhead: 0,
      ts: 1529997923478
    },  
    params:{...},
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

### Kennisgeving van veroudering

>[!IMPORTANT]
>
>Gedownloade inhoud kon eerder ook worden verzonden naar `/api/v1/sessions` API. Deze manier om gedownloade inhoud te volgen is **verouderd** en zal **verwijderd** in de toekomst.


De `/api/v1/sessions` API accepteert alleen sessieinitialisatiegebeurtenissen.
Wanneer u de nieuwe API gebruikt, is de vorige vereiste `media.downloaded` markering is niet langer nodig.
We raden u ten zeerste aan de `/api/v1/downloaded` API voor nieuwe gedownloade inhoudsimplementaties, evenals het bijwerken van bestaande implementaties die op oude API baseren.


```
POST /api/v1/sessions HTTP/1.1
[{
    eventType: "sessionStart",
    playerTime:{
      playhead: 0,
      ts: 1529997923478
    },
    params:{
        "media.downloaded": true,
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

Voor informatie over hoe te om gedownloade inhoud te vormen, zie [Referentie voor API voor mediatracker](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/).
