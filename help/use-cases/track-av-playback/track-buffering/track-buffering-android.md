---
title: Leer hoe u buffering kunt bijhouden op Android
description: Leer hoe u buffergebeurtenissen kunt bijhouden op Android.
uuid: f16ce76d-1db3-4b51-8c98-54cb781f71d7
exl-id: fcea2ef8-53c5-41fb-8b70-06599c2d9cbf
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# Trackbuffering op Android{#track-buffering-on-android}

De volgende instructies bieden richtlijnen voor implementatie voor alle 2.x SDK&#39;s.

>[!IMPORTANT]
>Als u een 1.x-versie van de SDK implementeert, kunt u de 1.x-handleidingen voor ontwikkelaars hier downloaden: [Download SDks.](/help/getting-started/download-sdks.md)

## Constanten voor bufferspatiëring

| Naam van constante | Beschrijving     |
|---|---|
| `MediaHeartbeat.Event.BufferStart` | Constante voor het bijhouden van de bufferstartgebeurtenis |
| `MediaHeartbeat.Event.BufferComplete` | Constante voor het bijhouden van de gebeurtenis Buffer Complete |

## Buffering implementeren

1. Luister naar de buffergebeurtenissen voor het afspelen vanaf de mediaspeler en volg bij een melding van een bufferstart de buffering met de knop `BufferStart` gebeurtenis:

   ```java
   public void onBufferStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BufferStart, null, null);
   }
   ```

1. Volg bij het verzenden van het volledige bericht over de buffer vanuit de mediaspeler het einde van de buffering met de `BufferComplete` gebeurtenis:

   ```java
   public void onBufferComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete,null, null);
   }
   ```

Zie het volgende scenario [VOD afspelen met bufferen](/help/use-cases/tracking-scenarios/vod-buffering.md) voor meer informatie .
