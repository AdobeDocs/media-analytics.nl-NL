---
title: Kwaliteit van ervaring bijhouden op iOS
description: Dit onderwerp beschrijft het uitvoeren van kwaliteit van ervaring (QoE, QoS) het volgen gebruikend Media SDK op iOS.
uuid: cae2c142-ed39-4234-a711-765dcabc5415
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Kwaliteit van ervaring bijhouden op iOS{#track-quality-of-experience-on-ios}

>[!IMPORTANT]
>
>De volgende instructies bieden richtlijnen voor implementatie voor alle 2.x SDK&#39;s. Als u een 1.x-versie van de SDK implementeert, kunt u de 1.x-handleidingen voor ontwikkelaars hier downloaden: SDK&#39;s [downloaden.](/help/sdk-implement/download-sdks.md)

## QOS implementeren

1. Bepaal wanneer de bitsnelheid verandert tijdens het afspelen van media en maak de `MediaObject` instantie met behulp van de QoS-informatie.

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
1. Roep de `BitrateChange` gebeurtenis in de Media Heartmaatinstantie aan wanneer bij het afspelen wordt geschakeld naar een andere bitsnelheid:

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

