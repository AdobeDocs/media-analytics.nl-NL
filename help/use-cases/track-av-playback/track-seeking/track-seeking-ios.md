---
title: Meer informatie over zoeken volgen op iOS
description: Leer hoe u de gebeurtenissen Start en Voltooien zoeken kunt bijhouden met de Media SDK op iOS.
uuid: 1d31ae99-384f-4b4d-b557-4018db177349
exl-id: e8cb4962-2a14-4bfe-9a25-2405e503ba0b
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---

# Zoeken volgen op iOS{#track-seeking-on-ios}

De volgende instructies bieden richtlijnen voor implementatie voor alle 2.x SDK&#39;s.

>[!IMPORTANT]
>
>Als u een 1.x versie van SDK uitvoert, kunt u de 1.x Gidsen van Ontwikkelaars hier downloaden: [&#x200B; Download SDKs.](/help/getting-started/download-sdks.md)

## Constanten voor bijhouden zoeken

| Naam van constante | Beschrijving     |
|---|---|
| `ADBMediaHeartbeatEventSeekStart` | Constante voor het bijhouden van de gebeurtenis Start van zoekopdracht. |
| `ADBMediaHeartbeatEventSeekComplete` | Constante voor het bijhouden van de gebeurtenis Seek Complete. |

## Zoeken implementeren

1. Luister naar het afspelen van zoekgebeurtenissen van de mediaspeler en volg zoekacties bij het zoeken naar gebeurtenissen via de gebeurtenis `SeekStart` :

   ```
   - (void)onSeekStart:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekStart  
                        mediaObject:nil  
                        data:nil];
   }
   ```

1. Volg bij het zoeken naar volledige meldingen van de mediaspeler het einde van het zoeken met de gebeurtenis `SeekComplete` :

   ```
   - (void)onSeekComplete:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekComplete  
                        mediaObject:nil  
                        data:nil];
   }
   ```

Zie het volgende scenario [&#x200B; de playback van VOD met het zoeken in de belangrijkste inhoud &#x200B;](/help/use-cases/tracking-scenarios/vod-seeking.md) voor meer informatie.
