---
title: Overzicht
description: Fout bij bijhouden met de SDK van Media.
uuid: d71429e6-ef8b-4ea2-8491-ff3cdbf4357f
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Overzicht{#overview}

>[!IMPORTANT]
>
>De volgende instructies bieden richtlijnen voor implementatie voor alle 2.x SDK&#39;s. Als u een 1.x-versie van de SDK implementeert, kunt u de 1.x-handleidingen voor ontwikkelaars hier downloaden: SDK&#39;s [downloaden.](/help/sdk-implement/download-sdks.md)

## Foutopsporing implementeren

1. Fouten met mediaspeler bijhouden.

   Bij foutgebeurtenissen moet u deze aanroepen `trackError` met de foutinformatie.

>[!NOTE]
>
>Fouten bij het bijhouden van mediaspeler stoppen de mediatrackingsessie niet. Als de fout in de mediaspeler voorkomt dat het afspelen wordt voortgezet, controleert u of de sessie voor het bijhouden van media is gesloten door het aanroepen `trackSessionEnd` na het aanroepen `trackError`.

