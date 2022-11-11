---
title: De SDK van Media instellen met JavaScript 3.x
description: Voer de volgende stappen uit om de Media SDK-toepassing in te stellen op JavaScript 3.x.
exl-id: 35e27495-e480-4463-9f00-4b60a54d02c1
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 2%

---

# JavaScript 3.x instellen{#set-up-javascript}

## Vereisten

* **Geldige configuratieparameters verkrijgen**
Deze parameters kunt u verkrijgen van een Adobe-medewerker nadat u uw analyseaccount hebt ingesteld.
* **Implementeren `AppMeasurement` en `Experience Cloud Identity Service` voor JavaScript in uw mediatoepassing**
Zie voor meer informatie [Analyses implementeren met JavaScript](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html) en [Experience Cloud Identity Service implementeren](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-analytics.html).

* **Biedt de volgende mogelijkheden in uw mediaspeler:**

   * *Een API die zich moet abonneren op spelergebeurtenissen* - De SDK van Media vereist dat u een set eenvoudige API&#39;s oproept wanneer gebeurtenissen in de speler plaatsvinden.
   * *Een API die spelerinformatie biedt* - Hier vindt u informatie over het momenteel afspelen van media, advertenties en hoofdstuk.

1. Voeg uw [gedownload](/help/getting-started/download-sdks.md) bibliotheek naar uw project. Maak lokale verwijzingen naar de klassen voor het gemak.

   1. Breid uit `MediaSDK-js-v3*.zip` bestand dat u hebt gedownload.
   1. Controleer of de `MediaSDK.js` bestand bestaat in het dialoogvenster `libs` directory.

   1. De gastheer van `MediaSDK.js` bestand.

      Dit kern-JavaScript-bestand moet worden gehost op een webserver die toegankelijk is voor alle pagina&#39;s op uw site. Voor de volgende stap hebt u het pad naar deze bestanden nodig.

   1. Referentie `MediaSDK.js` op alle sitepagina&#39;s.

      Inclusief `MediaSDK` voor JavaScript door de volgende coderegel toe te voegen in de `<head>` of `<body>` op elke pagina. Bijvoorbeeld:

      ```html
      <script type="text/javascript" src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.js"></script>
      ```

   1. Als u snel wilt controleren of de bibliotheek is geïmporteerd, controleert u `ADB.Media` wordt geëxporteerd op het object Window.

      >[!NOTE]
      >
      >De JavaScript SDK is compatibel met de AMD- en CommonJS-modulespecificaties en `MediaSDK.js` kan ook worden gebruikt met compatibele modulelezers.

1. Een instantie maken van `AppMeasurement` en configureren `visitor`.

   De configuratie van Media SDK vereist een geval van `AppMeasurement` with `visitor` geconfigureerd.

   ```js
    var appMeasurement = new AppMeasurement("<rsid>");
    appMeasurement.visitor = visitor;
    appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net";
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

1. Maak de `MediaTracker` -instantie.

   Nadat u de SDK van Media hebt geconfigureerd, kunnen tracker-instanties voor het bijhouden van media-inhoud worden gemaakt met `getInstance` API.

   ```js
   var tracker = ADB.Media.getInstance();
   ```

   >[!IMPORTANT]
   >
   >Zorg ervoor dat uw `tracker` -instantie is toegankelijk en wordt pas aan het einde van de mediasessie toegewezen. Deze instantie wordt gebruikt voor het bijhouden van alle volgende gebeurtenissen voor die sessie.

## Migreren van JavaScript 2.x naar 3.x

Voor gedetailleerde informatie over het migreren van 2.x naar 3.x, zie [Migratie van 2.x naar 3.x.](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/MigrationGuide.html)
