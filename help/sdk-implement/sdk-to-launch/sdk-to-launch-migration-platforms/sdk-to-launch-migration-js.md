---
title: Migreren van de standalone SDK van Media naar Adobe Launch - Web (JS)
description: Instructies en codevoorbeelden voor het migreren van de Media SDK naar Launch.
translation-type: tm+mt
source-git-commit: 0f9a985d04969eeca837a2655c666259ce30aee4
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 2%

---


# Migreren van de standalone SDK van Media naar Adobe Launch - Web (JS)

## Verschillen in functies

* *Starten* - De Lancering voorziet u van een UI die u door vestiging, het vormen, en het opstellen van uw web-based media volgende oplossingen loopt. Start verbetert het dynamisch tagbeheer (DTM).
* *Media SDK* - De Media SDK biedt u bibliotheken voor mediatracering die zijn ontworpen voor specifieke platforms (bijvoorbeeld: Android, iOS, enz.). Adobe raadt Media SDK aan om het mediagebruik in uw mobiele apps te volgen.

## Configuratie

### Standalone Media SDK

In de standalone SDK van Media, vormt u de volgende configuratie in appand gaat het tot SDK over wanneer u de trekker creeert.

```javascript
//Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
mediaConfig.trackingServer = "namespace.hb.omtrdc.net";
mediaConfig.playerName = "html5-player";
mediaConfig.channel = "sample-channel";
mediaConfig.ovp = "video-provider";
mediaConfig.appVersion = "v2.0.0"
mediaConfig.ssl = true;
mediaConfig.debugLogging = true;
```

Naast de `MediaHeartbeat` configuratie moet de pagina de instantie en de `AppMeasurement` `VisitorAPI` instantie voor het bijhouden van media configureren en doorgeven om correct te werken.

### Extensie starten

1. Klik in Experience Platform Launch op het [!UICONTROL Extensions] tabblad voor uw webeigenschap.
1. Zoek op het [!UICONTROL Catalog] tabblad de extensie Adobe Media Analytics for Audio and Video en klik op [!UICONTROL Install].
1. In de pagina van de uitbreidingsmontages, vorm de volgende parameters.
De uitbreiding van Media zal de gevormde parameters voor het volgen gebruiken.

   ![](assets/launch_config_js.png)

[Gebruikershandleiding starten - De extensie voor media installeren en configureren](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html#install-and-configure-the-ma-extension)

## Verschillen in het maken van Beheer

### Media-SDK

1. Voeg de bibliotheek van de Analyse van Media aan uw ontwikkelingsproject toe.
1. Maak een config-object (`MediaHeartbeatConfig`).
1. Voer het afgevaardigde protocol uit, blootstellend de `getQoSObject()` en `getCurrentPlaybackTime()` functies.
1. Maak een Media Heartbone-instantie (`MediaHeartbeat`).

```
// Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
...
// Configuration settings
mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER;
...
// Implement Media Delegate (Quality of Service and Playhead)
var mediaDelegate = new MediaHeartbeatDelegate();
...
mediaDelegate.getQoSObject = function() {
    return MediaHeartbeat.createQoSObject(<bitrate>, <startuptime>, <fps>, <droppedFrames>);
    ...
}
...
// Create your tracker
this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
```

<!--  Dead Link - from 2019 - can't locate where this should go
[Media SDK - Tracker Creation](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/cookbook/sdk-vs-launch-qoe.html) -->

### Starten

De lancering biedt twee benaderingen aan om de volgende infrastructuur te creëren. Beide benaderingen gebruiken de Uitbreiding van de Lancering van Media Analytics:

1. Gebruik de API&#39;s voor mediatracering van een webpagina.

   In dit scenario exporteert de extensie Media Analytics de API&#39;s voor mediatracering naar een geconfigureerde variabele in het globale vensterobject:

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. Gebruik de API&#39;s voor het bijhouden van media van een andere extensie voor Starten.

   In dit scenario gebruikt u de API&#39;s voor mediatracering die worden weergegeven door de `get-instance` `media-heartbeat` en de gedeelde modules.

   >[!NOTE]
   >
   >Gedeelde modules zijn niet beschikbaar voor gebruik in webpagina&#39;s. U kunt Gedeelde Modules van een andere uitbreiding slechts gebruiken.

   Maak een `MediaHeartbeat` instantie met de module `get-instance` Gedeeld.
Geef een gedelegeerd object door aan `get-instance` dat functies `getQoSObject()` `getCurrentPlaybackTime()` en functies toegankelijk maakt.

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   Toegang tot `MediaHeartbeat` constanten via de `media-heartbeat` Gedeelde Module.

## Verwante documentatie

### Media-SDK

* [JS instellen](/help/sdk-implement/setup/set-up-js.md)
* [Media SDK JS API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

### Starten

* [Overzicht van starten](https://docs.adobe.com/content/help/en/launch/using/overview.html)
* [Media Analytics-extensie](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)
