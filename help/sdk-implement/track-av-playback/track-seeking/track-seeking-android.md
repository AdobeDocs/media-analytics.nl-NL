---
title: Zoeken volgen op Android
description: In dit onderwerp wordt het implementeren van 'seek tracking' beschreven met de Media SDK op Android.
uuid: 65addd99-eebf-4a80-8b4a-d5fbdff8ab06
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Zoeken volgen op Android{#track-seeking-on-android}

>[!IMPORTANT]
>
>De volgende instructies bieden richtlijnen voor implementatie voor alle 2.x SDK&#39;s. Als u een 1.x-versie van de SDK implementeert, kunt u de 1.x-handleidingen voor ontwikkelaars hier downloaden: SDK&#39;s [downloaden.](/help/sdk-implement/download-sdks.md)

## Constanten voor reeksspatiëring zoeken

| Naam van constante | Beschrijving |
|---|---|
| `MediaHeartbeat.Event.SeekStart` | Constante voor het bijhouden van de gebeurtenis Start van zoekopdracht. |
| `MediaHeartbeat.Event.SeekComplete` | Constante voor het bijhouden van de gebeurtenis Seek Complete. |

## Zoeken implementeren

1. Luister naar het afspelen en zoeken van gebeurtenissen van de mediaspeler en volg zoekacties bij het starten van de gebeurtenis via de `SeekStart` gebeurtenis:

   ```java
   public void onSeekStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.SeekStart, null, null); 
   }
   ```

1. Volg bij het zoeken naar volledige meldingen van de mediaspeler het einde van het zoeken met behulp van de `SeekComplete` gebeurtenis:

   ```java
   public void onSeekComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete, null, null); 
   }
   ```

Zie het volgende scenario [VOD playback met het zoeken in de belangrijkste inhoud](/help/sdk-implement/tracking-scenarios/vod-seeking.md) voor meer informatie.
