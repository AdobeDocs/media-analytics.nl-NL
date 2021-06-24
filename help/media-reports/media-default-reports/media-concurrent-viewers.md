---
title: Mediagelijktijdige viewers
description: '"Leer meer over het dashboard Medium Gelijktijdige Viewers dat wordt gebruikt om gelijktijdige viewers gedurende één dag weer te geven. De gegevens kunnen door inhoud, apparatentype, of land worden gefiltreerd."'
uuid: e61c50e5-8196-4538-b67c-ebc01c6e6ba7
exl-id: 2c679c1a-a4bd-44fc-8e11-173c8544ab06
feature: '"Grondbeginselen van media-analyse, rapporten en analyses"'
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# Mediagelijktijdige viewers{#media-concurrent-viewers}

Op het dashboard Medium Gelijktijdige viewers worden gedurende één dag gelijktijdige viewers weergegeven. De gegevens kunnen worden gefilterd op inhoud, apparaattype of land.

>[!TIP]
>
> Dit rapport is gebaseerd op gelijktijdige actieve mediasessies.  Gebruik het [deelvenster Mediagelijktijdige viewers in Analysis Workspace](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/media-concurrent-viewers.html) om gelijktijdige viewers per unieke bezoeker weer te geven met de extra mogelijkheden om een segment toe te passen, op te splitsen en te vergelijken.


![](assets/video-concurrent-viewers.png)

## Rapportfuncties {#report-features}

Dit rapport bevat enkele kenmerken:

* Dit is niet in real time. Het heeft normale Adobe Analytics latentie.
* Het verslag bestrijkt een tijdsbestek van 24 uur. De x-as is tijd-van-dag die op de tijdzone van de rapportreeks wordt gebaseerd.
* Dit toont gelijktijdige kijkers bij minieme granulariteit.
* Er is een *Rapport Medium Gelijktijdige Viewers* dat toont hoeveel kijkers kijken of over alle inhoud luisteren.
* Er is een Gelijktijdig rapport Viewers in het rapport *Mediadetail* dat toont hoeveel kijkers naar één specifiek media-item kijken of luisteren.
* Het rapport werkt slechts over één dag.
* De klant kan naar historische gelijktijdige viewerrapporten (beperkt tot één dag) kijken.

## Beperkingen {#limitations}

Hier volgen enkele beperkingen voor dit rapport:

* Er worden geen gegevens weergegeven als het geselecteerde interval geen hele dag is.
* U kunt de gegevens, zoals ReportBuilder, niet exporteren.
* U kunt de gegevens niet in een tabelindeling presenteren.
* U kunt een rapport niet verzenden via e-mail.
* Zelfs als u geen advertenties bijhoudt, moet u media tracking opnieuw inschakelen en de module Media Ad selecteren.
* Deze functionaliteit biedt nauwkeurige gegevens wanneer u een hartslagbibliotheek gebruikt die mogelijkheden voor het bijhouden van pauzes heeft.
