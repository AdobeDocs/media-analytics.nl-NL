---
title: Leer hoe u fouten kunt bijhouden op Roku
description: Leer over het uitvoeren van fout het volgen gebruikend SDK van Media op Roku.
uuid: 4e0165f9-9169-47ed-9f11-ea8a8778f663
exl-id: 6a6aae4c-60c3-43ea-9954-0bb31f6456f8
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---

# Fouten bijhouden in Roku{#track-errors-on-roku}

De volgende instructies bieden richtlijnen voor implementatie voor alle 2.x SDK&#39;s.

>[!IMPORTANT]
>
> Als u een 1.x-versie van de SDK implementeert, kunt u de 1.x-handleidingen voor ontwikkelaars hier downloaden: [SDK&#39;s downloaden.](/help/getting-started/download-sdks.md)

## Foutopsporing implementeren

1. Fouten met mediaspeler bijhouden:

   ```
   ADBMobile().mediaTrackError(msg.GetMessage(),
                               ADBMobile().ERROR_SOURCE_PLAYER)
   ```

>[!NOTE]
>
>Fouten bij het bijhouden van mediaspeler stoppen de mediatrackingsessie niet. Als de fout in de mediaspeler voorkomt dat het afspelen wordt voortgezet, controleert u of de mediatrackingsessie is gesloten door `trackSessionEnd` na het aanroepen `trackError`.
