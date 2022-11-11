---
title: Leer hoe u fouten kunt bijhouden met JavaScript 2.x
description: Leer hoe u fouten kunt bijhouden met de SDK van Media in browser-apps (JS).
uuid: 5a4fc5df-2677-4189-92af-5cd074847b39
exl-id: b3012bce-4b92-408e-8b7a-57ae9d52e93d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# Fouten bijhouden met JavaScript 2.x{#track-errors-on-javascript}

De volgende instructies bieden richtlijnen voor implementatie voor alle 2.x SDK&#39;s.

>[!IMPORTANT]
>
>Als u een 1.x-versie van de SDK implementeert, kunt u de 1.x-handleidingen voor ontwikkelaars hier downloaden: [SDK&#39;s downloaden.](/help/getting-started/download-sdks.md)

## Foutopsporing implementeren

1. Fouten met mediaspeler bijhouden:

   ```js
   onPlayerError = function() {
       this._mediaHeartbeat.trackError("mediaErrorId");
   };
   ```

>[!NOTE]
>
>Fouten bij het bijhouden van mediaspeler stoppen de mediatrackingsessie niet. Als de fout in de mediaspeler voorkomt dat het afspelen wordt voortgezet, controleert u of de mediatrackingsessie is gesloten door `trackSessionEnd` na het aanroepen `trackError`.
