---
title: De SDK van Media instellen met JavaScript 2.x
description: Voer de volgende stappen uit om de Media SDK-toepassing in te stellen in JavaScript 2.x.
uuid: 0269d8ad-0af8-4bf1-9d15-e06c2952a005
exl-id: 33976096-8b86-4353-906b-e25bf4693471
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 3%

---

# JavaScript 2.x instellen{#set-up-javascript}

## Vereisten

* **Geldige configuratieparameters verkrijgen**
Deze parameters kunt u verkrijgen van een Adobe-medewerker nadat u uw analyseaccount hebt ingesteld.
* **Implementeren `AppMeasurement` voor JavaScript in uw mediatoepassing**
Voor meer informatie over de documentatie van Adobe Mobile SDK, zie [Analyses implementeren met JavaScript.](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=nl-NL)

* **Biedt de volgende mogelijkheden in uw mediaspeler:**

   * *Een API die zich moet abonneren op spelergebeurtenissen* - De SDK van Media vereist dat u een set eenvoudige API&#39;s oproept wanneer gebeurtenissen in de speler plaatsvinden.
   * *Een API die spelerinformatie biedt* - Deze informatie bevat details zoals de medianaam en de positie van de afspeelkop.

1. Voeg uw [gedownload](/help/getting-started/download-sdks.md) bibliotheek naar uw project. Maak lokale verwijzingen naar de klassen voor het gemak.

   1. Breid uit `MediaSDK-js-v2.*.zip` bestand dat u hebt gedownload.
   1. Controleer of de `MediaSDK.min.js` bestand bestaat in het dialoogvenster `libs` map:

   1. De gastheer van `MediaSDK.min.js` bestand.

      Dit kern-JavaScript-bestand moet worden gehost op een webserver die toegankelijk is voor alle pagina&#39;s op uw site. Voor de volgende stap hebt u het pad naar deze bestanden nodig.

   1. Referentie `MediaSDK.min.js` op alle sitepagina&#39;s.

      Inclusief `MediaSDK` voor JavaScript door de volgende coderegel toe te voegen in de `<head>` of `<body>` op elke pagina. Bijvoorbeeld:

      ```
      <script type="text/javascript"
      src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.min.js"></script>
      ```

   1. Als u snel wilt controleren of de bibliotheek is geïmporteerd, instantieert u het dialoogvenster `ADB.va.MediaHeartbeatConfig` klasse.

      >[!NOTE]
      >
      >Vanaf versie 2.1.0 voldoet de JavaScript SDK aan de specificaties van de AMD- en CommonJS-module, en `VideoHeartbeat.min.js` kan ook worden gebruikt met compatibele modulelezers.

1. Voor eenvoudige toegang tot de API&#39;s maakt u lokale verwijzingen naar de `MediaHeartbeat` klassen.

   ```js
   var MediaHeartbeat = ADB.va.MediaHeartbeat;
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig;
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate;
   ```

1. Een `MediaHeartbeatConfig` -instantie.

   Deze sectie helpt u begrijpen `MediaHeartbeat` config parameters en hoe te om correcte config waarden op uw te plaatsen `MediaHeartbeat` voor nauwkeurige tracering.

   Hier volgt een voorbeeld van initialisatie van `MediaHeartbeatConfig`:

   ```js
   //Media Heartbeat initialization
   var mediaConfig = new MediaHeartbeatConfig();
   mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER;
   mediaConfig.playerName = Configuration.PLAYER.NAME;
   mediaConfig.channel = Configuration.HEARTBEAT.CHANNEL;
   mediaConfig.debugLogging = true;
   mediaConfig.appVersion = Configuration.HEARTBEAT.SDK;
   mediaConfig.ssl = false;
   mediaConfig.ovp = Configuration.HEARTBEAT.OVP;
   ```

1. Implementeer de `MediaHeartbeatDelegate` protocol.

   ```js
   var mediaDelegate = new MediaHeartbeatDelegate();
   
   // Replace <currentPlaybackTime> with the video player current playback time
   mediaDelegate.getCurrentPlaybackTime = function() {
       return <currentPlaybackTime>;
   };
   
   // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames> with the current playback QoS values.  
   mediaDelegate.getQoSObject = function() {
       return MediaHeartbeat.createQoSObject(<bitrate>, <startuptime>, <fps>, <droppedFrames>);
   };
   ```

1. Maak de `MediaHeartbeat` -instantie.

   Gebruik de `MediaHeartbeatConfig` en `MediaHeartbeatDelegate` om de `MediaHeartbeat` -instantie.

   ```js
   this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
   ```

   >[!IMPORTANT]
   >
   >Zorg ervoor dat uw `MediaHeartbeat` -instantie is toegankelijk en wordt pas aan het einde van de mediasessie toegewezen. Deze instantie wordt gebruikt voor alle volgende gebeurtenissen tracking.

   >[!TIP]
   >
   >`MediaHeartbeat` vereist een instantie van `AppMeasurement` om oproepen naar Adobe Analytics te verzenden. Hier is een voorbeeld van een `AppMeasurement` instantie:

   ```js
   var appMeasurement = new AppMeasurement();
   appMeasurement.visitor = visitor;
   appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net";
   appMeasurement.account = <rsid>;
   appMeasurement.pageName = <page_name>;
   appMeasurement.charSet = "UTF­8";
   ```

## Migreren van JavaScript 1.x naar 2.x

In versie 2.x worden alle methoden van het type public geconsolideerd in de `ADB.va.MediaHeartbeat` om het voor ontwikkelaars gemakkelijker te maken. Bovendien worden alle configuraties nu geconsolideerd in de `ADB.va.MediaHeartbeatConfig` klasse.

Raadpleeg de documentatie bij Legacy Implementation voor informatie over het migreren van 1.x naar 2.x.
