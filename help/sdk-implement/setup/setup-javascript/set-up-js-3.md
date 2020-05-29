---
title: JavaScript 3.x instellen
description: Installatie van Media SDK-toepassingen voor implementatie op JavaScript 3.x.
translation-type: tm+mt
source-git-commit: b642bd1a136e62901847f2a8cf004d05282fca01
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 2%

---


# JavaScript 3.x instellen{#set-up-javascript}

## Vereisten

* **Verkrijg geldige configuratieparameters**. Deze parameters kunnen bij een vertegenwoordiger van Adobe worden verkregen nadat u uw analyseaccount hebt ingesteld.
* **Implementeren`AppMeasurement`en`Experience Cloud Identity Service`voor JavaScript in uw mediatoepassing** Zie Analyses [implementeren met JavaScript](https://docs.adobe.com/content/help/en/analytics/implementation/js/overview.html) en Cloud Identity Service [implementeren voor meer informatie.](https://docs.adobe.com/content/help/en/id-service/using/implementation/setup-analytics.html)

* **Biedt de volgende mogelijkheden in uw mediaspeler:**

   * *Een API die zich moet abonneren op spelergebeurtenissen* - De Media SDK vereist dat u een set eenvoudige API&#39;s aanroept wanneer gebeurtenissen in de speler plaatsvinden.
   * *Een API die spelerinformatie* biedt - Dit omvat informatie over het momenteel afspelen van media, advertenties, hoofdstuk.

1. Voeg uw [gedownloade](/help/sdk-implement/download-sdks.md#download-3x-sdks) bibliotheek aan uw project toe. Maak lokale verwijzingen naar de klassen voor het gemak.

   1. Vouw het `MediaSDK-js-v3*.zip` bestand uit dat u hebt gedownload.
   1. Controleer of het `MediaSDK.js` bestand in de `libs` map staat.

   1. Het `MediaSDK.js` bestand hosten.

      Dit kern-JavaScript-bestand moet worden gehost op een webserver die toegankelijk is voor alle pagina&#39;s op uw site. Voor de volgende stap hebt u het pad naar deze bestanden nodig.

   1. Verwijzing `MediaSDK.js` op alle sitepagina&#39;s.

      Neem code op `MediaSDK` voor JavaScript door de volgende coderegel toe te voegen in de `<head>` of `<body>` tag op elke pagina. Bijvoorbeeld:

      ```html
      <script type="text/javascript" src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.js"></script>
      ```

   1. Als u snel wilt controleren of de bibliotheek is geïmporteerd, controleert u of de bibliotheek is geëxporteerd naar een Window-object. `ADB.Media`

      >[!NOTE]
      >
      >De JavaScript SDK is compatibel met de AMD- en CommonJS-modulespecificaties en `MediaSDK.js` kan ook worden gebruikt met compatibele modulelezers.

1. Creeer een geval van `AppMeasurement` en vorm `visitor`.

   De configuratie van Media SDK vereist een geval van `AppMeasurement` met `visitor` gevormd.

   ```js
    var appMeasurement = new AppMeasurement(“<rsid>”);
    appMeasurement.visitor = visitor;
    appMeasurement.trackingServer = “<visitor_namespace>.sc.omtrdc.net”;
   ```

1. SDK van media configureren

   De SDK van media moet één keer per webpagina worden geconfigureerd en de configuratie is van toepassing op alle gemaakte tracker-instanties.

   >[!IMPORTANT]
   >
   > Media SDK (3.x) gebruikt Media Collection API voor het volgen van media die van het eindpunt HB verschillend is dat in 2.x SDKs wordt gebruikt. Neem contact op met uw Adobe-vertegenwoordiger voor meer informatie.

   Hier volgt een voorbeeld van initialisatie van `MediaConfig`:

   ```js
    // Create MediaConfig object (same as above)
    var mediaConfig = new ADB.MediaConfig();
    mediaConfig.trackingServer = Configuration.MEDIA_COLLECTION_ENDPOINT;
    mediaConfig.playerName = Configuration.PLAYER_NAME;
    mediaConfig.channel = Configuration.CHANNEL;
    mediaConfig.appVersion = Configuration.APP_VERSION;
    mediaConfig.debugLogging = false;
    mediaConfig.ssl = true;
   
    ADB.Media.configure(mediaConfig, appMeasurement);
   ```

1. Maak de `MediaTracker` instantie.

   Nadat u de SDK van Media hebt geconfigureerd, kunnen tracker-instanties voor het bijhouden van media-inhoud worden gemaakt met behulp van `getInstance` API.

   ```js
   var tracker = ADB.Media.getInstance();
   ```

   >[!IMPORTANT]
   >
   >Zorg ervoor dat uw `tracker` instantie toegankelijk is en pas aan het einde van de mediasessie wordt gedetoewijzingsd. Deze instantie wordt gebruikt voor het bijhouden van alle volgende gebeurtenissen voor die sessie.

## Migreren van JavaScript 2.x naar 3.x

Voor gedetailleerde informatie over migreren van 2.x naar 3.x, zie Migratie [2.x aan 3.x.](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/MigrationGuide.html)
