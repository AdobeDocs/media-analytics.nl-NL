---
title: JavaScript 3.x instellen
description: Installatie van Media SDK-toepassingen voor implementatie op JavaScript 3.x.
exl-id: 35e27495-e480-4463-9f00-4b60a54d02c1
source-git-commit: e56ce73316d9cf00193220df8959a489fc3f2124
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 4%

---

# JavaScript 3.x instellen{#set-up-javascript}

## Vereisten

* **Verkrijg geldige**
configuratieparameters. Deze parameters kunnen bij een Adobe vertegenwoordiger worden verkregen nadat u uw analyseaccount hebt ingesteld.
* **Implementeer  `AppMeasurement` en  `Experience Cloud Identity Service` voor JavaScript in uw mediatoepassingZie Analyses**
implementeren met  [JavaScript en Experience Cloud-identiteitsservice](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html)   [ ](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-analytics.html)implementeren voor meer informatie.

* **Biedt de volgende mogelijkheden in uw mediaspeler:**

   * *Een API die zich moet abonneren op spelergebeurtenissen* . De Media SDK vereist dat u een set eenvoudige API&#39;s aanroept wanneer gebeurtenissen in de speler plaatsvinden.
   * *Een API die spelerinformatie*  verschaft. Dit is informatie over het momenteel afspelen van media, advertenties en hoofdstuk.

1. Voeg uw [gedownloade ](/help/sdk-implement/download-sdks.md#download-3x-sdks) bibliotheek aan uw project toe. Maak lokale verwijzingen naar de klassen voor het gemak.

   1. Vouw het `MediaSDK-js-v3*.zip`-bestand uit dat u hebt gedownload.
   1. Controleer of het `MediaSDK.js`-bestand in de map `libs` aanwezig is.

   1. Het `MediaSDK.js`-bestand hosten.

      Dit kern-JavaScript-bestand moet worden gehost op een webserver die toegankelijk is voor alle pagina&#39;s op uw site. Voor de volgende stap hebt u het pad naar deze bestanden nodig.

   1. Verwijzing `MediaSDK.js` op alle sitepagina&#39;s.

      Neem `MediaSDK` op voor JavaScript door de volgende coderegel toe te voegen in de tag `<head>` of `<body>` op elke pagina. Bijvoorbeeld:

      ```html
      <script type="text/javascript" src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.js"></script>
      ```

   1. Als u snel wilt controleren of de bibliotheek is geïmporteerd, controleert u `ADB.Media` op het object Window.

      >[!NOTE]
      >
      >De JavaScript SDK is compatibel met de AMD- en CommonJS-modulespecificaties en `MediaSDK.js` kan ook worden gebruikt met compatibele modulelezers.

1. Maak een exemplaar van `AppMeasurement` en configureer `visitor`.

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

1. Maak de instantie `MediaTracker`.

   Nadat u de SDK van Media hebt geconfigureerd, kunnen tracker-instanties voor het bijhouden van media-inhoud worden gemaakt met de API `getInstance`.

   ```js
   var tracker = ADB.Media.getInstance();
   ```

   >[!IMPORTANT]
   >
   >Controleer of uw `tracker`-instantie toegankelijk is en pas aan het einde van de mediasessie wordt gedetoewijzingsd. Deze instantie wordt gebruikt voor het bijhouden van alle volgende gebeurtenissen voor die sessie.

## Migreren van JavaScript 2.x naar 3.x

Zie [2.x naar 3.x Migratie](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/MigrationGuide.html) voor gedetailleerde informatie over migreren van 2.x naar 3.x.
