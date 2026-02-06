---
title: Testen 2 onderbreking van media
description: Meer informatie over de mediaverstoring die wordt gebruikt bij de validatie.
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
exl-id: 3f22ce2d-4385-4a3b-8d1f-52e25a9b1101
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# Test 2: Onderbreking van media{#test-media-interruption}

Deze testcase valideert het gedrag van mobiele onderbrekingen.

## Testprocedure

U moet deze taken in de volgende volgorde voltooien en opnemen:

1. **Begin de media speler**

   Wanneer de mediaspeler start, worden de volgende aanroepen in de volgende volgorde verzonden:

   1. Adobe Analytics (AppMeasurement) Start
   1. Start van media-analyse (hartslagen)
   1. Media Analytics (heartbeats) Aanvraag voor Adobe Analytics Start aangevraagd

   De eerste twee hierboven vraag bevat extra meta-gegevens en variabelen. Voor vraagparameters en meta-gegevens, zie [&#x200B; de vraagdetails van de Test.](/help/legacy/validation/test-call-details.md#start-the-media-player)

   De derde vraag hierboven vertelt de server van de Analyse van Media dat de Media SDK verzocht om dat de vraag van het Begin van Adobe Analytics (`pev2=ms_s`) wordt verzonden naar de server van Adobe Analytics.

1. **belangrijkste inhoud van het Spel voor minstens 5 minuten ononderbroken**

   **Inhoud Spel**

   Tijdens het afspelen van inhoud verzendt de Media SDK om de tien seconden afspeelaanroepen (hartslagen) naar de Media Analytics-server.

   Voor vraagparameters en meta-gegevens, zie [&#x200B; de vraagdetails van de Test.](/help/legacy/validation/test-call-details.md#play-main-content)

   Zie ook het 0&rbrace; Spoor van uw platform Advertentie [&#x200B; instructies voor extra informatie over deze vraag van Advertentie.](/help/use-cases/track-ads/track-ads-overview.md)

1. **Beweeg app of browser aan de achtergrond**

   Terwijl de app op de achtergrond wordt uitgevoerd, moeten alleen `main:pause` -aanroepen naar de Media Analytics-server worden verzonden, te beginnen met VHL versie 1.6.6 en hoger.

1. **breng app of browser terug naar voorgrond**

   Als u terugkeert van de achtergrond, wordt het afspelen van de inhoud hervat.

1. **media van de belangrijkste inhoud van het Spel voor minstens 5 minuten ononderbroken**

   Voor vraagparameters en meta-gegevens, zie [&#x200B; de Details van de Vraag van de Test.](/help/legacy/validation/test-call-details.md#play-main-content)

1. **Sluiten media speler**

   Nadat de mediaspeler is gesloten, worden er geen aanvullende aanroepen voor bijhouden verzonden.
