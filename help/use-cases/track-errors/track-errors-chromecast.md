---
title: Leer hoe u fouten kunt bijhouden op Chromecast
description: Meer informatie over het bijhouden van fouten vindt u in Media SDK on Chromecast.
uuid: efa9de8d-c626-4cb6-b46d-108495dd013a
exl-id: 513772c2-582d-4b4b-92ed-0c32b99d7fdc
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# Fouten bijhouden in Chromecast{#track-errors-on-chromecast}

De volgende instructies bieden richtlijnen voor implementatie voor alle 2.x SDK&#39;s.

>[!IMPORTANT]
>
>Als u een 1.x versie van SDK uitvoert, kunt u de 1.x Gidsen van Ontwikkelaars hier downloaden: [&#x200B; Download SDKs.](/help/getting-started/download-sdks.md)

## Foutopsporing implementeren

1. De fouten van de media speler van het spoor: [&#x200B; trackError &#x200B;](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackError)

   ```
   trackError(errorId)
   ```

>[!NOTE]
>
>Fouten bij het bijhouden van mediaspeler stoppen de mediatrackingsessie niet. Als de fout in de mediaspeler voorkomt dat het afspelen wordt voortgezet, controleert u of de mediatrackingsessie is gesloten door `trackSessionEnd` aan te roepen na het aanroepen van `trackError` .
