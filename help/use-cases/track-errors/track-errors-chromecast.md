---
title: Leer hoe u fouten in Chromecast kunt bijhouden
description: Leer over het uitvoeren van fout het volgen gebruikend Media SDK op Chromecast.
uuid: efa9de8d-c626-4cb6-b46d-108495dd013a
exl-id: 513772c2-582d-4b4b-92ed-0c32b99d7fdc
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Fouten bijhouden in Chromecast{#track-errors-on-chromecast}

De volgende instructies bieden richtlijnen voor implementatie voor alle 2.x SDK&#39;s.

>[!IMPORTANT]
>
>Als u een 1.x-versie van de SDK implementeert, kunt u de 1.x-handleidingen voor ontwikkelaars hier downloaden: [SDK&#39;s downloaden.](/help/getting-started/download-sdks.md)

## Foutopsporing implementeren

1. Fouten met mediaspeler bijhouden: [trackError](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackError)

   ```
   trackError(errorId)
   ```

>[!NOTE]
>
>Fouten bij het bijhouden van mediaspeler stoppen de mediatrackingsessie niet. Als de fout in de mediaspeler voorkomt dat het afspelen wordt voortgezet, controleert u of de mediatrackingsessie is gesloten door `trackSessionEnd` na het aanroepen `trackError`.
