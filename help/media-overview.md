---
title: Audio en video meten in Adobe Analytics
description: Adobe Analytics voor Media (ook wel Media Analytics genoemd) biedt clients robuuste mediametingen voor content, audio en advertenties.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
translation-type: tm+mt
source-git-commit: bddcbcd844145788518c60399bee9e4744e42d3a

---


# Audio en video meten in Adobe Analytics {#measuring-audio-and-video-in-adobe-analytics}

![Banner](./assets/media_analytics_banner.png)

## Informatie over Adobe Analytics voor audio en video

Adobe Analytics for Audio and Video is een invoegtoepassing voor Adobe Analytics die krachtige meetgereedschappen voor audio, video en advertenties biedt. Adobe Analytics maakt deel uit van het Adobe Experience Platform.

Met Adobe Analytics for Audio and Video kunt u de volledige reis van de klant over uw site volgen. De metriek kan eenvoudig worden geïntegreerd in Adobe Analytics Reports en andere Adobe Experience Cloud-producten. Met mediummeting kunt u uw gegevens indelen in meerdere dimensies en segmenten en alle metagegevens vastleggen die u nodig hebt voor een volledige en gedetailleerde analyse. Vervolgens kunt u gegevens analyseren en succescriteria toewijzen aan volledig verbruikte media, gemiddelde gebruikte tijd en voltooide advertenties.

U kunt vitale leveringsmetriek met betrekking tot QoS, zoals gelaten vallen kaders, tijd doorgebrachte het als buffer optreden voor, en gemiddelde bitrate meten. En de metriek kan met uw website of toepassingsgegevens worden gecombineerd om het klantenweg en de belangen-om verbeterde aanbevelingen te verstrekken en klantenervaringen te personaliseren gebruikend de Wolk van de Ervaring van Adobe.

## Functies {#features}

Adobe-analysemogelijkheden voor audio en video bieden onder andere realtime bewaking, gedetailleerde analyse, inzichten in handelingen en mogelijkheden voor monetisering.
* **Analyse** in real time: maak realtime, uitvoerbare beslissingen met behulp van belangrijke prestatiemetriek zoals duration, ex2 en ex3, over meerdere kanalen. Gebeurtenissen in verband met hoofdcontent worden gemeten met tussenpozen van 10 seconden om alle activiteit vast te leggen terwijl deze plaatsvindt. Gebeurtenissen in verband met het bijhouden van advertenties vinden plaats met tussenpozen van 1 seconde.
* **Betrokkenheid** van de aandrijving - verbind gebruikers volledig door minder het bufferen gebeurtenissen en door te begrijpen waar en wanneer de advertenties binnen inhoud zouden moeten spelen om een vlotte, minder opdringerige ervaring te verstrekken die herhaalde bezoeken levert.
* **Holistisch beeld**- combineer veelvoudige gegevenspunten over al uw inhoudsverdelers om een volledige mening van al uw media activiteit te krijgen. Meet de betrokkenheid en de meningen/luistert over alle mogelijke kanalen door de Federated Analytics eigenschap.
* **Meer granulariteit**: evalueer het weergavegedrag op het meest korrelige niveau, inclusief de individuele bezoekerstijd van de dag, gelijktijdige viewers/listeners op minuut en de gemiddelde duur van de inhoud.
* **Nauwkeurige meting**-Meet over de veelvoudige apparaten die voor media consumptie, met inbegrip van OTT, smartphone, tablet, Desktop, en meer worden gebruikt, om de patronen en gewoonten van de gebruikersbetrokkenheid te controleren.
* **Segmentatie**- Pas classificaties op uw spelers, apparaten, genres, hoofdstukken toe, en toont om te zien hoe elk een effect op uw algemene meningen/luistert en klantenbetrokkenheid met inhoud, audio, advertenties, en gecombineerde heeft.

## Hartslagmaat {#heartbeat}

