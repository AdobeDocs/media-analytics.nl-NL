---
title: Leer hoe u buffering kunt bijhouden op iOS
description: Leer hoe u buffergebeurtenissen kunt bijhouden op iOS.
uuid: 4f4db23a-489b-4b41-bb6e-393ec64d52a2
exl-id: 5f0a3c4b-7c9e-499d-98d0-6fcf316c4d9c
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# buffering bijhouden op iOS{#track-buffering-on-ios}

De volgende instructies bieden richtlijnen voor implementatie voor alle 2.x SDK&#39;s.

>[!IMPORTANT]
>
>Als u een 1.x-versie van de SDK implementeert, kunt u de 1.x-handleidingen voor ontwikkelaars hier downloaden: [SDK&#39;s downloaden.](/help/getting-started/download-sdks.md)

## Constanten voor bufferspatiëring


| Naam van constante | Beschrijving     |
|---|---|
| `ADBMediaHeartbeatEventBufferStart` | Constante voor het bijhouden van de bufferstartgebeurtenis |
| `ADBMediaHeartbeatEventBufferComplete` | Constante voor het bijhouden van de gebeurtenis Buffer Complete |

## Buffering implementeren

1. Luister naar de buffergebeurtenissen voor het afspelen vanaf de mediaspeler en volg bij een melding van een bufferstart de buffering met de knop `BufferStart` gebeurtenis:

   ```
   - (void)onBufferStart:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferStart  
                        mediaObject:nil  
                        data:nil];
   }
   ```

1. Volg bij het verzenden van het volledige bericht over de buffer vanuit de mediaspeler het einde van de buffering met de `BufferComplete` gebeurtenis:

   ```
   - (void)onBufferComplete:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferComplete  
                        mediaObject:nil  
                        data:nil];
   }
   ```

Zie het volgende scenario [VOD afspelen met bufferen](/help/use-cases/tracking-scenarios/vod-buffering.md) voor meer informatie .
