---
title: Testen 2 Onderbreking media
description: Meer informatie over de mediaverstoring die wordt gebruikt bij validatie.
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
exl-id: 3f22ce2d-4385-4a3b-8d1f-52e25a9b1101
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# Test 2: Onderbreking media{#test-media-interruption}

Deze testcase valideert het gedrag van mobiele onderbrekingen.

## Testprocedure

U moet deze taken in de volgende volgorde voltooien en opnemen:

1. **De mediaspeler starten**

   Wanneer de mediaspeler start, worden de volgende aanroepen in de volgende volgorde verzonden:

   1. Start Adobe Analytics (AppMeasurement)
   1. Start van media-analyse (hartslagen)
   1. Media Analytics (heartbeats) Aanvraag voor Adobe Analytics Start aangevraagd

   De eerste twee bovenstaande aanroepen bevatten aanvullende metagegevens en variabelen. Voor vraagparameters en meta-gegevens, zie [de vraagdetails van de test.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   De derde vraag hierboven vertelt de server van de Analyse van Media dat de Media SDK verzocht om de vraag van het Begin van Adobe Analytics (`pev2=ms_s`) naar de server van Adobe Analytics wordt verzonden.

1. **De belangrijkste inhoud van het spel gedurende minstens 5 minuten ononderbroken**

   **Inhoud afspelen**

   Tijdens het afspelen van inhoud verzendt de Media SDK afspeelaanroepen (hartslagen) naar de Media Analytics-server om de tien seconden.

   Voor vraagparameters en meta-gegevens, zie [de vraagdetails van de test.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

   Zie ook de instructies [Trackadvertenties](/help/sdk-implement/track-ads/track-ads-overview.md) van uw platform voor extra informatie over deze aanroepen van Advertentie.

1. **App of browser naar achtergrond verplaatsen**

   Tijdens de uitvoering van de app op de achtergrond moeten alleen `main:pause`-aanroepen naar de Media Analytics-server worden verzonden, te beginnen met VHL versie 1.6.6 en hoger.

1. **App of browser terug naar voorgrond**

   Als u terugkeert van de achtergrond, wordt het afspelen van de inhoud hervat.

1. **De media met de belangrijkste inhoud gedurende minstens 5 minuten ononderbroken afspelen**

   Voor vraagparameters en meta-gegevens, zie [de Details van de Vraag van de Test.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Mediaspeler sluiten**

   Nadat de mediaspeler is gesloten, worden er geen aanvullende aanroepen voor bijhouden verzonden.
