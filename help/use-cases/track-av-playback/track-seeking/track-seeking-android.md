---
title: Meer informatie over zoeken volgen op Android
description: Leer hoe u de gebeurtenissen Start en Voltooien zoeken kunt bijhouden met de Media SDK op Android.
uuid: 65addd99-eebf-4a80-8b4a-d5fbdff8ab06
exl-id: 8a8fcbcf-3232-4565-8c27-4167b6741613
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---

# Zoeken volgen op Android{#track-seeking-on-android}

De volgende instructies bieden richtlijnen voor implementatie voor alle 2.x SDK&#39;s.

>[!IMPORTANT]
>
>Als u een 1.x versie van SDK uitvoert, kunt u de 1.x Gidsen van Ontwikkelaars hier downloaden: [&#x200B; Download SDKs.](/help/getting-started/download-sdks.md)

## Constanten voor bijhouden zoeken

| Naam van constante | Beschrijving     |
|---|---|
| `MediaHeartbeat.Event.SeekStart` | Constante voor het bijhouden van de gebeurtenis Start van zoekopdracht. |
| `MediaHeartbeat.Event.SeekComplete` | Constante voor het bijhouden van de gebeurtenis Seek Complete. |

## Zoeken implementeren

1. Luister naar het afspelen van zoekgebeurtenissen van de mediaspeler en volg zoekacties bij het zoeken naar gebeurtenissen via de gebeurtenis `SeekStart` :

   ```java
   public void onSeekStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.SeekStart, null, null);
   }
   ```

1. Volg bij het zoeken naar volledige meldingen van de mediaspeler het einde van het zoeken met de gebeurtenis `SeekComplete` :

   ```java
   public void onSeekComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete, null, null);
   }
   ```

Zie het volgende scenario [&#x200B; de playback van VOD met het zoeken in de belangrijkste inhoud &#x200B;](/help/use-cases/tracking-scenarios/vod-seeking.md) voor meer informatie.
