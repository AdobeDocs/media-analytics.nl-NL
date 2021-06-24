---
title: Berekende standaarden
description: Leer over Adobe die Media berekende metriek en metrische formules stroomt.
uuid: 9dd35155-58aa-4f05-896e-c5cbc4b13d59
exl-id: 253f6c61-70b5-4bdf-8e79-840545aeca0e
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 5%

---

# Berekende standaarden{#calculated-metrics}

>[!NOTE]
>
>Deze berekende maatstaven werden op 13-9-18 geïntroduceerd.

| Metrisch | Beschrijving | Formule |
|---|---|---|
| Gem. Advertenties per mediastroom | Advertentie start per mediumstart | `Ad Starts / Media Starts` |
| Gem. Hoofdstukken per mediastroom | Hoofdstuk start per medium | `Chapter Start / Media Starts` |
| Gem. Tijd besteed aan media | Totale tijd die per media wordt besteed (HH:MM:SS) | `Media Time Spent / Media Starts` |
| Gem. Tijd van inhoud besteed | Tijd van inhoud per inhoud begint (HH:MM:SS) | `Content Time Spent / Content Start` |
| Gem. Toegevoegde tijd | Adviseer tijd die per Advertentie begint (HH:MM:SS) | `Ad Time Spent / Ad Start` |
| Gem. Tijd besteed aan hoofdstuk | De Tijd die van het hoofdstuk per Hoofdstuk wordt uitgegeven begint (HH:MM:SS) | `Chapter Time Spent / Chapter Start` |
| Voltooiingssnelheid van media | Percentage voltooide inhoud versus geïnitieerde media (%) | `Content Completes/ Media Starts` |
| Voltooiingssnelheid van inhoud | Percentage van voltooide inhoud versus begin van inhoud (%) | `Content Completes / Content Starts` |
| Voltooiingssnelheid van advertentie | Percentage voltooide advertenties vs Advertentiestart (%) | `Ad Completes / Ad Starts` |
| Afsluitingspercentage hoofdstuk | Percentage voltooide hoofdstukfuncties vs Hoofdstukstarters (%) | `Chapter Completes / Chapter Starts` |
| Waarden neerzetten voor beginsnelheid | Snelheid van druppels voor begin vs mediumstart (%) | `Drops before Starts / Media Starts` |
| Tijdsduur inhoudspauze | Percentage van totale pauzeduur vs Content Time Spent (%) | `Total Pause Duration / Content Time Spent` |
| Duur van inhoudsbuffer | Percentage van totale bufferduur vs Content Time Spent (%) | `Total Buffer Duration / Content Time Spent` |
| Inhoudstijd tot beginsnelheid | Tijdsfrequentie tot begin vs Content Time Spent (%) | `Time to Start / Content Time Spent` |
| Tijdssnelheid toevoegen | Processorsnelheid van bestede advertentietijd versus bestede inhoudstijd (%) | `Ad Time Spent / Content Time Spent` |
