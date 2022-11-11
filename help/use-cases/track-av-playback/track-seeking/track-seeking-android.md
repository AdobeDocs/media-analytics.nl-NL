---
title: Meer informatie over zoeken bijhouden op Android
description: Leer hoe u de gebeurtenissen Start en Voltooid zoeken kunt bijhouden met de Media SDK op Android.
uuid: 65addd99-eebf-4a80-8b4a-d5fbdff8ab06
exl-id: 8a8fcbcf-3232-4565-8c27-4167b6741613
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---

# Zoeken volgen op Android{#track-seeking-on-android}

De volgende instructies bieden richtlijnen voor implementatie voor alle 2.x SDK&#39;s.

>[!IMPORTANT]
>
>Als u een 1.x-versie van de SDK implementeert, kunt u de 1.x-handleidingen voor ontwikkelaars hier downloaden: [SDK&#39;s downloaden.](/help/getting-started/download-sdks.md)

## Constanten voor reeksspatiëring zoeken

| Naam van constante | Beschrijving     |
|---|---|
| `MediaHeartbeat.Event.SeekStart` | Constante voor het bijhouden van de gebeurtenis Start van zoekopdracht. |
| `MediaHeartbeat.Event.SeekComplete` | Constante voor het bijhouden van de gebeurtenis Seek Complete. |

## Zoeken implementeren

1. Luister naar de afspeelzoekgebeurtenissen van de mediaspeler en volg bij het zoeken de zoekgebeurtenis op zoek naar de zoekfunctie `SeekStart` gebeurtenis:

   ```java
   public void onSeekStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.SeekStart, null, null);
   }
   ```

1. Volg bij het zoeken naar volledige meldingen van de mediaspeler het einde van het zoeken met de `SeekComplete` gebeurtenis:

   ```java
   public void onSeekComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete, null, null);
   }
   ```

Zie het volgende scenario [VOD afspelen met zoeken in de hoofdinhoud](/help/use-cases/tracking-scenarios/vod-seeking.md) voor meer informatie .
