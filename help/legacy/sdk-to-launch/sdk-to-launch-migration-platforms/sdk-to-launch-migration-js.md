---
title: "Migrating from the Standalone Media SDK to Adobe Launch - Web (JS)"
description: Leer hoe u van de SDK van Media naar Starten voor JS migreert.
exl-id: 19b506b2-3070-4a5e-9732-a5cd0867afde
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 3%

---

# Migreren van de standalone SDK van Media naar Adobe Launch - Web (JS)

>[!NOTE]
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=en) voor een geconsolideerde referentie van de terminologische wijzigingen.

## Verschillen in functies

* *Starten* - De lancering voorziet u van een UI die u door vestiging, het vormen, en het opstellen van uw web-based media volgende oplossingen loopt. Launch verbetert bij Dynamic Tag Management (DTM).
* *Media SDK* - De Media SDK biedt u bibliotheken voor mediatracering die zijn ontworpen voor specifieke platforms (bijvoorbeeld: Android, iOS, enz.). Adobe raadt Media SDK aan om het mediagebruik in uw mobiele apps te volgen.

## Configuratie

### Standalone Media SDK

In de standalone SDK van Media, vormt u de het volgen configuratie in app en gaat het tot SDK over wanneer u de trekker creeert.

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

Naast de `MediaHeartbeat` configuratie, moet de pagina vormen en overgaan `AppMeasurement` instantie en `VisitorAPI` -instantie voor het bijhouden van media voor een juiste werking.

### Extensie starten

1. Klik in het Experience Platform Launch op de knop [!UICONTROL Extensions] tabblad voor uw webeigenschap.
1. Op de [!UICONTROL Catalog] , zoekt u de Adobe Media Analytics for Audio and Video-extensie en klikt u op [!UICONTROL Install].
1. In de pagina van de uitbreidingsmontages, vorm de volgende parameters.
De uitbreiding van Media zal de gevormde parameters voor het volgen gebruiken.

   ![](assets/launch_config_js.png)

[Gebruikershandleiding starten - De extensie voor media installeren en configureren](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html#install-and-configure-the-ma-extension)

## Verschillen in het maken van Beheer

### Media-SDK

1. Voeg de bibliotheek van de Analyse van Media aan uw ontwikkelingsproject toe.
1. Een configuratieobject maken (`MediaHeartbeatConfig`).
1. Voer het afgevaardigde protocol uit, blootstellend het `getQoSObject()` en `getCurrentPlaybackTime()` functies.
1. Een instantie van Media Heartboard maken (`MediaHeartbeat`).

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

De lancering biedt twee benaderingen aan om de volgende infrastructuur te creëren. Beide benaderingen gebruiken de Uitbreiding van de Lancering van Media Analytics:

1. Gebruik de API&#39;s voor mediatracering van een webpagina.

   In dit scenario exporteert de extensie Media Analytics de API&#39;s voor mediatracering naar een geconfigureerde variabele in het globale vensterobject:

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. Gebruik de API&#39;s voor het bijhouden van media van een andere extensie voor Starten.

   In dit scenario gebruikt u de API&#39;s voor mediatracering die door de `get-instance` en `media-heartbeat` Gedeelde modules.

   >[!NOTE]
   >
   >Gedeelde modules zijn niet beschikbaar voor gebruik in webpagina&#39;s. U kunt Gedeelde Modules van een andere uitbreiding slechts gebruiken.

   Een `MediaHeartbeat` instantie die de `get-instance` Gedeelde module.
Een gedelegeerd object doorgeven aan `get-instance` die `getQoSObject()` en `getCurrentPlaybackTime()` functies.

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   Toegang `MediaHeartbeat` constanten via de `media-heartbeat` Gedeelde module.

## Verwante documentatie

### Media-SDK

* [JavaScript 2.x instellen](/help/legacy/media-sdk/setup/setup-javascript/set-up-js-2.md)
* [JavaScript 3.x instellen](/help/legacy/media-sdk/setup/setup-javascript/set-up-js-3.md)
* [Media SDK JS API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

### Starten

* [Overzicht van Launch](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html)
* [Media Analytics-extensie](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html)
