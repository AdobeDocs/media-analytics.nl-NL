---
title: Meer informatie over het bijhouden van fouten op iOS
description: Meer informatie over het bijhouden van fouten met de Media SDK op iOS.
uuid: 18ea93d3-5948-4375-bcdb-72309268e38d
exl-id: c4ce7092-a102-41da-80a6-a4359f925708
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---

# Fouten bijhouden op iOS{#track-errors-on-ios}

De volgende instructies bieden richtlijnen voor implementatie voor alle 2.x SDK&#39;s.

>[!IMPORTANT]
>
>Als u een 1.x-versie van de SDK implementeert, kunt u de 1.x-handleidingen voor ontwikkelaars hier downloaden: [SDK&#39;s downloaden.](/help/getting-started/download-sdks.md)

## Foutopsporing implementeren

1. Fouten met mediaspeler bijhouden:

   ```
   - (void)onPlayerError:(NSNotification *)notification {
       [_mediaHeartbeat trackError:@"mediaoErrorId"];
   }
   ```

>[!NOTE]
>
>Fouten bij het bijhouden van mediaspeler stoppen de mediatrackingsessie niet. Als de fout in de mediaspeler voorkomt dat het afspelen wordt voortgezet, controleert u of de mediatrackingsessie is gesloten door `trackSessionEnd` na het aanroepen `trackError`.
