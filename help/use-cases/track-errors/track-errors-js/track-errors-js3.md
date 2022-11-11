---
title: Leer hoe u fouten kunt bijhouden met JavaScript 3.x
description: Leer hoe u fouten kunt bijhouden met de SDK van Media in browser-apps (JS).
exl-id: 3769fc47-fbc4-4498-9d2a-04c88cdd0e83
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# Fouten bijhouden met JavaScript 3.x{#track-errors-on-javascript}

De volgende instructies bieden richtlijnen voor implementatie voor alle 2.x SDK&#39;s.

>[!IMPORTANT]
>
>Als u eerdere versies van de SDK implementeert, kunt u de ontwikkelaarsgidsen hier downloaden: [SDK&#39;s downloaden.](/help/getting-started/download-sdks.md)

## Foutopsporing implementeren

1. Fouten met mediaspeler bijhouden:

   ```js
   onPlayerError = function() {
       tracker.trackError("errorId");
   };
   ```

>[!NOTE]
>
>Fouten bij het bijhouden van mediaspeler stoppen de mediatrackingsessie niet. Als de fout in de mediaspeler voorkomt dat het afspelen wordt voortgezet, controleert u of de mediatrackingsessie is gesloten door `trackSessionEnd` na het aanroepen `trackError`.
