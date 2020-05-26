---
title: Audio en video meten in Adobe Analytics
description: Adobe Analytics voor Media (ook wel Media Analytics genoemd) biedt clients robuuste mediametingen voor content, audio en advertenties.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
translation-type: ht
source-git-commit: bddcbcd844145788518c60399bee9e4744e42d3a

---


# Audio en video meten in Adobe Analytics {#measuring-audio-and-video-in-adobe-analytics}

![Banner](./assets/media_analytics_banner.png)

## Adobe Analytics voor audio en video

Adobe Analytics voor audio en video is een add-on voor Adobe Analytics met krachtige meettools voor audio, video en advertenties. Adobe Analytics maakt deel uit van het Adobe Experience Platform.

Met Adobe Analytics voor audio en video kunt u het volledige traject van de klant op uw site volgen. De statistieken kunnen eenvoudig worden geïntegreerd in Adobe Analytics Reports en andere Adobe Experience Cloud-producten. Met mediameting kunt u uw data indelen in meerdere dimensies en segmenten, en zo alle metadata vastleggen die u nodig hebt voor een volledige en gedetailleerde analyse. Vervolgens kunt u data analyseren en succescriteria toewijzen aan volledig verbruikte media, gemiddelde bestede tijd en voltooide advertenties.

U kunt essentiële leveringsstatistieken in verband met QoS meten, zoals dropped frames, buffertijd en gemiddelde bitsnelheid. En de statistieken kunnen met uw website of appdata worden gecombineerd om het traject en de interesses van de klant te visualiseren en op basis daarvan verbeterde aanbevelingen te verstrekken en klantervaringen te personaliseren met Adobe Experience Cloud.

## Functies {#features}

Adobe Analytics voor audio en video biedt onder andere realtime monitoring, gedetailleerde analyse, inzichten waarvoor acties kunnen worden uitgevoerd en mogelijkheden voor monetisatie.
* **Real-time analyse**: maak real-time beslissingen waarvoor acties kunnen worden uitgevoerd op basis van essentiële prestatiestatistieken zoals duur, ex2 en ex3, op meerdere kanalen. Gebeurtenissen in verband met hoofdcontent worden gemeten met tussenpozen van 10 seconden om alle activiteit vast te leggen terwijl deze plaatsvindt. Gebeurtenissen in verband met het bijhouden van advertenties vinden plaats met tussenpozen van 1 seconde.
* **Betrokkenheid stimuleren**: Betrek gebruikers volledig door minder buffergebeurtenissen en door te begrijpen waar en wanneer de advertenties binnen content moeten worden afgespeeld om een soepele, minder opdringerige ervaring te bieden waardoor bezoeken worden herhaald.
* **Holistisch beeld**: Combineer meerdere datapunten bij al uw contentdistributeurs om volledig zicht op al uw media-activiteit te krijgen. Meet betrokkenheid en kijk/luister op alle mogelijke kanalen via de Federated Analytics-functie.
* **Meer granulariteit**: Evalueer het kijkgedrag op het meest gedetailleerde niveau, waaronder het tijdstip van individuele bezoeken, gelijktijdige kijkers/luisteraars per minuut, en de gemiddelde duur van gebruik van de content.
* **Nauwkeurige meting**: Meet op meerdere apparaten die worden gebruikt voor mediaverbruik, waaronder OTT, smartphone, tablet, desktop, enz., om de patronen en gewoonten van de gebruikersbetrokkenheid bij te houden.
* **Segmentering**: Pas classificaties toe op uw spelers, apparaten, genres en hoofdstukken, en laat zien hoe ze elk invloed hebben op uw totaal aan weergaven en klantenbetrokkenheid bij content, audio, advertenties en combinaties daarvan.

## Hartbeatmeting {#heartbeat}

