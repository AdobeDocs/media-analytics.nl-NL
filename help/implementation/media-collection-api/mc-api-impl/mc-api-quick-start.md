---
title: "Streaming Media Collection API - Snel starten"
description: Aan de slag met de API voor streaming media. Leer hoe u uw aanvraaggegevens snel kunt verifiëren.
uuid: ca20bad4-2c8f-406b-833e-b4883a9aa534
exl-id: 08bb5873-f69a-4fdd-8f27-69649b4acb17
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# Snel starten{#quick-start}

>[!TIP]
>
>Verzamel de aanvraaggegevens die nodig zijn om een geslaagde [Sessieverzoek](../mc-api-ref/mc-api-sessions-req.md) naar de back-endserver van de verzameling-API voor Media Analytics (MA). U kunt uw aanvraaggegevens snel verifiëren door verzoeken handmatig te verzenden (met `curl`, of Postman, enz.). Zo kunt u direct feedback geven over de vraag of er problemen zijn met onjuiste gegevenstypen of onjuiste gegevens in uw aanvraag. Gebruik de [JSON-validatieschema&#39;s](../mc-api-ref/mc-api-json-validation.md) om te verifiëren dat u juiste verzoekgegevens verstrekt.

1. Verzamel de standaard, vereiste Adobe Analytics- en Bezoekergegevens die u moet leveren om een van de Experience Cloud-toepassingen uit te voeren:

   * Bezoeker Experience Cloud Org ID
   * Gebruikersnaam bezoeker Experience Cloud
   * ID Analyserapport
   * URL Analytics Tracking Server

1. Een JSON-object maken voor uw `sessions` verzoek het lichaam, dat de minimumgegevens bevat die voor een succesvolle vraag worden vereist. Bijvoorbeeld:

   ```json
   {
       "playerTime": {
           "playhead": 0,
           "ts": 1234560890123
       },
       "eventType": "sessionStart",
       "params": {
           "media.playerName": "sample-html5-api-player",
           "analytics.trackingServer": "[YOUR_TS]",
           "analytics.reportSuite": "[YOUR_RSID]",
           "media.contentType": "VOD",
           "media.length": 60.39333333333333,
           "media.id": "MA Collection API Sample Player",
           "visitor.marketingCloudOrgId": "[YOUR_ORG_ID]",
           "visitor.marketingCloudUserId": "[YOUR_ECID]",
           "media.name": "ClickMe",
           "media.channel": "sample-channel",
           "media.sdkVersion": "va-api-0.0.0",
           "analytics.enableSSL": false
       }
   }
   ```

   >[!NOTE]
   >
   >U moet de correcte gegevenstypes in het JSON verzoeklichaam gebruiken. bijv. `analytics.enableSSL` een booleaanse waarde vereist, `media.length` is numeriek, enzovoort. U kunt parametertypen en verplichte versus optionele vereisten controleren door de [JSON-validatieschema&#39;s.](mc-api-validate-reqs.md)

1. Verzend Sessieverzoeken naar het API-eindpunt van de MA-verzameling. Als uw aanvraag ongeldig is, identificeert u het probleem en probeert u het opnieuw totdat u een `201 Created` reactie. In dit `curl` De JSON-aanvraaginstantie bevindt zich bijvoorbeeld in een bestand met de naam `sample_data_session`:

   ```sh
   $ curl -i -d \
     @sample_data_session https://{uri}/api/v1/sessions \
     > curl.sessions.out
   
   $ cat curl.sessions.out
   HTTP/1.1 201 Created
   Server: nginx/1.13.5
   Date: Mon, 18 Dec 2017 22:34:12 GMT
   Content-Type: application/octet-stream
   Content-Length: 0
   Connection: keep-alive
   Location: /api/v1/sessions/a39c037641f[...]  # <== Session ID  
   Access-Control-Allow-Origin: *
   Access-Control-Allow-Methods: OPTIONS,POST,PUT
   Access-Control-Allow-Headers: Content-Type
   Access-Control-Expose-Headers: Location
   ```

Als de [Aanvraag voor sessies](../mc-api-ref/mc-api-sessions-req.md) succesvol, u ontvangt `201 Created` dezelfde reactie als hierboven. De reactie bevat een sessie-id in de koptekst Locatie. Identiteitskaart van de Zitting is het cruciale stuk van informatie in de reactie, aangezien het voor alle verdere het volgen vraag wordt vereist. Na een geslaagde terugkeer van een [Aanvraag voor sessies](../mc-api-ref/mc-api-sessions-req.md)kunt u er zeker van zijn dat u verdergaat met het implementeren van videotracering met behulp van de MA API in uw videospeler.
