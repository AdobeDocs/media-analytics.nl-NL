---
title: Hoe te opstelling media SKD gebruikend JavaScript 2.x
description: Voer de volgende stappen uit om de Media SDK-toepassing in te stellen in JavaScript 2.x.
uuid: 0269d8ad-0af8-4bf1-9d15-e06c2952a005
exl-id: 33976096-8b86-4353-906b-e25bf4693471
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 2%

---

# JavaScript 2.x instellen{#set-up-javascript}

## Vereisten

* **Verkrijg geldige**
configuratieparameters. Deze parameters kunnen bij een Adobe vertegenwoordiger worden verkregen nadat u uw analyseaccount hebt ingesteld.
* **Implementeren  `AppMeasurement` voor JavaScript in uw**
mediatoepassing. Zie Analyses  [implementeren met JavaScript voor meer informatie over de documentatie van de Adobe Mobile SDK.](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html)

* **Biedt de volgende mogelijkheden in uw mediaspeler:**

   * *Een API die zich moet abonneren op spelergebeurtenissen* . De Media SDK vereist dat u een set eenvoudige API&#39;s aanroept wanneer gebeurtenissen in de speler plaatsvinden.
   * *Een API die spelerinformatie*  verschaft. Deze informatie bevat details zoals de medianaam en de positie van de afspeelkop.

1. Voeg uw [gedownloade ](/help/sdk-implement/download-sdks.md#download-2x-sdks) bibliotheek aan uw project toe. Maak lokale verwijzingen naar de klassen voor het gemak.

   1. Vouw het `MediaSDK-js-v2.*.zip`-bestand uit dat u hebt gedownload.
   1. Controleer of het `MediaSDK.min.js`-bestand aanwezig is in de map `libs`:

   1. Het `MediaSDK.min.js`-bestand hosten.

      Dit kern-JavaScript-bestand moet worden gehost op een webserver die toegankelijk is voor alle pagina&#39;s op uw site. Voor de volgende stap hebt u het pad naar deze bestanden nodig.

   1. Verwijzing `MediaSDK.min.js` op alle sitepagina&#39;s.

      Neem `MediaSDK` op voor JavaScript door de volgende coderegel toe te voegen in de tag `<head>` of `<body>` op elke pagina. Bijvoorbeeld:

      ```
      <script type="text/javascript"
      src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.min.js"></script>
      ```

   1. Instantieer de klasse `ADB.va.MediaHeartbeatConfig` om snel te controleren of de bibliotheek is geïmporteerd.

      >[!NOTE]
      >
      >Vanaf versie 2.1.0 is de JavaScript SDK compatibel met de specificaties van de AMD- en CommonJS-module en kan `VideoHeartbeat.min.js` ook worden gebruikt met compatibele modulelezers.

1. Voor eenvoudige toegang tot APIs, creeer lokale verwijzingen naar de `MediaHeartbeat` klassen.

   ```js
   var MediaHeartbeat = ADB.va.MediaHeartbeat;
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig;
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate;
   ```

1. Maak een `MediaHeartbeatConfig`-instantie.

   Deze sectie helpt u om `MediaHeartbeat` configuratieparameters te begrijpen en hoe te om correcte configuratiewaarden op uw `MediaHeartbeat` instantie te plaatsen, voor nauwkeurige het volgen.

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

1. Implementeer het `MediaHeartbeatDelegate`-protocol.

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

1. Maak de instantie `MediaHeartbeat`.

   Gebruik `MediaHeartbeatConfig` en `MediaHeartbeatDelegate` om de `MediaHeartbeat` instantie tot stand te brengen.

   ```js
   this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
   ```

   >[!IMPORTANT]
   >
   >Controleer of uw `MediaHeartbeat`-instantie toegankelijk is en pas aan het einde van de mediasessie wordt gedetoewijzingsd. Deze instantie wordt gebruikt voor alle volgende gebeurtenissen tracking.

   >[!TIP]
   >
   >`MediaHeartbeat` vereist een geval van  `AppMeasurement` om vraag naar Adobe Analytics te verzenden. Hier volgt een voorbeeld van een `AppMeasurement`-instantie:

   ```js
   var appMeasurement = new AppMeasurement();
   appMeasurement.visitor = visitor;
   appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net";
   appMeasurement.account = <rsid>;
   appMeasurement.pageName = <page_name>;
   appMeasurement.charSet = "UTF­8";
   ```

## Migreren van JavaScript 1.x naar 2.x

In versie 2.x, worden alle openbare methodes geconsolideerd in de `ADB.va.MediaHeartbeat` klasse om het voor ontwikkelaars gemakkelijker te maken. Bovendien worden alle configuraties nu geconsolideerd in de klasse `ADB.va.MediaHeartbeatConfig`.

Voor gedetailleerde informatie over het migreren van 1.x aan 2.x, zie [VHL 1.x aan Migratie 2.x.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
