---
title: Meer informatie over zoeken bijhouden op Android
description: Leer hoe u de gebeurtenissen Start en Voltooid zoeken kunt bijhouden met de Media SDK op Android.
uuid: 65addd99-eebf-4a80-8b4a-d5fbdff8ab06
exl-id: 8a8fcbcf-3232-4565-8c27-4167b6741613
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---

# Zoeken volgen op Android{#track-seeking-on-android}

>[!IMPORTANT]
>
>De volgende instructies bieden richtlijnen voor implementatie voor alle 2.x SDK&#39;s. Als u een 1.x-versie van de SDK implementeert, kunt u de 1.x-handleidingen voor ontwikkelaars hier downloaden: [SDK&#39;s downloaden.](/help/sdk-implement/download-sdks.md)

## Constanten voor reeksspatiëring zoeken

| Naam van constante | Beschrijving     |
|---|---|
| `MediaHeartbeat.Event.SeekStart` | Constante voor het bijhouden van de gebeurtenis Start van zoekopdracht. |
| `MediaHeartbeat.Event.SeekComplete` | Constante voor het bijhouden van de gebeurtenis Seek Complete. |

## Zoeken implementeren

1. Luister naar het afspelen van zoekgebeurtenissen van de mediaspeler en volg het zoeken naar de gebeurtenis `SeekStart` bij het starten van de zoekgebeurtenis:

   ```java
   public void onSeekStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.SeekStart, null, null); 
   }
   ```

1. Volg bij het zoeken naar volledige meldingen van de mediaspeler het einde van het zoeken met de gebeurtenis `SeekComplete`:

   ```java
   public void onSeekComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete, null, null); 
   }
   ```

Zie het volgende scenario [VOD playback met het zoeken in de belangrijkste inhoud](/help/sdk-implement/tracking-scenarios/vod-seeking.md) voor meer informatie.
