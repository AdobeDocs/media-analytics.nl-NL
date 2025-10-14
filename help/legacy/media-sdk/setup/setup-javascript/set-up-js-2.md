---
title: Media SDK instellen met JavaScript 2.x
description: Voer de volgende stappen uit om de Media SDK-toepassing in te stellen op JavaScript 2.x.
uuid: 0269d8ad-0af8-4bf1-9d15-e06c2952a005
exl-id: 33976096-8b86-4353-906b-e25bf4693471
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 2%

---

# JavaScript 2.x instellen{#set-up-javascript}

## Vereisten

* **verkrijg geldige configuratieparameters**
Deze parameters kunt u verkrijgen van een Adobe-medewerker nadat u uw analyseaccount hebt ingesteld.
* **voer `AppMeasurement` voor JavaScript in uw media toepassing** uit
Voor meer informatie over de documentatie van Adobe Mobile SDK, zie [&#x200B; het Uitvoeren Analytics die JavaScript gebruiken.](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=nl-NL)

* **verstrek de volgende mogelijkheden in uw media speler:**

   * *API om aan spelergebeurtenissen* in te tekenen - de Media SDK vereist dat u een reeks eenvoudige APIs roept wanneer de gebeurtenissen in uw speler voorkomen.
   * *API die spelerinformatie* verstrekt - Deze informatie omvat details zoals de media naam en de positie van het spelhoofd.

1. Voeg uw [&#x200B; gedownload &#x200B;](/help/getting-started/download-sdks.md) bibliotheek aan uw project toe. Maak lokale verwijzingen naar de klassen voor het gemak.

   1. Vouw het `MediaSDK-js-v2.*.zip` -bestand uit dat u hebt gedownload.
   1. Controleer of het bestand `MediaSDK.min.js` aanwezig is in de map `libs` :

   1. Het `MediaSDK.min.js` -bestand hosten.

      Dit JavaScript-kernbestand moet worden gehost op een webserver die toegankelijk is voor alle pagina&#39;s op uw site. Voor de volgende stap hebt u het pad naar deze bestanden nodig.

   1. Verwijzing `MediaSDK.min.js` op alle sitepagina&#39;s.

      Neem `MediaSDK` op voor JavaScript door de volgende coderegel toe te voegen in de tag `<head>` of `<body>` op elke pagina. Bijvoorbeeld:

      ```
      <script type="text/javascript"
      src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.min.js"></script>
      ```

   1. Instantieer de klasse `ADB.va.MediaHeartbeatConfig` om snel te controleren of de bibliotheek is geïmporteerd.

      >[!NOTE]
      >
      >Vanaf versie 2.1.0 voldoet de JavaScript SDK aan de specificaties van de AMD- en CommonJS-module en kan `VideoHeartbeat.min.js` ook worden gebruikt met compatibele moduleloaders.

1. Voor eenvoudige toegang tot de API&#39;s maakt u lokale verwijzingen naar de `MediaHeartbeat` -klassen.

   ```js
   var MediaHeartbeat = ADB.va.MediaHeartbeat;
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig;
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate;
   ```

1. Maak een `MediaHeartbeatConfig` -instantie.

   Deze sectie helpt u `MediaHeartbeat` configuratieparameters te begrijpen en hoe te om correcte configuratiewaarden op uw `MediaHeartbeat` instantie, voor nauwkeurige het volgen te plaatsen.

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

1. Implementeer het protocol `MediaHeartbeatDelegate` .

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

   Gebruik `MediaHeartbeatConfig` en `MediaHeartbeatDelegate` om de instantie `MediaHeartbeat` te maken.

   ```js
   this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
   ```

   >[!IMPORTANT]
   >
   >Zorg ervoor dat uw `MediaHeartbeat` -instantie toegankelijk is en pas aan het einde van de mediasessie wordt gedealiteerd. Deze instantie wordt gebruikt voor alle volgende gebeurtenissen tracking.

   >[!TIP]
   >
   >`MediaHeartbeat` vereist een instantie van `AppMeasurement` om aanroepen naar Adobe Analytics te verzenden. Hier volgt een voorbeeld van een instantie `AppMeasurement` :

   ```js
   var appMeasurement = new AppMeasurement();
   appMeasurement.visitor = visitor;
   appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net";
   appMeasurement.account = <rsid>;
   appMeasurement.pageName = <page_name>;
   appMeasurement.charSet = "UTF­8";
   ```

## Migreren van JavaScript 1.x naar 2.x

In versie 2.x worden alle methoden van het type public geconsolideerd in de klasse `ADB.va.MediaHeartbeat` , zodat ontwikkelaars deze eenvoudiger kunnen gebruiken. Bovendien worden alle configuraties nu geconsolideerd in de klasse `ADB.va.MediaHeartbeatConfig` .

Raadpleeg de documentatie bij Legacy Implementation voor informatie over het migreren van 1.x naar 2.x.
