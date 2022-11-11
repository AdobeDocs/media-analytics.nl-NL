---
title: "Migreren van de standalone Media SDK naar Adobe Launch - Android"
description: Leer hoe u van de SDK van Media naar Starten voor Android migreert.
exl-id: 26764835-4781-417b-a6c0-ea6ae78d76ae
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# Migreren van de standalone Media SDK naar Adobe Launch - Android

>[!NOTE]
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=en) voor een geconsolideerde referentie van de terminologische wijzigingen.


## Configuratie

### Standalone Media SDK

In de standalone SDK van Media, vormt u het volgen in app, en gaat het tot SDK over wanneer u de trekker creeert.

```java
MediaHeartbeatConfig config = new MediaHeartbeatConfig();
config.trackingServer = "namespace.hb.omtrdc.net";
config.channel = "sample-channel";
config.appVersion = "v2.0.0";
config.ovp = "video-provider";
config.playerName = "native-player";
config.ssl = true;
config.debugLogging = true;

MediaHeartbeat tracker = new MediaHeartbeat(... , config);
```

### Extensie starten

1. Klik in het Experience Platform Launch op de knop [!UICONTROL Extensions] tabblad voor uw eigenschap mobile.
1. Op de [!UICONTROL Catalog] , zoekt u de Adobe Media Analytics for Audio and Video-extensie en klikt u op [!UICONTROL Install].
1. In de pagina van de uitbreidingsmontages, vorm de volgende parameters.
De uitbreiding van Media zal de gevormde parameters voor het volgen gebruiken.

![](assets/launch_config_mobile.png)

