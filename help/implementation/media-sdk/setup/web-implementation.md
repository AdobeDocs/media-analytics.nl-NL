---
title: Een webimplementatie instellen voor Analytics voor Streaming Media
description: Leer hoe u Adobe Streaming Media voor web-apps implementeert.
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: aed561d0-defc-4be5-87d3-0f331cdfab34
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 1%

---

# Media SDK installeren met JavaScript {#install-web-sdks}

In de informatie op deze pagina wordt beschreven hoe u de zelfstandige webversie van SDK kunt installeren en JavaScript kunt instellen.

Alternatief, kunt u de uitbreiding van de Analyse van de Media van Adobe gebruiken om het stromen media diensten uit te voeren, zoals die in [ wordt beschreven installeer het stromen media diensten gebruikend de uitbreiding van de Analyse van Media ](/help/implementation/media-sdk/setup/web-implementation-tags.md).

## Vereisten {#prerequesites}

* **verkrijg geldige configuratieparameters**

  Deze parameters kunt u verkrijgen van een Adobe-medewerker nadat u uw analyseaccount hebt ingesteld.

* **voer `AppMeasurement` en `Experience Cloud Identity Service` voor JavaScript in uw media toepassing uit**

  Voor meer informatie, zie [ het Uitvoeren Analytics Gebruikend JavaScript ](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=nl-NL) en [ het Uitvoeren van de Dienst van de Identiteit van Experience Cloud ](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-analytics.html?lang=nl-NL).

* **omvat volgende APIs in uw media speler**

   * *API om aan spelergebeurtenissen* in te tekenen - de Media SDK vereist dat u een reeks eenvoudige APIs roept wanneer de gebeurtenissen in uw speler voorkomen.
   * *API die spelerinformatie* verstrekt - dit omvat informatie over momenteel het spelen media, advertenties, en hoofdstuk.

## JavaScript 3.x instellen {#set-up-javascript}

1. Voeg uw [ gedownload ](/help/getting-started/download-sdks.md) bibliotheek aan uw project toe. Maak lokale verwijzingen naar de klassen voor het gemak.

   1. Vouw het `MediaSDK-js-v3*.zip` -bestand uit dat u hebt gedownload.
   1. Controleer of het `MediaSDK.js` -bestand in de map `libs` staat.

   1. Het `MediaSDK.js` -bestand hosten.

      Dit JavaScript-kernbestand moet worden gehost op een webserver die toegankelijk is voor alle pagina&#39;s op uw site. Voor de volgende stap hebt u het pad naar deze bestanden nodig.

   1. Verwijzing `MediaSDK.js` op alle sitepagina&#39;s.

      Neem `MediaSDK` op voor JavaScript door de volgende coderegel toe te voegen in de tag `<head>` of `<body>` op elke pagina. Bijvoorbeeld:

      ```html
      <script type="text/javascript" src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.js"></script>
      ```

   1. Als u snel wilt controleren of de bibliotheek is geïmporteerd, schakelt u `ADB.Media` in op het object Window.

      >[!NOTE]
      >
      >De JavaScript SDK is compatibel met de AMD- en CommonJS-modulespecificaties en `MediaSDK.js` kan ook worden gebruikt met compatibele modulelaadapparaten.

1. Maak een instantie van `AppMeasurement` en configureer `visitor` .

   Voor de configuratie van Media SDK is een instantie van `AppMeasurement` met `visitor` geconfigureerd vereist.

   ```js
    var appMeasurement = new AppMeasurement("<rsid>");
    appMeasurement.visitor = visitor;
    appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net";
   ```

1. Media SDK configureren

   Media SDK moet één keer per webpagina worden geconfigureerd en de configuratie is van toepassing op alle instanties van Beheer die worden gemaakt.

   >[!IMPORTANT]
   >
   > Media SDK (3.x) gebruikt Media Collection API voor het volgen van media die van het eindpunt HB verschillend is dat in 2.x SDKs wordt gebruikt. Neem contact op met je Adobe-vertegenwoordiger voor meer informatie.

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

   Nadat u Media SDK hebt geconfigureerd, kunnen tracker-instanties voor het bijhouden van media-inhoud worden gemaakt met de `getInstance` API.

   ```js
   var tracker = ADB.Media.getInstance();
   ```

   >[!IMPORTANT]
   >
   >Zorg ervoor dat uw `tracker` -instantie toegankelijk is en pas aan het einde van de mediasessie wordt gedealiteerd. Deze instantie wordt gebruikt voor het bijhouden van alle volgende gebeurtenissen voor die sessie.

## Migreren van JavaScript 2.x naar 3.x

Voor gedetailleerde informatie over het migreren van 2.x naar 3.x, zie [ 2.x aan migratie 3.x.](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/MigrationGuide.html)

Voor erfenisinhoud, zie [ uitvoeringen van de Oudheid ](/help/legacy/media-sdk/setup/setup-overview.md)
