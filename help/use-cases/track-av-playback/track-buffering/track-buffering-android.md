---
title: Leer hoe u buffering kunt bijhouden op Android
description: Leer hoe u buffergebeurtenissen kunt bijhouden op Android.
uuid: f16ce76d-1db3-4b51-8c98-54cb781f71d7
exl-id: fcea2ef8-53c5-41fb-8b70-06599c2d9cbf
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# buffering bijhouden op Android{#track-buffering-on-android}

De volgende instructies bieden richtlijnen voor implementatie voor alle 2.x SDK&#39;s.

>[!IMPORTANT]
>Als u een 1.x versie van SDK uitvoert, kunt u de 1.x Gidsen van Ontwikkelaars hier downloaden: [&#x200B; Download SDks.](/help/getting-started/download-sdks.md)

## Constanten voor bufferspatiëring

| Naam van constante | Beschrijving     |
|---|---|
| `MediaHeartbeat.Event.BufferStart` | Constante voor het bijhouden van de bufferstartgebeurtenis |
| `MediaHeartbeat.Event.BufferComplete` | Constante voor het bijhouden van de gebeurtenis Buffer Complete |

## Buffering implementeren

1. Luister naar de buffergebeurtenissen voor het afspelen vanaf de mediaspeler en volg de buffergebeurtenissen bij het starten van de buffer met behulp van de gebeurtenis `BufferStart` :

   ```java
   public void onBufferStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BufferStart, null, null);
   }
   ```

1. Volg bij het verzenden van het volledige bericht over de buffer vanuit de mediaspeler het einde van de buffering met behulp van de gebeurtenis `BufferComplete` :

   ```java
   public void onBufferComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete,null, null);
   }
   ```

Zie het volgende scenario [&#x200B; playback van VOD met het als buffer optreden voor &#x200B;](/help/use-cases/tracking-scenarios/vod-buffering.md) voor meer informatie.
