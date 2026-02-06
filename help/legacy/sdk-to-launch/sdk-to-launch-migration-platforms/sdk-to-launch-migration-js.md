---
title: Migreren van de standalone Media SDK naar Adobe Launch - Web (JS)
description: Leer hoe u van Media SDK naar Launch voor JS migreert.
exl-id: 19b506b2-3070-4a5e-9732-a5cd0867afde
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 8%

---

# Migreren van de stand-alone Media SDK naar Adobe Launch - Web (JS)

>[!NOTE]
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Als gevolg hiervan zijn er verschillende terminologiewijzigingen in de productdocumentatie doorgevoerd. Raadpleeg het volgende [&#x200B; document &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=en) voor een geconsolideerde referentie van de terminologiewijzigingen.

## Verschillen in functies

* *Lancering* - de Lancering voorziet u van een UI die u door vestiging, het vormen, en het opstellen van uw web-based media volgende oplossingen loopt. Launch verbetert bij Dynamic Tag Management (DTM).
* *Media SDK* - de Media SDK voorziet u van media volgende bibliotheken die voor specifieke platforms (bijvoorbeeld: Android, iOS, enz.) worden ontworpen. Adobe raadt Media SDK aan om het mediagebruik in uw mobiele apps te volgen.

## Configuratie

### Standalone Media SDK

In de standalone Media SDK configureert u de trackingconfiguratie in de app
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

Naast de configuratie van `MediaHeartbeat` moet de pagina configureren en doorgeven
de instantie `AppMeasurement` en `VisitorAPI` voor mediatracering in volgorde
naar behoren te werken.

### Extensie starten

1. Klik in Experience Platform Launch op het tabblad [!UICONTROL Extensions] voor uw
web-eigenschap.
1. Zoek op het tabblad [!UICONTROL Catalog] de Adobe Media Analytics voor Audio en
Video-extensie en klik op [!UICONTROL Install] .
1. In de pagina van de uitbreidingsmontages, vorm de volgende parameters.
De uitbreiding van Media zal de gevormde parameters voor het volgen gebruiken.

   ![](assets/launch_config_js.png)

[&#x200B; Gids van de Gebruiker van de Start - installeer en vorm de media uitbreiding &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html#install-and-configure-the-ma-extension)

## Verschillen in het maken van Beheer

### Media-SDK

1. Voeg de bibliotheek van de Analyse van Media aan uw ontwikkelingsproject toe.
1. Creeer een config voorwerp (`MediaHeartbeatConfig`).
1. Implementeer het gedelegeerde protocol en open de functies `getQoSObject()` en `getCurrentPlaybackTime()` .
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

### Starten

De lancering biedt twee benaderingen aan om de volgende infrastructuur te creëren. Beide benaderingen gebruiken de Uitbreiding van de Lancering van de Analyse van Media:

1. Gebruik de API&#39;s voor mediatracering van een webpagina.

   In dit scenario exporteert de extensie Media Analytics de API&#39;s voor mediatracering naar een geconfigureerde variabele in het globale vensterobject:

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. Gebruik de API&#39;s voor het bijhouden van media van een andere extensie voor Starten.

   In dit scenario gebruikt u de API&#39;s voor mediatracering die door de gedeelde modules `get-instance` en `media-heartbeat` worden weergegeven.

   >[!NOTE]
   >
   >Gedeelde modules zijn niet beschikbaar voor gebruik in webpagina&#39;s. U kunt Gedeelde Modules van een andere uitbreiding slechts gebruiken.

   Maak een `MediaHeartbeat` -instantie met de `get-instance` Gedeelde module.
Geef een gedelegeerd object door aan `get-instance` dat `getQoSObject()` - en `getCurrentPlaybackTime()` -functies beschikbaar maakt.

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   Open `MediaHeartbeat` -constanten via de `media-heartbeat` Gedeelde module.

## Verwante documentatie

### Media-SDK

* [JavaScript 2.x instellen](/help/legacy/media-sdk/setup/setup-javascript/set-up-js-2.md)
* [&#x200B; Media SDK JS API &#x200B;](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

### Starten

* [Overzicht van Launch](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html)
* [&#x200B; Uitbreiding van de Analytics van Media &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html)
