---
title: Snel starten
description: null
uuid: ca20bad4-2c8f-406b-833e-b4883a9aa534
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Snel starten{#quick-start}

>[!TIP]
>
>Verzamel de verzoekgegevens noodzakelijk voor de voltooiing van een succesvol verzoek [van de](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) Zitting aan de achtergrond-eindserver van de Inzameling van Media Analytics (MA). U kunt uw aanvraaggegevens snel verifiëren door aanvragen handmatig te verzenden (met `curl`, of Postman, enz.). Zo kunt u direct feedback geven over de vraag of er problemen zijn met onjuiste gegevenstypen of onjuiste gegevens in uw aanvraag. Gebruik de [JSON-validatieschema](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) &#39;s om te controleren of u de juiste aanvraaggegevens opgeeft.

1. Verzamel de standaard, vereiste gegevens van Adobe Analytics en Visitor die u moet leveren om een of meer van de Experience Cloud-toepassingen uit te voeren:

   * Bezoeker Cloud Org ID
   * Gebruikersnaam voor gebruiker in de cloud
   * ID Analyserapport
   * URL Analytics Tracking Server

1. Creeer een voorwerp JSON voor uw `sessions` verzoeklichaam, dat de minimumgegevens bevat die voor een succesvolle vraag worden vereist. Bijvoorbeeld:

   ```
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
   >U moet de correcte gegevenstypes in het JSON verzoeklichaam gebruiken. Bijvoorbeeld: `analytics.enableSSL` vereist een Booleaanse waarde, `media.length` is numeriek, enzovoort. U kunt parametertypen en verplichte versus optionele vereisten controleren door de [JSON-validatieschema&#39;s te controleren.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

1. Verzend Sessieverzoeken naar het API-eindpunt van de MA-verzameling. Als de lading van uw verzoek ongeldig is, identificeer het probleem en probeer opnieuw tot u een `201 Created` reactie krijgt. In dit `curl` voorbeeld bevindt de JSON-aanvraaginstantie zich in een bestand met de naam `sample_data_session`:

   ```
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

Als het verzoek [van](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) Sessies is geslaagd, ontvangt u een `201 Created` vergelijkbare reactie als hierboven. De reactie bevat een sessie-id in de koptekst Locatie. Identiteitskaart van de Zitting is het cruciale stuk van informatie in de reactie, aangezien het voor alle verdere het volgen vraag wordt vereist. Nadat een [sessieverzoek](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)met succes is geretourneerd, kunt u met vertrouwen doorgaan met het implementeren van videotracering met behulp van de MA API in uw videospeler.
