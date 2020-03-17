---
title: Fouten bijhouden in Chromecast
description: Dit onderwerp beschrijft het uitvoeren van fout het volgen gebruikend Media SDK op Chromecast.
uuid: efa9de8d-c626-4cb6-b46d-108495dd013a
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Fouten bijhouden in Chromecast{#track-errors-on-chromecast}

>[!IMPORTANT]
>
>De volgende instructies bieden richtlijnen voor implementatie voor alle 2.x SDK&#39;s. Als u een 1.x-versie van de SDK implementeert, kunt u de 1.x-handleidingen voor ontwikkelaars hier downloaden: SDK&#39;s [downloaden.](/help/sdk-implement/download-sdks.md)

## Foutopsporing implementeren

1. Fouten met mediaspeler bijhouden: [trackError](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackError)

   ```
   trackError(errorId)
   ```

>[!NOTE]
>
>Fouten bij het bijhouden van mediaspeler stoppen de mediatrackingsessie niet. Als de fout in de mediaspeler voorkomt dat het afspelen wordt voortgezet, controleert u of de sessie voor het bijhouden van media is gesloten door het aanroepen `trackSessionEnd` na het aanroepen `trackError`.