[Mobiele extensies gebruiken](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

## Beheer maken

### Standalone Media SDK

In de standalone SDK van Media maakt u handmatig de `MediaHeartbeatConfig` en configureert u de volgende parameters. Implementeer de gedelegeerde interface die blootstelt
`getQoSObject()` en `getCurrentPlaybackTime()functions.`
Een `MediaHeartbeat` -instantie voor reeksspatiëring.

```java
MediaHeartbeatConfig config = new MediaHeartbeatConfig();
config.trackingServer = "namespace.hb.omtrdc.net";
config.channel = "sample-channel";
config.appVersion = "v2.0";
config.ovp = "video-provider";
config.playerName = "native-player";
config.ssl = true;
config.debugLogging = true;

MediaHeartbeatDelegate delegate = new MediaHeartbeatDelegate() {
    @Override
    public MediaObject getQoSObject() {
        // When called should return the latest qos values.
        return MediaHeartbeat.createQoSObject(<bitrate>,  
                                              <startupTime>,  
                                              <fps>,  
                                              <droppedFrames>);
    }

    @Override
    public Double getCurrentPlaybackTime() {
        // When called should return the current player time in seconds.
        return <currentPlaybackTime>;
    }

    MediaHeartbeat tracker = new MediaHeartbeat(delegate, config);
}
```

### Extensie starten

[Referentie voor media-API - Een mediabeheer maken](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#create-a-media-tracker)

Voordat u Beheer maakt, moet u de media-extensie en afhankelijke extensies registreren bij de mobiele kern.

```java
// Register the extension once during app launch
try {
    // Media needs Identity and Analytics extension
    // to function properly
    Identity.registerExtension();
    Analytics.registerExtension();

    // Initialize media extension.
    Media.registerExtension();                
    MobileCore.start(new AdobeCallback () {
        @Override
        public void call(Object o) {
            // Launch mobile property to pick extension settings.
            MobileCore.configureWithAppID("LAUNCH_MOBILE_PROPERTY");
        }
    });
} catch (InvalidInitException ex) {
    ...
}
```

Wanneer u de media-extensie hebt geregistreerd, maakt u de tracker met behulp van de volgende API.
Tracker selecteert automatisch de configuratie van het gevormde lanceringsbezit.

```java
Media.createTracker(new AdobeCallback<MediaTracker>() {
    @Override
    public void call(MediaTracker tracker) {
        // Use the instance for tracking media.
    }
});
```

## Waarden voor afspeelkop en kwaliteit van ervaring bijwerken.

### Standalone Media SDK

In de standalone SDK van Media, gaat u een afgevaardigde voorwerp over dat uitvoert
`MediaHeartbeartDelegate` interface tijdens het maken van tracker.  De implementatie zou recentste QoE en playhead moeten terugkeren telkens als de trekker de
`getQoSObject()` en `getCurrentPlaybackTime()` interfacemethoden.

### Extensie starten

De huidige afspeelkop van de speler moet in de implementatie worden bijgewerkt door de
`updateCurrentPlayhead` door de verklikker aan het licht gebrachte methode. Voor het nauwkeurig volgen zou u deze methode minstens eens per seconde moeten roepen.

[Referentie voor media-API: huidige speler bijwerken](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updatecurrentplayhead)

De implementatie moet de QoE-informatie bijwerken door de `updateQoEObject`
door de verklikker aan het licht gebrachte methode. We verwachten dat deze methode wordt aangeroepen wanneer de kwaliteitswaarden veranderen.

[Referentie voor media-API - QoE-object bijwerken](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updateqoeobject)

## Standaardmedia/metagegevens doorgeven

### Standalone Media SDK

* Metagegevens standaardmedia:

   ```java
   MediaObject mediaInfo =
     MediaHeartbeat.createMediaObject("media-name",
                                      "media-id",
                                      60D,
                                      MediaHeartbeat.StreamType.VOD,
                                      MediaHeartbeat.MediaType.Video);
   
   // Standard metadata keys provided by adobe.
   Map <String, String> standardVideoMetadata =
     new HashMap<String, String>();
   standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.EPISODE,
                             "Sample Episode");
   standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SHOW,
                             "Sample Show");
   standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SEASON,
                             "Sample Season");
   mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardMediaMetadata,
                      standardVideoMetadata);
   
   // Custom metadata keys
   HashMap<String, String> mediaMetadata = new HashMap<String, String>();
   mediaMetadata.put("isUserLoggedIn", "false");
   mediaMetadata.put("tvStation", "Sample TV Station");
   tracker.trackSessionStart(mediaInfo, mediaMetadata);
   ```

* Standaard advertentiemetagegevens:

   ```java
   MediaObject adInfo =
     MediaHeartbeat.createAdObject("ad-name",
                                   "ad-id",
                                   1L,
                                   15D);
   
   // Standard metadata keys provided by adobe.
   Map <String, String> standardAdMetadata =
     new HashMap<String, String>();
   standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER,
                          "Sample Advertiser");
   standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID,
                          "Sample Campaign");
   adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata,
                   standardAdMetadata);
   
   HashMap<String, String> adMetadata =
     new HashMap<String, String>();
   adMetadata.put("affiliate",
                  "Sample affiliate");
   
   tracker.trackEvent(MediaHeartbeat.Event.AdStart,
                      adObject,
                      adMetadata);
   ```

### Extensie starten

* Metagegevens standaardmedia:

   ```java
   HashMap<String, Object> mediaObject =
     Media.createMediaObject("media-name",
                             "media-id",
                             60D,
                             MediaConstants.StreamType.VOD,
                             Media.MediaType.Video);
   
   HashMap<String, String> mediaMetadata =
     new HashMap<String, String>();
   
   // Standard metadata keys provided by adobe.
   mediaMetadata.put(MediaConstants.VideoMetadataKeys.EPISODE,
                     "Sample Episode");
   mediaMetadata.put(MediaConstants.VideoMetadataKeys.SHOW,
                     "Sample Show");
   
   // Custom metadata keys
   mediaMetadata.put("isUserLoggedIn", "false");
   mediaMetadata.put("tvStation", "Sample TV Station");
   
   tracker.trackSessionStart(mediaInfo, mediaMetadata);
   ```

* Standaard advertentiemetagegevens:

   ```java
   HashMap<String, Object> adObject =
     Media.createAdObject("ad-name",
                          "ad-id",
                          1L,
                          15D);
   HashMap<String, String> adMetadata =
     new HashMap<String, String>();
   
   // Standard metadata keys provided by adobe.
   adMetadata.put(MediaConstants.AdMetadataKeys.ADVERTISER,
                  "Sample Advertiser");
   adMetadata.put(MediaConstants.AdMetadataKeys.CAMPAIGN_ID,
                  "Sample Campaign");
   
   // Custom metadata keys
   adMetadata.put("affiliate",
                  "Sample affiliate");
   _tracker.trackEvent(Media.Event.AdStart,
                       adObject,
                       adMetadata);
   ```