Adobe Analytics gebruikt ‘heartbeats’ om videostatistieken te verzamelen. Tijdens het afspelen van video worden heartbeats naar de heartbeat-trackingserver verzonden om de afspeeltijd te meten. De heartbeatsignalen worden om de tien seconden verzonden. Heartbeats resulteren in gedetailleerde videobetrokkenheidsstatistieken en nauwkeurigere video-uitvalrapporten. Met Adobe Analytics voor audio en video worden heartbeats gemeten met behulp van Adobe Launch met de extensie Media Analytics, de Media SDK en de Media Collection API. De componenten `AppMeasurement` en `VisitorID` worden gebruikt om videodata te ontvangen.

Het gebruik van heartbeats in Adobe Analytics voor audio en video biedt de volgende voordelen:

| Functie | Beschrijving |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Mediagebeurtenissen | Gedetailleerde en aangepaste gebeurtenissen worden elke 10 seconden verzonden voor de hoofdinhoud en elke seconde voor advertenties |
| Statistieken en dimensies | Duidelijke, gestandaardiseerde statistieken, dimensies en benchmarks voor verkopers<br>Met een gestandaardiseerde oplossing op alle platforms kunt u consistente, gestandaardiseerde variabelen op al uw media en platforms gebruiken om een efficiëntere vergelijking voor verschillende campagnes, apparaten en verkopers mogelijk te maken. |
| Integraties | De Experience Cloud-ID is gekoppeld aan Adobe Experience Cloud voor eenvoudigere kruisanalyse<br>Met de automatische integratie van Adobe Experience Cloud kunt u uw mediapubliek segmenteren, dit publiek gericht benaderen en media-aanbevelingen doen op basis van gebruikersvoorkeuren. |
| Prijzen | Transparant bijhouden via mediastream (enkel) |
| Implementatie en ondersteuning | Gestroomlijnde configuratie met doorlopende updates en verbeteringen<br>Met een gestroomlijnd implementatieproces kunt u snel variabelen toewijzen via de speler-API en implementaties valideren met de Adobe Debug-tool om ervoor te zorgen dat alle benodigde variabelen correct worden bijgehouden. |
| Delen via partners | Federated Analytics en Certified Metrics<br>Met gedeelde data via Federated Analytics kunt u gebruikmaken van onze toonaangevende mogelijkheden voor delen om data holistisch te evalueren via al uw mediadistributiepartners: operators, programmeurs, en distributeurs. |
| Geavanceerde tracking | Tracking van gedownloade content, tracking van foutherstel en gelijktijdige kijkers:<br>U kunt audio- en video-inhoud bijhouden die wordt gedownload en afgespeeld op een apparaat, ongeacht de connectiviteit hiervan. |



## Beveiliging {#security}

Bij Adobe nemen we de beveiliging van uw digitale assets serieus. Van de rigoureuze integratie van beveiliging in ons interne softwareontwikkelingsproces en onze tools tot onze functieoverschrijdende responsteams voor incidenten: wij streven ernaar proactief en flexibel te zijn. Verder helpen onze samenwerking met partners, onderzoekers en andere brancheorganisaties ons de nieuwste dreigingen en best practices op het gebied van beveiliging te begrijpen, en zorgen we ervoor dat de producten en services die we aanbieden voortdurend veilig zijn.


### Transport Layer Security {#transport-layer-security}

**TLS-kennisgeving**: Adobe heeft beveiligingscompatibiliteitsnormen waarvoor einde-levensduur van oudere beveiligingsprotocollen vereist is. Om te blijven voldoen aan de evoluerende normen van veiligheidsprotocollen is Adobe op weg naar van TLS 1.2 om de meest actuele en veilige versie te gebruiken. Vanaf 20 februari 2019 biedt Adobe alleen nog ondersteuning voor TLS 1.1 of hoger. Met deze wijziging verzamelt Adobe geen data meer van eindgebruikers met oudere apparaten of webbrowsers die gebruikmaken van TLS 1.0. Migratie naar TLS 1.2 biedt betere beveiliging. Het is belangrijk dat u de details doorloopt en de wijzigingen plant voor een vloeiende overgang.

>[!NOTE]
>
>TLS is momenteel het meest gebruikte veiligheidsprotocol in webbrowsers en andere toepassingen waarin data veilig over een netwerk worden uitgewisseld.
