---
title: '"Migreren van de standalone Media SDK naar Adobe Launch - Android"'
description: Leer hoe u van de SDK van Media naar Starten voor Android migreert.
exl-id: 26764835-4781-417b-a6c0-ea6ae78d76ae
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# Migreren van de standalone Media SDK naar Adobe Launch - Android

## Configuratie

### Standalone Media SDK

In de standalone SDK van Media, vormt u het volgen in app en gaat het tot
de SDK wanneer u de Beheer maakt.

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

1. Klik in Experience Platform Launch op het tabblad [!UICONTROL Extensions] voor uw
eigenschap mobile.
1. Zoek op het tabblad [!UICONTROL Catalog] de Adobe Media Analytics for Audio
en Video-extensie en klik op [!UICONTROL Install].
1. In de pagina van de uitbreidingsmontages, vorm de volgende parameters.
De uitbreiding van Media zal de gevormde parameters voor het volgen gebruiken.

![](assets/launch_config_mobile.png)

[Mobiele extensies gebruiken](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

## Beheer maken

### Standalone Media SDK

In de standalone SDK van Media maakt u handmatig het `MediaHeartbeatConfig`-object
en configureert u de volgende parameters. Implementeer de gedelegeerde interface die blootstelt
`getQoSObject()` en `getCurrentPlaybackTime()functions.`
Maak een `MediaHeartbeat`-instantie om te volgen.

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

Voordat u de Beheer maakt, moet u de media-extensie registreren en
afhankelijke extensies met de mobiele kern.

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
`MediaHeartbeartDelegate` interface tijdens het creëren van de trekker.  De uitvoering
zou recentste QoE en playhead moeten terugkeren telkens als de trekker de
`getQoSObject()` en `getCurrentPlaybackTime()` interfacemethoden.

### Extensie starten

De huidige afspeelkop van de speler moet in de implementatie worden bijgewerkt door de
`updateCurrentPlayhead` methode blootgesteld door de trekker. Voor nauwkeurige tracering
u zou deze methode minstens eens per seconde moeten roepen.

[Referentie voor media-API: huidige speler bijwerken](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updatecurrentplayhead)

De implementatie moet de QoE-informatie bijwerken door `updateQoEObject` aan te roepen
door de verklikker aan het licht gebrachte methode. We verwachten dat deze methode altijd wordt gebruikt
Dit is een wijziging in de kwaliteitswaarden.

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
