---
title: Opmerkingen bij de release Adobe Analytics for Streaming Media
description: Bekijk de opmerkingen bij de release van Adobe Analytics.
feature: Release Notes
exl-id: ef068aa6-fdf4-4a5c-b5d0-b93ad31894e8
source-git-commit: 0c02fec77d6484774ea81e997529accddb19d175
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 7%

---

# Opmerkingen bij de release Adobe Analytics for Streaming Media (september 2022)

**Laatste update**: 22 september 2022

## Gerelateerde bronnen

Voor informatie over nieuwe eigenschappen, moeilijke situaties, en belangrijke informatie voor beheerders, zie de volgende middelen.

* [Opmerkingen bij de release van Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/release-notes/latest.html?lang=en)
* [Opmerkingen bij de release Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/releases/latest.html)
* De nieuwste release-updates voor [Adobe Experience Cloud-producten](https://business.adobe.com/products/adobe-experience-cloud-products.html)

* [Tutorials voor Adobe Analytics](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=en)

## *Opmerkingen bij de huidige release*

## Nieuwe en bijgewerkte functies in Adobe Customer Journey Analytics voor streaming media {#cja-features}

| Functie | Beschrijving | Doeldatum |
| ----------- | ---------- | ------- |
| Media-verzameling: Integratie met Experience Edge (API en mobiele SDK) | Met de Experience Edge API en de Mobile SDK kunt u nu streaming media implementeren, zodat u meer persoonlijke campagnes kunt maken en meer persoonlijke inhoud kunt bieden, waardoor er meer trackinggegevens beschikbaar komen om op te geven.<p>Deze verbetering verstrekt een verenigde inzamelingsmethode over alle oplossingen, zoals CJA die, RT-CDP, AJO, en Gebeurtenis door:sturen melden.  [Meer informatie](/help/implementation/media-sdk/implementation-edge.md) | Eind mei 2023 |
| Deelvenster Mediagelijktijdige viewer | Begrijp waar de piekgelijktijdig voorkwam of waar drop-outs voorkwamen. Krijg waardevol inzicht in de kwaliteit van inhoud en viewerbetrokkenheid, en hulp bij het oplossen van problemen of het plannen voor volume en schaal. [Meer informatie](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers.html?lang=en) | 9 augustus 2022 |
| Media afspelen tijd besteed, deelvenster | Media Playback Time Spent biedt een waardevol inzicht in de betrokkenheid van de kijker en stelt mediaorganisaties in staat diepere, meer korrelige inzichten af te leiden met de betrokkenheid van gebruikers van minuut tot minuut door middel van geavanceerde tijdbestede analyse met mogelijkheden voor het parseren van dagen. U kunt de hoeveelheid tijd waarnemen die het bekijken van uw media stromen op een specifiek punt in tijd besteedt. U kunt de afspeelduur splitsen op verschillende granulariteiten, zoals nieuwe granulariteiten van 5 minuten, 15 minuten en 30 minuten. [Meer informatie](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/panels/media-playback-timespent/media-playback-time-spent.html) | 9 augustus 2022 |
| Annotaties delen op mobiele scorecards | U kunt annotaties weergeven die zijn gemaakt in Workspace, in Mobiele Scorecards. Hierdoor kunt u contextuele gegevensnuances en inzichten over uw organisatie en campagnes rechtstreeks delen binnen Mobile Scorecard-projecten, die kunnen worden weergegeven in de mobiele app Analytics dashboards. [Meer informatie](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/annotations/mobile-annotations.html?lang=en) | 15 juni 2022 |
| Report Builder voor CJA-updates | Bevat functies zoals planning en gegevensblokbeheer. [Meer informatie](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-reportbuilder/manage-reportbuilder.html) | 18 mei 2022 |
| Annotaties in werkruimte | Met annotaties in Workspace kunt u op effectieve wijze contextuele gegevensnuances en inzichten aan uw organisatie meedelen. [Meer informatie](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/annotations/overview.html) | Geleidelijke uitrol start op 23 maart 2022 |
| Modus voor voorvertoning van mobiel scorecard-project | Start een voorvertoning van hoe uw mobiele scorecard eruit zal zien in de app Analytics dashboards, rechtstreeks vanuit de scorecard builder. In de voorvertoningsmodus kunnen gebruikers op dezelfde manier werken met filters en grafieken als in de app, zodat ze een voorvertoning van de ervaring kunnen bekijken voordat ze de scorecard opslaan en delen. Gebruikers kunnen de apparaatkiezer ook in de voorvertoningsmodus gebruiken om te zien hoe hun scorecard er op verschillende apparaten uitziet. [Meer informatie](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dashboards/create-scorecard.html#preview) | 16 februari 2022 |


## Nieuwe en bijgewerkte functies in Adobe Analytics voor Streaming Media {#sm-features}

| Functie | Beschrijving | Doeldatum |
| ----------- | ---------- | ------- |
| Meerdere statussen van speler bijhouden | Gebruik de Media Collection API om veelvoudige spelerstaat het volgen uit te voeren. [Meer informatie](https://experienceleague.adobe.com/docs/media-analytics/using/player-state-tracking/multiple-player-states.html) | September 2022 |
| Naam XDM-velden wijzigen | Naam van XDM-velden is gewijzigd voor consistentie:<br>* Parameters voor audio en video<br>* Toegevoegde parameters<br>* Hoofdstukparameters<br>* Parameters spelerstatus<br>* Parameters voor kwaliteit | September 2022 |
| Apparaatcoopverwijzing | Verwijzing naar Adobe Experience Cloud Device Co-op en de servicevereiste voor Experience Cloud-id is verwijderd. | Augustus 2022 |
| Bijgewerkte veldnamen en XDM-paden voor verzameling en rapportage | Het volgende is bijgewerkt:<br>* Parameters voor audio en video<br>* Toegevoegde parameters<br>* Hoofdstukparameters<br>* Parameters spelerstatus<br>* Parameters voor kwaliteit | Augustus 2022 |
| Gemiddeld aantal minuten publiek | Klanten van Media Analytics kunnen het deelvenster Gemiddelde miniatuur gebruiken om een beter inzicht te krijgen in het gemiddelde verbruik van inhoud. <br>Het gemiddelde minutenpubliek maakt vergelijkingen van programmering van om het even welke lengte of genre mogelijk. Bovendien kunt u het digitale gemiddelde minusepubliek vergelijken of toevoegen aan lineaire gemiddelde de minmetriek van TV. Dit deelvenster biedt meer flexibiliteit om het gemiddelde publiek voor aangepaste tijdsperiodes te meten en om te bepalen wanneer de classificatie van de duur is bijgewerkt.  [Meer informatie](https://experienceleague.adobe.com/docs/media-analytics/using/media-reports/average-minute-audience.html?lang=en) | 16 maart 2022 |
| Deelvenster Tijd van afspelen van media | Leer hoe mediagebruikers met het deelvenster Tijd voor afspelen van media hun viewer kunnen begrijpen op basis van de hoeveelheid tijd die ze de dag over een gekozen korreligheid hebben bekeken. <br>[Deelvenster Tijd van afspelen van media (zelfstudie)](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/media-analytics/measuring-media-analytics/media-playback-time-spent-panel.html?lang=en) | Januari 2022 |


## *Opmerkingen bij vorige release*

| Functie | Beschrijving | Doeldatum of Bijgewerkte datum |
| ----------- | ---------- | -------------- |
| Tijd van afspelen van media besteed | Adobe Streaming Media Playback Time Spent biedt een waardevol inzicht in de betrokkenheid van de kijker en stelt mediaorganisaties in staat diepere, meer granulaire inzichten af te leiden met de betrokkenheid van gebruikers van minuut tot minuut door middel van geavanceerde tijdbestede analyse met mogelijkheden voor het parseren van dagen. U kunt de hoeveelheid tijd waarnemen die het bekijken van uw media stromen op een specifiek punt in tijd besteedt. U kunt de afspeelduur splitsen op verschillende granulariteiten, zoals nieuwe granulariteiten van 5 minuten, 15 minuten en 30 minuten. [Meer informatie...](/help/reporting/workspace/media-playback-time-spent.md) | September 2021 |
| Deelvenster Mediagelijktijdige viewer in de werkruimte Analyse | Begrijp waar de piekgelijktijdig voorkwam of waar drop-outs voorkwamen. Krijg waardevol inzicht in de kwaliteit van inhoud en viewerbetrokkenheid, en hulp bij het oplossen van problemen of het plannen voor volume en schaal. [Meer informatie...](/help/reporting/workspace/media-concurrent-viewers-overview.md) <br><br>[Deelvenster Mediagelijktijdige viewers in de werkruimte Analytics (zelfstudie)](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/analysis-workspace/using-panels/media-concurrent-viewers-panel-in-analysis-workspace.html?lang=en#analysis-workspace) | september 2020 <br><br><br>Januari 2021 |
| Ondersteunde apparaten en platforms | De extensie Media Launch met AEP SDK ondersteunt nu de volgende OTT-apparaten: <div><ul><li>Apple TV (tvOS)</li><li>Fire TV (Fire OS)</li><li>Android-tv</li></ul></div> | Juni 2020 |


<!-- ## Important notices for [!DNL Analytics] administrators

**Updated on March 3, 2022**

| Notice | Date Added or Updated  | Description |
| ----------- | ---------- | ---------- |
| description | date | description |
| description | date | description |
| description | date | description |
| description | date | description | -->
