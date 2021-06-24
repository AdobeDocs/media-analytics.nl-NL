---
title: Uitleg over de kwaliteit van de ervaring
description: Een overzicht van het volgen van kwaliteit van ervaring (QoE, QoS) gebruikend Media SDK.
uuid: 4d73c47f-d0a4-4228-9040-d6432311c9eb
exl-id: af5f3372-a9a5-46ea-9c2f-81b0f5c96ccf
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 2%

---

# Overzicht{#overview}

>[!IMPORTANT]
>
>De volgende instructies bieden richtlijnen voor implementatie voor alle 2.x SDK&#39;s. Als u een 1.x-versie van de SDK implementeert, kunt u de 1.x-handleidingen voor ontwikkelaars hier downloaden: [SDK&#39;s downloaden.](/help/sdk-implement/download-sdks.md)

De kwaliteit van ervaring het volgen omvat kwaliteit van de dienst (QoS) en fout het volgen, allebei facultatieve elementen zijn en **niet** vereist voor kernmedia het volgen implementaties. U kunt de mediaspeler-API gebruiken om de variabelen met betrekking tot QoS en foutcontrole te identificeren. Hier volgen de belangrijkste elementen van de kwaliteit van ervaring:

## Gebeurtenissen van Player {#player-events}

### Op om het even welke metrische veranderingen QoS:

Maak of werk de instantie van het object QoS bij voor het afspelen. [QoS API-naslaggids](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createQoSObject)

### Bij alle gebeurtenissen die betrekking hebben op bitsnelheden

`trackEvent(Media.Heartbeat.Event.BitrateChange);` aanroepen

## QOS implementeren

1. Identificeer wanneer om het even welke metriek QOS tijdens media playback veranderen, creeer `MediaObject` gebruikend de informatie QoS, en werk de nieuwe informatie QoS bij.

   QoSObject-variabelen:

   >[!TIP]
   >
   >Deze variabelen zijn slechts vereist als u van plan bent om QoS te volgen.

   | Variabele | Beschrijving | Vereist |
   | --- | --- | :---: |
   | `bitrate` | Huidige bitsnelheid | Ja |
   | `startupTime` | Opstarttijd | Ja |
   | `fps` | FPS-waarde | Ja |
   | `droppedFrames` | Aantal gedropte frames | Ja |

1. Zorg ervoor dat `getQoSObject()` de methode de meest bijgewerkte informatie QoS terugkeert.
1. Wanneer de playbackschakelaars bitrates, roep de `BitrateChange` gebeurtenis in de instantie van de Hartslag van Media.

   >[!IMPORTANT]
   >
   >Werk het object QoS bij en roep de gebeurtenis Bitrate change aan bij elke wijziging in de bitsnelheid. Dit verstrekt de nauwkeurigste gegevens QoS.

In de volgende voorbeeldcode wordt de JavaScript 2.x SDK gebruikt voor een HTML5-mediaspeler. Gebruik deze code met de afspeelcode voor de kernmedia.

```js
var mediaDelegate = new MediaHeartbeatDelegate(); 
...  
 
// This is called periodically by MediaHeartbeat instance 
mediaDelegate.prototype.getQoSObject = function() { 
    return this.qosInfo; 
}; 
 
if (e.type == "qos_update") { 
    var qosInfo = MediaHeartbeat.createQoSObject(<BITRATE>,<STARTUP_TIME>,<FPS>,<DROPPED_FRAMES>); 
    mediaDelegate.qosInfo = qosInfo; 
}; 
 
if (e.type == "bitrate_change") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, qosObject); 
};
```
