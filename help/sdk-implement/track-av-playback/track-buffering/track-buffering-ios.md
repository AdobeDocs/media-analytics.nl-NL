---
title: buffering bijhouden op iOS
description: Beschrijft het bijhouden van buffergebeurtenissen op iOS.
uuid: 4f4db23a-489b-4b41-bb6e-393ec64d52a2
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# buffering bijhouden op iOS{#track-buffering-on-ios}

>[!IMPORTANT]
>
>De volgende instructies bieden richtlijnen voor implementatie voor alle 2.x SDK&#39;s. Als u een 1.x-versie van de SDK implementeert, kunt u de 1.x-handleidingen voor ontwikkelaars hier downloaden: SDK&#39;s [downloaden.](/help/sdk-implement/download-sdks.md)

## Constanten voor bufferspatiëring


| Naam van constante | Beschrijving |
|---|---|
| `ADBMediaHeartbeatEventBufferStart` | Constante voor het bijhouden van de bufferstartgebeurtenis |
| `ADBMediaHeartbeatEventBufferComplete` | Constante voor het bijhouden van de gebeurtenis Buffer Complete |

## Buffering implementeren

1. Luister naar de buffergebeurtenissen voor het afspelen vanaf de mediaspeler en volg de buffering met de `BufferStart` gebeurtenis bij het melden van de buffergebeurtenis:

   ```
   - (void)onBufferStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferStart  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. Volg bij het verzenden van het volledige bericht over de buffer vanuit de mediaspeler het einde van de buffering met behulp van de `BufferComplete` gebeurtenis:

   ```
   - (void)onBufferComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

Zie het volgende scenario [VOD playback met het als buffer optreden](/help/sdk-implement/tracking-scenarios/vod-buffering.md) voor voor meer informatie.
