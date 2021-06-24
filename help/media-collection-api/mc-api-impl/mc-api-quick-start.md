---
title: '"Streaming Media Collection API - Snel starten"'
description: Aan de slag met de API voor streaming media. Leer hoe u uw aanvraaggegevens snel kunt verifiëren.
uuid: ca20bad4-2c8f-406b-833e-b4883a9aa534
exl-id: 08bb5873-f69a-4fdd-8f27-69649b4acb17
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# Snel starten{#quick-start}

>[!TIP]
>
>Verzamel de verzoekgegevens noodzakelijk voor de voltooiing van een succesvol [Sessieverzoek](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) aan de achtergrondserver van de Media Analytics (MA) Collection API. U kunt uw verzoekgegevens snel verifiëren door verzoeken manueel te verzenden (met `curl`, of Postman, enz.). Zo kunt u direct feedback geven over de vraag of er problemen zijn met onjuiste gegevenstypen of onjuiste gegevens in uw aanvraag. Gebruik [JSON bevestigingsschema&#39;s](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) om te verifiëren dat u juiste verzoekgegevens verstrekt.

1. Verzamel de standaard, vereiste Adobe Analytics- en Bezoekergegevens die u moet leveren om een van de Experience Cloud-toepassingen uit te voeren:

   * Bezoeker Experience Cloud Org ID
   * Gebruikersnaam bezoeker Experience Cloud
   * ID Analyserapport
   * URL Analytics Tracking Server

1. Creeer een voorwerp JSON voor uw `sessions` verzoeklichaam, die de minimumgegevens bevatten die voor een succesvolle vraag worden vereist. Bijvoorbeeld:

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
   >U moet de correcte gegevenstypes in het JSON verzoeklichaam gebruiken. `analytics.enableSSL` vereist bijvoorbeeld een booleaanse waarde, `media.length` is numeriek, enzovoort. U kunt parametertypen en verplichte versus optionele vereisten controleren door de [JSON-validatieschema&#39;s te controleren.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

1. Verzend Sessieverzoeken naar het API-eindpunt van de MA-verzameling. Als uw verzoek lading ongeldig is, identificeer het probleem en probeer opnieuw tot u een `201 Created` reactie krijgt. In dit `curl` voorbeeld, is het JSON verzoeklichaam in een dossier genoemd `sample_data_session`:

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

Als [Sessies request](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) slaagt, ontvangt u een `201 Created` reactie gelijkend op hierboven. De reactie bevat een sessie-id in de koptekst Locatie. Identiteitskaart van de Zitting is het cruciale stuk van informatie in de reactie, aangezien het voor alle verdere het volgen vraag wordt vereist. Na een succesvolle terugkeer van [Sessies request](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md), kunt u met vertrouwen doorgaan met het implementeren van video tracking met behulp van de MA API in uw videospeler.