Adobe Analytics gebruikt &#39;heartbeats&#39; om videomeetgegevens te verzamelen. Tijdens het afspelen van video worden hartslagen naar de hartslagvolgserver verzonden om de afspeeltijd te meten. De hartslagvraag wordt verzonden om de tien seconden. De hartslagen resulteren in korrelige videobetrokkenheidsmetriek en nauwkeurigere video valutapporten. Met Adobe Analytics for Audio and Video worden hartslagen gemeten bij het gebruik van Adobe Launch met de extensie Media Analytics, de Media SDK en de Media Collection API. De componenten `AppMeasurement` en `VisitorID` worden gebruikt om videogegevens te ontvangen.

Het gebruik van hartslagen biedt de volgende voordelen voor Adobe Analytics voor Audio en Video:

| Functie | Beschrijving |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Mediagebeurtenissen | Gedetailleerde en aangepaste gebeurtenissen worden elke 10 seconden verzonden voor de hoofdinhoud en elke 1 seconde voor advertenties |
| Statistieken en dimensies | Duidelijk gestandaardiseerde metriek, afmetingen, en benchmarks over<br>verkopersMet een gestandaardiseerde oplossing over alle platforms, kunt u verenigbare, gestandaardiseerde variabelen over al uw media en platforms gebruiken om voor een efficiëntere dwars-campagne, apparaat en verkopersvergelijking toe te staan. |
| Integraties | Experience Cloud-id is gekoppeld aan Adobe Experience Cloud voor eenvoudige<br>kruisanalyseMet de automatische integratie van Adobe Experience Cloud kunt u mediapubliek segmenteren, doelgroepen maken en mediumaanbevelingen doen op basis van gebruikersvoorkeuren. |
| Prijzen | Transparant bijhouden via mediastream (enkel) |
| Implementatie en ondersteuning | Gestroomlijnde configuratie met doorlopende updates en<br>verbeteringenMet een gestroomlijnd implementatieproces kunt u snel variabelen toewijzen via de speler-API en implementaties valideren met Adobe Debug Tool om ervoor te zorgen dat alle benodigde variabelen correct worden bijgehouden. |
| Delen via partners | Federated Analytics and Certified Metrics<br>With shared data through Federated Analytics, you can capitalize on our industry-first media sharing capabilities, to evaluate data holistically across all of your media distribution partners—operators, programmers, and distributors. |
| Geavanceerde tracking | Gedownloade Inhoud bijhouden, Foutherstel bijhouden en Gelijktijdige<br>viewersU kunt audio- en video-inhoud bijhouden die wordt gedownload en afgespeeld op een apparaat, ongeacht de connectiviteit ervan. |



## Beveiliging {#security}

Bij Adobe nemen we de beveiliging van uw digitale middelen serieus. Van onze rigoureuze integratie van veiligheid in ons interne softwareontwikkelingsproces en -instrumenten tot onze interfunctionele responsteams voor incidenten, streven we ernaar proactief en nimble te zijn. Bovendien helpen onze samenwerking met partners, onderzoekers en andere brancheorganisaties ons de nieuwste dreigingen en best practices op het gebied van beveiliging te begrijpen, en zorgen we ervoor dat de producten en services die we aanbieden voortdurend veilig zijn.


### Transport Layer Security {#transport-layer-security}

**TLS-kennisgeving -** Adobe heeft beveiligingscompatibiliteitsnormen waarvoor einde-levensduur van oudere beveiligingsprotocollen vereist is. Om te blijven voldoen aan de evoluerende normen van veiligheidsprotocollen is Adobe op weg naar van TLS 1.2 om de meest actuele en veilige versie te gebruiken. Vanaf 20 februari 2019 biedt Adobe alleen nog ondersteuning voor TLS 1.1 of hoger. Met deze wijziging verzamelt Adobe geen data meer van eindgebruikers met oudere apparaten of webbrowsers die gebruikmaken van TLS 1.0. Migratie naar TLS 1.2 biedt betere beveiliging. Het is belangrijk dat u de details doorloopt en de wijzigingen plant voor een vloeiende overgang.

>[!NOTE]
>
>TLS is momenteel het meest gebruikte veiligheidsprotocol in webbrowsers en andere toepassingen waarin data veilig over een netwerk worden uitgewisseld.
