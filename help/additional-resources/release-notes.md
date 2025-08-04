---
title: Opmerkingen bij de release Streaming Media Collection
description: Bekijk de releaseopmerkingen voor de opmerkingen bij de release Streaming Media Collection.
feature: Release Notes
role: User, Admin, Data Engineer
exl-id: ef068aa6-fdf4-4a5c-b5d0-b93ad31894e8
source-git-commit: a0a357c3fe7e958b0b6491c84f17f26a806ea205
workflow-type: tm+mt
source-wordcount: '1195'
ht-degree: 6%

---

# Opmerkingen bij de release Streaming Media Collection (mei 2023)

**Laatste update**: 29 mei, 2024

## Gerelateerde bronnen

Voor informatie over nieuwe eigenschappen, moeilijke situaties, en belangrijke informatie voor beheerders, zie de volgende middelen.

* [ de versienota&#39;s van Adobe Analytics ](https://experienceleague.adobe.com/docs/analytics/release-notes/latest.html?lang=en)
* [ de versienota&#39;s van Customer Journey Analytics ](https://experienceleague.adobe.com/docs/analytics-platform/using/releases/latest.html)
* De recentste versie werkt voor [ producten van Adobe Experience Cloud ](https://business.adobe.com/products/adobe-experience-cloud-products.html) bij

* [Adobe Analytics-tutorials](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=en)

## *Huidige Nota&#39;s van de Versie*

## Nieuwe en bijgewerkte functies in de Adobe Streaming Media Collection {#cja-features}

| Functie | Beschrijving | Doeldatum |
| ----------- | ---------- | ------- |
| Bijgewerkte XDM-velden voor het verzamelen van Streaming Media-gegevens in Adobe Experience Platform | Wanneer het verzamelen van de Gegevens van Media van de Streaming in Adobe Experience Platform, zouden de XDM gebiedspaden onder de rubriek van &quot;Pad van het Gebied XDM&quot;van de Streaming de parameterdocumentatie van Media niet meer moeten worden gebruikt. In plaats daarvan, moeten de klanten die de analytische bronschakelaar uitvoerden om het stromen gegevens van Media in Platform vóór 9 Mei te verzamelen, 2025 hun bestaande configuraties aan mediaReporting gebiedspaden, zoals aangetoond onder de rubriek &quot;het Weg van het Gebied van XDM&quot;van de documentatie van de parameters van Media het Streamen.<p> Deze gebiedspaden worden gevonden op de volgende pagina&#39;s en als &quot;Vervangen&quot;duidelijk: [ Audio en videoparameters ](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/audio-video-parameters), [ Advertentieparameters ](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/ad-parameters), [ de parameters van het Hoofdstuk ](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/chapter-parameters), [ de staatsparameters van de Speler ](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/player-state-parameters), en [ de parameters van de Kwaliteit ](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/quality-parameters). (Geen actie wordt vereist voor klanten die de bron van Analytics schakelaar na 9 Mei, 2025 uitvoeren, en reeds mediaReporting XDM wegen gebruiken.)</p><p>Gegevensinvoer op de afgekeurde XDM-veldpaden gaat door tot eind oktober 2025. Na die tijd, zullen de afgekeurde gebiedspaden volledig worden verwijderd en niet meer zichtbaar in het Schema UI van Adobe Experience Platform, en de gegevens zullen worden verzonden slechts gebruikend mediaReporting gebiedspaden.</p><p>Voor meer informatie, zie [ migreren een implementatie van de Verbinding van Analytics Source aan bijgewerkte XDM Streaming Media ](/help/use-cases/xdm-updates/updated-xdm-fields.md).</p><p>Neem contact op met uw Adobe Consulting Services of accountteam voor ondersteuning van migratie. </p> | Oktober 2025 |
| Webgegevens naar Adobe Experience Platform Edge Network verzenden met de Web SDK | U kunt [ het Web SDK van Adobe Experience Platform nu gebruiken om het stromen mediaWeb gegevens naar Adobe Experience Platform Edge Network ](/help/implementation/edge/edge-web-sdk.md) te verzenden, toestaand u om meer gepersonaliseerde campagnes te bouwen en meer gepersonaliseerde inhoud te verstrekken, resulterend in meer het volgen gegevens om op te melden.<p>Deze verbetering verstrekt een verenigde inzamelingsmethode voor Webimplementaties over alle oplossingen van het Platform, zoals Customer Journey Analytics, RT-CDP, AJO, en Gebeurtenis het Door:sturen. Eerder was de enige manier om streaming media webgegevens naar Edge Network te verzenden met de Media Edge API. | donderdag 29 mei 2024 |
| Roku-gegevens verzenden naar Adobe Experience Platform Edge | Nu wanneer [ het stromen de Inzameling van Media met Experience Platform Edge ](/help/implementation/edge/implementation-edge.md) installeert, kunt u Adobe Experience Platform Roku SDK gebruiken om het stromen media gegevens naar Adobe Experience Platform te verzenden. | zaterdag 12 april 2024 |
| Media Collection: Integratie met de Ervaring Edge (API en Mobiele SDK) | U kunt nu de Experience Edge API en Mobile SDK gebruiken om de Adobe Streaming Media Collection te implementeren, zodat u meer gepersonaliseerde campagnes kunt maken en meer gepersonaliseerde inhoud kunt bieden, waardoor meer trackinggegevens worden gebruikt om over te rapporteren.<p>Deze verbetering verstrekt een verenigde inzamelingsmethode over alle oplossingen, zoals Customer Journey Analytics rapporterend, RT-CDP, AJO, en Gebeurtenis het Door:sturen.  [Meer informatie](/help/implementation/edge/implementation-edge.md) | zaterdag 12 mei 2023 |
| Deelvenster Mediagelijktijdige viewer | Begrijp waar de piekgelijktijdig voorkwam of waar drop-outs voorkwamen. Geniet van waardevolle insight voor de kwaliteit van de betrokkenheid van content en viewers en hulp bij het oplossen van problemen of het plannen van volumes en schaal. [Meer informatie](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers.html?lang=en) | woensdag 9 augustus 2022 |
| Media afspelen tijd besteed, deelvenster | Media Playback Time Spent biedt waardevolle insight in de betrokkenheid van de kijker en stelt mediaorganisaties in staat diepgaandere, meer granulaire inzichten af te leiden met de betrokkenheid van gebruikers van minuut tot minuut door middel van geavanceerde tijdbestede analyse met mogelijkheden voor het parseren van dagen. U kunt de hoeveelheid tijd waarnemen die het bekijken van uw media stromen op een specifiek punt in tijd besteedt. U kunt de afspeelduur splitsen op verschillende granulariteiten, zoals nieuwe granulariteiten van 5 minuten, 15 minuten en 30 minuten. [Meer informatie](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/panels/media-playback-timespent/media-playback-time-spent.html) | woensdag 9 augustus 2022 |
| Annotaties delen op mobiele scorecards | U kunt annotaties weergeven die zijn gemaakt in Workspace, in Mobile Scorecards. Hierdoor kunt u contextuele gegevensnuances en inzichten over uw organisatie en campagnes rechtstreeks delen binnen Mobile Scorecard-projecten, die kunnen worden weergegeven in de mobiele app Analytics dashboards. [Meer informatie](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/annotations/mobile-annotations.html?lang=en) | donderdag 15 juni 2022 |
| Report Builder for Customer Journey Analytics-updates | Bevat functies zoals planning en gegevensblokbeheer. [Meer informatie](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-reportbuilder/manage-reportbuilder.html) | donderdag 18 mei 2022 |
| Annotaties in Workspace | Met annotaties in Workspace kunt u op effectieve wijze contextuele gegevensnuances en inzichten aan uw organisatie doorgeven. [Meer informatie](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/annotations/overview.html) | Geleidelijke uitrol start op 23 maart 2022 |
| Modus voor voorvertoning van mobiel scorecard-project | Start een voorvertoning van hoe uw mobiele scorecard eruit zal zien in de app Analytics dashboards, rechtstreeks vanuit de scorecard builder. In de voorvertoningsmodus kunnen gebruikers op dezelfde manier werken met filters en grafieken als in de app, zodat ze een voorvertoning van de ervaring kunnen bekijken voordat ze de scorecard opslaan en delen. Gebruikers kunnen de apparaatkiezer ook in de voorvertoningsmodus gebruiken om te zien hoe hun scorecard er op verschillende apparaten uitziet. [Meer informatie](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dashboards/create-scorecard.html#preview) | donderdag 16 februari 2022 |


## Nieuwe en bijgewerkte functies in de Adobe Streaming Media Collection {#sm-features}

| Functie | Beschrijving | Doeldatum |
| ----------- | ---------- | ------- |
| Meerdere statussen van speler bijhouden | Gebruik de Media Collection API om veelvoudige spelerstaat het volgen uit te voeren. [Meer informatie](https://experienceleague.adobe.com/docs/media-analytics/using/player-state-tracking/multiple-player-states.html) | September 2022 |
| Naam XDM-velden wijzigen | De anders genoemde XDM gebiedsnamen voor consistentie:<br> * Audio en Videoparameters <br>* Adparameters <br> * Parameters van het Hoofdstuk <br> * Parameters van de Staat van de Speler * <br> * Parameters van de Kwaliteit | September 2022 |
| Apparaatcoopverwijzing | Verwijzing naar Adobe Experience Cloud Device Co-op en de Experience Cloud ID service requirements verwijderd. | Augustus 2022 |
| Bijgewerkte veldnamen en XDM-paden voor verzameling en rapportage | Bijgewerkt het volgende:<br> * Audio en Video Parameters <br> * Add Parameters <br> * de Parameters van het Hoofdstuk <br> * Parameters van de Staat van de Speler * <br> * Parameters van de Kwaliteit | Augustus 2022 |
| Gemiddeld aantal minuten publiek | Klanten van Media Analytics kunnen het deelvenster Gemiddelde miniatuur gebruiken om een beter inzicht te krijgen in het gemiddelde verbruik van inhoud. <br> Gemiddeld minusepubliek laat vergelijkingen van programmering van om het even welke lengte of genre toe. Bovendien kunt u het digitale gemiddelde minusepubliek vergelijken of toevoegen aan lineaire gemiddelde de minmetriek van TV. Dit deelvenster biedt meer flexibiliteit om het gemiddelde publiek voor aangepaste tijdsperiodes te meten en om te bepalen wanneer de classificatie van de duur is bijgewerkt.  [Meer informatie](https://experienceleague.adobe.com/docs/media-analytics/using/media-reports/average-minute-audience.html?lang=en) | donderdag 16 maart 2022 |
| Deelvenster Tijd van afspelen van media | Leer hoe mediagebruikers met het deelvenster Tijd voor afspelen van media hun viewer kunnen begrijpen op basis van de hoeveelheid tijd die ze de dag over een gekozen korreligheid hebben bekeken. <br>[ Media Playback Time Spent Panel (leerprogramma) ](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/media-analytics/measuring-media-analytics/media-playback-time-spent-panel.html?lang=en) | Januari 2022 |


## *de Vorige Nota&#39;s van de Versie*

| Functie | Beschrijving | Doeldatum of Bijgewerkte datum |
| ----------- | ---------- | -------------- |
| Tijd van afspelen van media besteed | De Adobe Streaming Media Playback Time Spent biedt waardevolle insight voor de betrokkenheid van de kijker en stelt mediaorganisaties in staat diepgaandere, meer granulaire inzichten af te leiden met een minuscule betrokkenheid van gebruikers door middel van een geavanceerde tijdbestede analyse met de mogelijkheden voor het parseren van dagen. U kunt de hoeveelheid tijd waarnemen die het bekijken van uw media stromen op een specifiek punt in tijd besteedt. U kunt de afspeelduur splitsen op verschillende granulariteiten, zoals nieuwe granulariteiten van 5 minuten, 15 minuten en 30 minuten. [Meer informatie...](/help/reporting/workspace/media-playback-time-spent.md) | September 2021 |
| Deelvenster Mediagelijktijdige viewer in Analyse Workspace | Begrijp waar de piekgelijktijdig voorkwam of waar drop-outs voorkwamen. Geniet van waardevolle insight voor de kwaliteit van de betrokkenheid van content en viewers en hulp bij het oplossen van problemen of het plannen van volumes en schaal. [ leer meer... ](/help/reporting/workspace/media-concurrent-viewers-overview.md) <br><br>[ het Gelijktijdige Comité van Kijkers van Media in Workspace van de Analyse (leerprogramma) ](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/analysis-workspace/using-panels/media-concurrent-viewers-panel-in-analysis-workspace.html?lang=en#analysis-workspace) | September 2020 <br><br><br> Januari 2021 |
| Ondersteunde apparaten en platforms | De extensie Media Launch met AEP SDK ondersteunt nu de volgende OTT-apparaten: <div><ul><li>Apple TV (tvOS)</li><li>Fire TV (Fire OS)</li><li>Android-tv</li></ul></div> | Juni 2020 |


<!-- ## Important notices for [!DNL Analytics] administrators

**Updated on March 3, 2022**

| Notice | Date Added or Updated  | Description |
| ----------- | ---------- | ---------- |
| description | date | description |
| description | date | description |
| description | date | description |
| description | date | description | -->
