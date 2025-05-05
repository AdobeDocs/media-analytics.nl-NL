---
title: Webgegevens naar Edge verzenden met de Adobe Experience Platform Web SDK
description: Leer hoe u Adobe Streaming Media-gegevens naar Experience Platform Edge verzendt met de Adobe Experience Platform Web SDK.
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: de40ebd9-46be-4a52-866f-7bb2589fce28
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# Webgegevens naar Edge verzenden met de Adobe Experience Platform Web SDK

Beginnend met versie 2.20.0, laat de `streamingMedia` component van Adobe Experience Platform [ Web SDK ](https://experienceleague.adobe.com/nl/docs/experience-platform/web-sdk/home) u toe om gegevens te verzamelen met betrekking tot media zittingen op uw website. De verzamelde gegevens kunnen informatie over media playbacks, pauzes, voltooiing, en andere verwante gebeurtenissen omvatten.

Nadat gegevens zijn verzameld, kunt u deze naar Adobe Experience Platform en/of Adobe Analytics verzenden om rapporten te genereren. Deze functie biedt een uitgebreide oplossing voor het bijhouden en begrijpen van het gedrag van het mediaconsumptie op uw website.

Voor klanten die Media JS SDK gebruiken, verstrekt Web SDK een migratieweg om zich van Media JS SDK aan Web SDK te bewegen, terwijl het omvat steun voor bestaande functionaliteit van Media JS, zoals het behandelen van media gebeurtenissen.

## Vereisten {#prerequisites}

Als u de `streamingMedia` -component van Web SDK wilt gebruiken, moet u aan de volgende voorwaarden voldoen:

* Alvorens u het stromen media gegevens naar Edge kunt verzenden, voltooi eerst de stappen in [ installeer de het stromen Inzameling van Media met Experience Platform Edge ](/help/implementation/edge/implementation-edge.md).
* Zorg ervoor dat u toegang hebt tot Adobe Experience Platform en/of Adobe Analytics.
* U moet Web SDK versie 2.20.0 of later gebruiken. Zie het [ de installatieoverzicht van SDK van het Web ](https://experienceleague.adobe.com/nl/docs/experience-platform/web-sdk/install/overview) leren hoe te om de recentste versie te installeren.
* Laat de **[[!UICONTROL Media Analytics]](https://experienceleague.adobe.com/nl/docs/experience-platform/datastreams/configure)** optie voor de gegevensstroom toe u gebruikt.
* Zorg ervoor dat het schema dat door uw gegevensstroom wordt gebruikt de het schemagebieden van de Inzameling van Media omvat.
* Vorm de Streaming eigenschap van Media in de configuratie van SDK van het Web, zoals aangetoond in deze pagina, of door de [ markeringsuitbreiding ](#tag-extension) of door de [ bibliotheek van JavaScript ](#library).

Voer de stappen uit die in deze pagina worden beschreven om uw implementatie van de verzameling van streaming media te migreren van Media JS naar Web SDK.

### Stap 1: Installeer Experience Platform Web SDK

Zie [ specifieke documentatie ](https://experienceleague.adobe.com/nl/docs/experience-platform/web-sdk/install/overview) leren hoe te om SDK van het Web op uw Webeigenschappen te installeren.

### Stap 2: Configureer de Web SDK `streamingMedia` -component.

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

In plaats daarvan moet u de `streamingMedia` -component configureren in de Web SDK, zoals hieronder wordt geïllustreerd.

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

Zie het Web SDK `streamingMedia` component [ documentatie ](https://experienceleague.adobe.com/nl/docs/experience-platform/web-sdk/commands/configure/streamingmedia) voor volledige details over hoe te om het te vormen.

### Stap 3: Haal de instantie van de mediatracker op wanneer u migreert van de Media JS SDK

Voor klanten die Media JS SDK gebruiken, verstrekt Web SDK een migratieweg om zich van Media JS SDK aan Web SDK te bewegen, terwijl het omvat steun voor bestaande functionaliteit van Media JS, zoals het behandelen van media gebeurtenissen.

[!DNL Web SDK] bevat een opdracht voor het ophalen van een Media Analytics Tracker. U kunt dit bevel gebruiken om een objecten instantie tot stand te brengen en dan, gebruikend zelfde APIs zoals die door de [ bibliotheek JS van Media ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html) worden verstrekt, de gebeurtenissen van de spoormedia.

Zie de [`getMediaAnalyticsTracker` ](https://experienceleague.adobe.com/nl/docs/experience-platform/web-sdk/commands/getmediaanalyticstracker) documentatie voor volledige details over de gesteunde methodes.

In het onderstaande fragment ziet u hoe u de instantie van de mediatracker in Media JS kunt ophalen.

```javascript
var tracker = ADB.Media.getInstance();
```

Gebruik in plaats daarvan de opdracht `getMediaAnalyticsTracker` in Web SDK om hetzelfde resultaat te bereiken, zoals hieronder wordt weergegeven.

```js
// aquire Media Analytics APIs
const Media = await window.alloy("getMediaAnalyticsTracker", {});
// create a media tracker instance
const trackerInstance = Media.getInstance();
```

Alle hulpmethoden zijn beschikbaar voor het `Media` -object. De trackermethoden zijn beschikbaar op de tracker-instantie, zoals hieronder wordt weergegeven.

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
