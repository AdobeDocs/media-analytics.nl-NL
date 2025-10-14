---
title: API voor streaming media-verzameling - Snel starten
description: Aan de slag met de API voor streaming media. Leer hoe u uw aanvraaggegevens snel kunt verifiëren.
uuid: ca20bad4-2c8f-406b-833e-b4883a9aa534
exl-id: 08bb5873-f69a-4fdd-8f27-69649b4acb17
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# Snel starten{#quick-start}

>[!TIP]
>
>Verzamel de verzoekgegevens noodzakelijk voor de voltooiing van een succesvol [&#x200B; verzoek van de Zitting &#x200B;](../mc-api-ref/mc-api-sessions-req.md) aan de de achterste deelserver van de Inzameling API van de Analyse van Media (MA). U kunt uw aanvraaggegevens snel verifiëren door aanvragen handmatig te verzenden (met `curl` of Postman, enz.). Zo kunt u direct feedback geven over de vraag of er problemen zijn met onjuiste gegevenstypen of onjuiste gegevens in uw aanvraag. Gebruik de [&#x200B; JSON bevestigingsschema&#39;s &#x200B;](../mc-api-ref/mc-api-json-validation.md) om te verifiëren dat u juiste verzoekgegevens verstrekt.

1. Verzamel de standaard, vereiste Adobe Analytics- en Bezoekergegevens die u moet opgeven om een Experience Cloud-toepassing uit te voeren:

   * Bezoeker Experience Cloud Org ID
   * Experience Cloud-gebruikersnaam bezoeker
   * ID Analyserapport
   * URL Analytics Tracking Server

1. Creeer een voorwerp JSON voor uw `sessions` verzoeklichaam, dat de minimumgegevens bevat die voor een succesvolle vraag worden vereist. Bijvoorbeeld:

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
   >U moet de correcte gegevenstypes in het JSON verzoeklichaam gebruiken. `analytics.enableSSL` vereist bijvoorbeeld een Booleaanse waarde, `media.length` is numeriek, enzovoort. U kunt parametertypes en verplichte versus facultatieve vereisten controleren door de [&#x200B; JSON bevestigingsschema&#39;s te controleren.](mc-api-validate-reqs.md)

1. Verzend Sessieverzoeken naar het API-eindpunt van de MA-verzameling. Als uw verzoek ongeldig is, identificeert u het probleem en probeert u het opnieuw totdat u een `201 Created` reactie krijgt. In dit `curl` voorbeeld bevindt de JSON-aanvraagtekst zich in een bestand met de naam `sample_data_session` :

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

Als het [&#x200B; verzoek van zittingen &#x200B;](../mc-api-ref/mc-api-sessions-req.md) slaagt, ontvangt u een `201 Created` reactie gelijkend op hierboven. De reactie bevat een sessie-id in de koptekst Locatie. Identiteitskaart van de Zitting is het cruciale stuk van informatie in de reactie, aangezien het voor alle verdere het volgen vraag wordt vereist. Na een succesvolle terugkeer van het verzoek van a [&#x200B; Sessies &#x200B;](../mc-api-ref/mc-api-sessions-req.md), kunt u met het uitvoeren van video het volgen vertrouwend te werk gaan gebruikend MA API in uw videospeler.
