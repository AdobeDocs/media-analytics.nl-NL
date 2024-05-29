---
title: Webgegevens naar Edge verzenden met de SDK van Adobe Experience Platform Web
description: Leer hoe u Adobe Streaming Media-gegevens naar Experience Platform Edge kunt verzenden met de Adobe Experience Platform Web SDK.
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: ad40260d29bd5b739184cb551f084565d05e65a7
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---

# Webgegevens naar Edge verzenden met de SDK van Adobe Experience Platform Web

Vanaf versie 2.20.0 worden de `streamingMedia` onderdeel van de Adobe Experience Platform [Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home) kunt u gegevens verzamelen die betrekking hebben op mediasessies op uw website. De verzamelde gegevens kunnen informatie over media playbacks, pauzes, voltooiing, en andere verwante gebeurtenissen omvatten.

Nadat gegevens zijn verzameld, kunt u deze naar Adobe Experience Platform en/of Adobe Analytics verzenden om rapporten te genereren. Deze functie biedt een uitgebreide oplossing voor het bijhouden en begrijpen van het gedrag van het mediaconsumptie op uw website.

Voor klanten die de Media JS SDK gebruiken, verstrekt het Web SDK een migratieweg om van Media JS SDK aan Web SDK te bewegen, terwijl het omvat steun voor bestaande de functionaliteit van Media JS, zoals het behandelen van media gebeurtenissen.

## Vereisten {#prerequisites}

Als u de opdracht `streamingMedia` component van Web SDK, moet u aan de volgende voorwaarden voldoen:

* Voordat u gegevens van Media Analytics naar Edge kunt verzenden, voert u eerst de stappen in [Media Analytics installeren met Experience Platform Edge](/help/implementation/edge/implementation-edge.md).
* Zorg ervoor dat u toegang hebt tot Adobe Experience Platform en/of Adobe Analytics.
* U moet Web SDK versie 2.20.0 of later gebruiken. Zie de [Overzicht van de installatie van Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview) voor informatie over het installeren van de nieuwste versie.
* De optie **[[!UICONTROL Media Analytics]](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)** voor de gegevensstroom die u gebruikt.
* Zorg ervoor dat het schema dat door uw gegevensstroom wordt gebruikt de het schemagebieden van de Inzameling van Media omvat.
* Vorm de Streaming eigenschap van Media in de configuratie van SDK van het Web, zoals aangetoond in deze pagina, of door [tagextensie](#tag-extension) of via de [JavaScript-bibliotheek](#library).

Voer de stappen uit die in deze pagina worden beschreven om uw Analytics para medios de streaming-implementatie te migreren van Media JS naar Web SDK.

### Stap 1: SDK van Web Experience Platform installeren

Zie de [speciale documentatie](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview) voor meer informatie over het installeren van Web SDK op uw wegeigenschappen.

### Stap 2: Vorm SDK van het Web `streamingMedia` component.

**Voorbeeld**

In het onderstaande fragment ziet u hoe u mediaconcering in Media JS configureert.

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "company.hb-api.omtrdc.net";
mediaConfig.playerName = "player_name";
mediaConfig.channel = "sample_channel";
mediaConfig.appVersion = "app_version";
mediaConfig.debugLogging = true;
mediaConfig.ssl = true;

ADB.Media.configure(mediaConfig, appMeasurement);
```

In plaats daarvan, moet u vormen `streamingMedia` in de Web SDK zoals hieronder wordt geïllustreerd.

```js
alloy("configure", {
  streamingMedia: {
    channel: "sample_channel",
    playerName: "player_name",
    appVersion: "app_version",
    mainPingInterval: 10,
    adPingInterval: 10
  }
});
```

Zie de Web SDK `streamingMedia` component [documentatie](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/configure/streamingmedia) voor volledige details over hoe te om het te vormen.

### Stap 3: Haal de instantie van de mediatracker op wanneer u migreert van de Media JS SDK

Voor klanten die de Media JS SDK gebruiken, verstrekt het Web SDK een migratieweg om van Media JS SDK aan Web SDK te bewegen, terwijl het omvat steun voor bestaande de functionaliteit van Media JS, zoals het behandelen van media gebeurtenissen.

[!DNL Web SDK] bevat een opdracht om een Media Analytics Tracker op te halen. U kunt deze opdracht gebruiken om een objectinstantie te maken en vervolgens dezelfde API&#39;s te gebruiken als de API&#39;s die door de [Media JS-bibliotheek](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html), media-gebeurtenissen volgen.

Zie de [`getMediaAnalyticsTracker`](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/getmediaanalyticstracker) documentatie voor volledige informatie over de ondersteunde methoden.

In het onderstaande fragment ziet u hoe u de instantie van de mediatracker in Media JS kunt ophalen.

```javascript
var tracker = ADB.Media.getInstance();
```

Gebruik in plaats daarvan de opdracht `getMediaAnalyticsTracker` bevel in Web SDK om het zelfde resultaat, zoals hieronder getoond te bereiken.

```js
// aquire Media Analytics APIs
const Media = await window.alloy("getMediaAnalyticsTracker", {});
// create a media tracker instance
const trackerInstance = Media.getInstance();
```

Alle hulpmethoden zijn beschikbaar op de `Media` object. De trackermethoden zijn beschikbaar op de tracker-instantie, zoals hieronder wordt weergegeven.

```js
const mediaInfo = Media.createMediaObject(
  "video name",
  "player video",
  60,
  Media.StreamType.VOD,
  Media.MediaType.Video
);

const contextData = {
  isUserLoggedIn: "false",
  tvStation: "Sample TV station",
  programmer: "Sample programmer",
  assetID: "/uri-reference"
};

// Set standard Video Metadata
contextData[Media.VideoMetadataKeys.Episode] = "Sample Episode";
contextData[Media.VideoMetadataKeys.Show] = "Sample Show";

trackerInstance.trackSessionStart(mediaInfo, contextData);
```
