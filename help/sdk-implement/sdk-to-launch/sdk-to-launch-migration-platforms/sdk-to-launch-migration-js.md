---
title: '"Migrating from the Standalone Media SDK to Adobe Launch - Web (JS)"'
description: Leer hoe u van de SDK van Media naar Starten voor JS migreert.
exl-id: 19b506b2-3070-4a5e-9732-a5cd0867afde
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 3%

---

# Migreren van de standalone SDK van Media naar Adobe Launch - Web (JS)

## Verschillen in functies

* *Starten*  - De Lancering voorziet u van een UI die u door vestiging, het vormen, en het opstellen van uw web-based media volgende oplossingen loopt. Start verbetert het dynamisch tagbeheer (DTM).
* *Media SDK*  - De Media SDK biedt u bibliotheken voor mediatracering die zijn ontworpen voor specifieke platforms (bijvoorbeeld: Android, iOS, enz.). Adobe raadt Media SDK aan om het mediagebruik in uw mobiele apps te volgen.

## Configuratie

### Standalone Media SDK

In de standalone SDK van Media, vormt u de het volgen configuratie in app
en geeft deze door aan de SDK wanneer u de Beheer maakt.

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

Naast de `MediaHeartbeat` configuratie, moet de pagina vormen en overgaan
de `AppMeasurement`-instantie en `VisitorAPI`-instantie voor mediatracering in volgorde
naar behoren te werken.

### Extensie starten

1. Klik in Experience Platform Launch op het tabblad [!UICONTROL Extensions] voor uw
web-eigenschap.
1. Zoek op het tabblad [!UICONTROL Catalog] de Adobe Media Analytics voor Audio en
Video-extensie en klik op [!UICONTROL Install].
1. In de pagina van de uitbreidingsmontages, vorm de volgende parameters.
De uitbreiding van Media zal de gevormde parameters voor het volgen gebruiken.

   ![](assets/launch_config_js.png)

[Gebruikershandleiding starten - De extensie voor media installeren en configureren](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html#install-and-configure-the-ma-extension)

## Verschillen in het maken van Beheer

### Media-SDK

1. Voeg de bibliotheek van de Analyse van Media aan uw ontwikkelingsproject toe.
1. Creeer een config voorwerp (`MediaHeartbeatConfig`).
1. Voer het afgevaardigde protocol uit, blootstellend `getQoSObject()` en `getCurrentPlaybackTime()` functies.
1. Creeer een instantie van de Hartslag van Media (`MediaHeartbeat`).

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
[Media SDK - Tracker Creation](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/cookbook/sdk-vs-launch-qoe.html) -->

### Starten

De lancering biedt twee benaderingen aan om de volgende infrastructuur te creëren. Beide benaderingen gebruiken de Uitbreiding van de Lancering van Media Analytics:

1. Gebruik de API&#39;s voor mediatracering van een webpagina.

   In dit scenario exporteert de extensie Media Analytics de API&#39;s voor mediatracering naar een geconfigureerde variabele in het globale vensterobject:

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. Gebruik de API&#39;s voor het bijhouden van media van een andere extensie voor Starten.

   In dit scenario, gebruikt u media het volgen APIs die door `get-instance` en `media-heartbeat` Gedeelde Modules worden blootgesteld.

   >[!NOTE]
   >
   >Gedeelde modules zijn niet beschikbaar voor gebruik in webpagina&#39;s. U kunt Gedeelde Modules van een andere uitbreiding slechts gebruiken.

   Creeer een `MediaHeartbeat` instantie gebruikend `get-instance` Gedeelde Module.
Geef een gedelegeerd object door aan `get-instance` dat `getQoSObject()`- en `getCurrentPlaybackTime()`-functies beschikbaar maakt.

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   Open constanten `MediaHeartbeat` via de `media-heartbeat` Gedeelde module.

## Verwante documentatie

### Media-SDK

* [JavaScript 2.x instellen](/help/sdk-implement/setup/setup-javascript/set-up-js-2.md)
* [JavaScript 3.x instellen](/help/sdk-implement/setup/setup-javascript/set-up-js-3.md)
* [Media SDK JS API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

### Starten

* [Overzicht van Launch](https://experienceleague.adobe.com/docs/launch/using/overview.html)
* [Media Analytics-extensie](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)
