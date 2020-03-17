---
title: Testen 2 Onderbreking media
description: Dit onderwerp beschrijft de media onderbreking test die in bevestiging wordt gebruikt.
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
translation-type: tm+mt
source-git-commit: cebf5697e3746721d29bfaa5356d5a2748fea435

---


# Test 2: Onderbreking media{#test-media-interruption}

Deze testcase valideert het gedrag van mobiele onderbrekingen.

## Testprocedure

U moet deze taken in de volgende volgorde voltooien en opnemen:

1. **De mediaspeler starten**

   Wanneer de mediaspeler start, worden de volgende aanroepen in de volgende volgorde verzonden:

   1. Start Adobe Analytics (AppMeasurement)
   1. Start van media-analyse (hartslagen)
   1. Media Analytics (heartbeats) Adobe Analytics Start call requested
   De eerste twee bovenstaande aanroepen bevatten aanvullende metagegevens en variabelen. Voor vraagparameters en meta-gegevens, zie de vraagdetails van de [Test.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   In de derde bovenstaande oproep wordt aan de Media Analytics-server doorgegeven dat de Media SDK heeft verzocht dat de aanroep van Adobe Analytics Start (`pev2=ms_s`) naar de Adobe Analytics-server wordt verzonden.

1. **De belangrijkste inhoud van het spel gedurende minstens 5 minuten ononderbroken**

   **Inhoud afspelen**

   Tijdens het afspelen van inhoud verzendt de Media SDK afspeelaanroepen (hartslagen) naar de Media Analytics-server om de tien seconden.

   Voor vraagparameters en meta-gegevens, zie de vraagdetails van de [Test.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

   Zie ook de instructies van [Trackadvertenties](/help/sdk-implement/track-ads/track-ads-overview.md) van uw platform voor aanvullende informatie over deze Ad-aanroepen.

1. **App of browser naar de achtergrond verplaatsen**

   Terwijl de app op de achtergrond wordt uitgevoerd, moeten alleen `main:pause` aanroepen naar de Media Analytics-server worden verzonden, te beginnen met VHL versie 1.6.6 en hoger.

1. **App of browser terug naar voorgrond**

   Als u terugkeert van de achtergrond, wordt het afspelen van de inhoud hervat.

1. **De media met de belangrijkste inhoud gedurende minstens 5 minuten ononderbroken afspelen**

   Voor vraagparameters en meta-gegevens, zie de Details van de Vraag van de [Test.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Mediaspeler sluiten**

   Nadat de mediaspeler is gesloten, worden er geen aanvullende aanroepen voor bijhouden verzonden.
