---
title: Berekende standaarden
description: Leer over berekende metriek en metrische formules in de het stromen Inzameling van Media.
uuid: 9dd35155-58aa-4f05-896e-c5cbc4b13d59
exl-id: 253f6c61-70b5-4bdf-8e79-840545aeca0e
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 3%

---

# Berekende cijfers{#calculated-metrics}

Berekende meetwaarden voor de Adobe die de Verzameling van Media stroomt zijn douanemetriek die u toestaan om gerichte het stromen media gegevens zoals gemiddelde gebruikte tijd of gemiddelde advertenties per media stroom te verkrijgen.

Voor informatie over Adobe Analytics berekende metriek, zie [ Berekende en Geavanceerde Berekende (Afgeleid) Metriek ](https://experienceleague.adobe.com/docs/analytics/components/calculated-metrics/cm-overview.html?lang=nl-NL) in de Gids van de Componenten van Adobe Analytics.

>[!NOTE]
>
>Deze berekende maatstaven werden op 13-9-18 geïntroduceerd.

| Metrisch | Beschrijving | Formule |
|---|---|---|
| Gem. Advertenties per mediastroom | Advertentie start per mediumstart | `Ad Starts / Media Starts` |
| Gem. Hoofdstukken per mediastroom | Hoofdstuk start per medium | `Chapter Start / Media Starts` |
| Gem. Tijd besteed aan media | Totale tijd die per Media begint (`HH:MM:SS`) | `Media Time Spent / Media Starts` |
| Gem. Tijd van inhoud besteed | Tijd van inhoud die per Content begint (`HH:MM:SS`) | `Content Time Spent / Content Start` |
| Gem. Toegevoegde tijd | Advertentietijd doorgebracht per Advertentiestart (`HH:MM:SS`) | `Ad Time Spent / Ad Start` |
| Gem. Tijd besteed aan hoofdstuk | De Tijd die van het hoofdstuk per Hoofdstuk begint (`HH:MM:SS`) | `Chapter Time Spent / Chapter Start` |
| Voltooiingssnelheid van media | Percentage voltooide inhoud versus geïnitieerde media (%) | `Content Completes/ Media Starts` |
| Voltooiingssnelheid van inhoud | Percentage van voltooide inhoud versus begin van inhoud (%) | `Content Completes / Content Starts` |
| Voltooiingssnelheid van advertentie | Percentage voltooide advertenties vs Advertentiestart (%) | `Ad Completes / Ad Starts` |
| Afsluitingspercentage hoofdstuk | Percentage voltooide hoofdstukken versus Start van hoofdstuk (%) | `Chapter Completes / Chapter Starts` |
| Waarden neerzetten voor beginsnelheid | Snelheid van druppels voor begin vs mediumstart (%) | `Drops before Starts / Media Starts` |
| Tijdsduur inhoudspauze | Percentage van totale pauzeduur vs Content Time Spent (%) | `Total Pause Duration / Content Time Spent` |
| Duur van inhoudsbuffer | Percentage van totale bufferduur vs Content Time Spent (%) | `Total Buffer Duration / Content Time Spent` |
| Inhoudstijd tot beginsnelheid | Tijdsfrequentie tot begin vs Content Time Spent (%) | `Time to Start / Content Time Spent` |
| Tijdssnelheid toevoegen | Processorsnelheid van bestede advertentietijd versus bestede inhoudstijd (%) | `Ad Time Spent / Content Time Spent` |
