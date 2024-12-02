---
title: Leer hoe u de kwaliteit van ervaring kunt bijhouden op iOS
description: Leer over het uitvoeren van kwaliteit van ervaring (QoE, QoS) het volgen gebruikend Media SDK op iOS.
uuid: cae2c142-ed39-4234-a711-765dcabc5415
exl-id: 7f01e6eb-95bd-4e3d-93d0-8a2e68323313
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 2ce09eafeb8def909ae2a8ae7cc09a88b2f663af
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 3%

---

# Kwaliteit van ervaring bijhouden op iOS{#track-quality-of-experience-on-ios}

De volgende instructies bieden richtlijnen voor implementatie voor alle 2.x SDK&#39;s.

>[!IMPORTANT]
>
>Als u een 1.x versie van SDK uitvoert, kunt u de 1.x Gidsen van Ontwikkelaars hier downloaden: [ Download SDKs.](/help/getting-started/download-sdks.md)

## QOS implementeren

1. Bepaal wanneer de bitsnelheid verandert tijdens het afspelen van media en maak de `MediaObject` -instantie met behulp van de QoS-informatie.

   QoSObject-variabelen:

   | Variabele | Beschrijving | Vereist |
   | --- | --- | :---: |
   | `bitrate` | Huidige bitsnelheid | Ja |
   | `startupTime` | Opstarttijd | Ja |
   | `fps` | FPS-waarde | Ja |
   | `droppedFrames` | Aantal gedropte frames | Ja |

   >[!TIP]
   >
   >Deze variabelen zijn slechts vereist als u van plan bent om QoS te volgen.

   Maken van QoS-objecten:

   ```
   id qosObject = [ADBMediaHeartbeat createQoSObjectWithBitrate:[BITRATE]
                                     startupTime:[STARTUP_TIME]  
                                     fps:[FPS]  
                                     droppedFrames:[DROPPED_FRAMES]];
   ```

1. Zorg ervoor dat de `getQoSObject` methode de meest bijgewerkte informatie QoS terugkeert.
1. Roep de gebeurtenis `BitrateChange` in de Media Heartbeat-instantie aan wanneer er wordt geschakeld naar een andere bitsnelheid:

   ```
   - (void)onBitrateChange:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBitrateChange  
                        mediaObject:nil  
                        data:nil];
   }
   ```

   >[!IMPORTANT]
   >
   >Werk het object QoS bij en roep de gebeurtenis Bitrate change aan bij elke wijziging in de bitsnelheid. Dit verstrekt de nauwkeurigste gegevens QoS.
