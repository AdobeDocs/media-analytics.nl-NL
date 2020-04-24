---
title: Audio en video meten in Adobe Analytics
description: 'Adobe Analytics voor Media (ook wel Media Analytics genoemd) biedt clients robuuste mediametingen voor content, audio en advertenties. '
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
translation-type: ht
source-git-commit: 689b7d4ce632d3ddba6704bb8040eec52bfc326f

---


# Audio en video meten in Adobe Analytics {#measuring-audio-and-video-in-adobe-analytics}

![Banner](./assets/media_analytics_banner.png)

>[!IMPORTANT]
>
>De documentatie die hier wordt geboden, is specifiek voor klanten die versie 1.5 of hoger van de *Media-SDK* van Adobe, of de nieuwere *Media Collection-API* van Adobe gebruiken voor hartslagmeting. De documentatie omvat geen instructies voor de verouderde Milestone-video-implementatie. We moedigen alle klanten aan om over te stappen op één of beide van de twee nieuwste oplossingen voor mediatracking om te kunnen profiteren van verbeteringen en uitgebreide metingen. U kunt de [voordelen van de overstap naar de nieuwste oplossingen](media-overview.md#heartbeat-versus-milestone-benefits) hieronder bekijken. Hoewel we de Milestone-methode voor het bijhouden van video&#39;s blijven ondersteunen, zullen er geen geplande updates, oplossingen of functieverbeteringen komen. Neem contact op met uw Adobe-accountmanager als u nog vragen hebt.

## Overzicht {#overview}

Adobe Analytics voor Media (ook wel Media Analytics genoemd) is een invoegtoepassing voor de basistoepassing Analytics, waarmee clients een robuuste mediameting binnenhaalt voor content, audio en advertenties. Media Analytics biedt klanten veel voordelen voor realtimecontrole, gedetailleerde analyse, uitvoerbare inzichten en mogelijkheden voor monetisatie.

Mediatracking wordt ingeschakeld door een van de twee volgende items:

* **Media SDK -** integreert met de meest gebruikte mediaspelers.
* **Media Collection API -** (RESTful API) integreert met spelers waarvoor geen SDK-ondersteuning is (of met spelers waarvoor geen SDK-integratie vereist is).

Met Adobe Analytics voor Media kunnen klanten het volledige klanttraject op hun site volgen, inclusief mediaconsumptie. Deze metingen kunnen gemakkelijk worden geïntegreerd in Analytics-rapporten en andere Experience Cloud-producten. Met mediametingen kunt u uw data in meerdere dimensies en segmenten opsplitsen en zo alle metadata vastleggen die u nodig hebt om een volledige, gedetailleerde analyse te maken, en om succescriteria toe te wijzen aan volledig gebruikte media, gemiddelde doorgebrachte tijd en voltooide advertenties.

De mediaoplossingen meten niet alleen essentiële leveringsstatistieken in verband met QoS, zoals dropped frames, buffertijd en gemiddelde bitsnelheid. Ze kunnen ook worden gecombineerd met uw website- of appdata om de stroom en de interesses van de klant zichtbaar te maken, zodat u betere aanbevelingen kunt doen en hun ervaringen kunt aanpassen via de Adobe Experience Cloud.

## Voordelen {#benefits}

De mediametingsoplossingen van Adobe bieden onder andere de volgende voordelen:

* **Tijdige analyse -** Neem uitvoerbare, realtimebesluiten aan de hand van de belangrijkste prestatiestatistieken (b.v. duur) via meerdere kanalen. Gebeurtenissen in verband met hoofdcontent worden gemeten met tussenpozen van **10 seconden** om alle activiteit vast te leggen terwijl deze plaatsvindt. Gebeurtenissen in verband met het bijhouden van advertenties vinden plaats met tussenpozen van **1 seconde**.
* **Betrokkenheid stimuleren -** Betrek gebruikers volledig door minder buffergebeurtenissen en door te begrijpen waar en wanneer de advertenties binnen content moeten worden afgespeeld spelen voor een soepele, minder opdringerige ervaring te verstrekken waardoor gebruikers terugkomen en hun bezoeken herhalen.
* **Holistisch beeld -** Combineer meerdere datapunten bij al uw contentdistributeurs om volledig zicht op al uw media-activiteit te krijgen, betrokkenheid te meten en te kijken/luisteren op alle mogelijke kanalen via de [Federated Analytics](/help/federated-analytics.md)-functie.
* **Meer granulariteit -** Evalueer het kijkgedrag op het meest gedetailleerde niveau, waaronder het tijdstip van individuele bezoeken, gelijktijdige kijkers/luisteraars per minuut, en de gemiddelde duur van gebruik van de content.
* **Nauwkeurige meting -** Meet op meerdere apparaten die worden gebruikt voor mediaverbruik, waaronder OTT, smartphone, tablet, desktop, enz., om de patronen en gewoonten van de gebruikersbetrokkenheid bij te houden.
* **Segmentering -** Pas classificaties toe op uw spelers, apparaten, genres en hoofdstukken, en laat zien hoe ze elk invloed hebben op uw totaal aan weergaven en klantenbetrokkenheid bij content, audio, advertenties en combinaties daarvan.

## Voordelen van Heartbeat versus Milestone {#heartbeat-versus-milestone-benefits}

Adobe Analytics voor Media kan op twee manieren worden gemeten: de oudere Mijlpaal-methode (alleen video) en de huidige Heartbeats-methode (audio en video, aanwezig in zowel de Media SDK als de Media Collection-API). De Heartbeats-methode is de geprefereerde meetmethode en we raden alle klanten aan op deze versie over te stappen als ze dat nog niet hebben gedaan, zodat ze van de hieronder beschreven voordelen kunnen profiteren.

De oudere Milestone-methode is gebaseerd op individuele server calls aan de Analytics-server voor starts, kwartielen, duur, en voltooiingen van video. De methode Heartbeats biedt een robuustere oplossing voor mediatracking waarmee de belangrijkste content wordt gemeten met tussenpozen van 10 seconden voor verbeterde, gestandaardiseerde statistieken. Daarnaast heeft Adobe van onze Milestone-methode geleerd om een vloeiender, gestroomlijnder implementatieproces te bieden via de Media SDK of de Media Collection-API die door Heartbeats wordt gebruikt.

Een paar van de vele voordelen van de Heartbeats-methode:

* **Gestroomlijnd implementatieproces -** Wijs variabelen gemakkelijker toe via de speler-API en valideer implementaties via het Adobe Debug-gereedschap om ervoor te zorgen dat alle vereiste variabelen correct worden bijgehouden.
* **Automatische Adobe Experience Cloud-integratie** - profiteer van de automatische integratie met de Adobe Experience Cloud via de Experience Cloud ID, segmenteer uw mediadoelgroepen, target deze en doe media-aanbevelingen op basis van gebruikersvoorkeuren.
* **Gedeelde data via Federated Analytics -** Maak gebruik van onze marktleidende mogelijkheden voor delen via media om data holistisch te evalueren via al uw mediadistributiepartners: operators, programmeurs, en distributeurs.
* **Gestandaardiseerde oplossing op alle platforms -** Zorg voor consistente, gestandaardiseerde variabelen bij al uw media en platforms om een efficiëntere vergelijking tussen campagnes, apparaten en leveranciers mogelijk te maken.
* **Gedownloade inhoud bijhouden -** Houd mediacontent (video en audio) bij die op een apparaat wordt gedownload en afgespeeld, ongeacht de connectiviteit.

### Vergelijkingstabel

|  | Video Analytics - Milestone | Media Analytics - Heartbeats |
|---|---|---|
| **Mediagebeurtenissen** | Standaardgebeurtenissen op hoog niveau | Gedetailleerde en aangepaste gebeurtenissen elke de 10 seconden voor hoofdcontent, elke seconde voor advertenties |
| **Statistieken en dimensies** | Verschillen tussen leveranciers, niet-gestandaardiseerde statistieken en dimensies | Duidelijke, gestandaardiseerde statistieken, dimensies en benchmarks van leveranciers |
| **Integraties met Adobe-producten** | Individuele sessies met een aantal toewijzingen en integraties | Verbonden Experience Cloud ID gekoppeld aan de volledige Adobe Experience Cloud voor eenvoudige kruisanalyse |
| **Prijzen** | Bijgehouden en gefactureerd tegen elke server call | Transparant bijhouden via mediastream (enkel) |
| **Implementatie en ondersteuning** | Langere integraties met beperkte ondersteuning voor oudere versies en geen upgrades | Gestroomlijnde configuratie met doorlopende updates en verbeteringen |
| **Delen via partners** | N.v.t. | Federated Analytics en gecertificeerde statistieken |
| **Geavanceerde tracking** | N.v.t. | Foutherstel bijhouden en gelijktijdige kijkers |

## Ondersteunde apparaten {#devices-supported}

Adobe Analytics voor Media heeft zich binnen de branche ontwikkeld om krachtige gereedschappen voor dataverzameling te bieden, zodat elke mediastream wordt verzameld en gerapporteerd op alle relevante apparaten. Onze Media SDK is ontwikkeld voor de meest gebruikte apparaten, waaronder:

* iOS- en Android-smartphones en -tablets
* OTT-apparaten voor ROKU, AppleTV, FireTV en Android TV
* JavaScript-browser voor desktop en laptop

De SDK&#39;s worden routinematig bijgewerkt wanneer nieuwe versies van apparaten worden uitgebracht. Met deze SDK&#39;s kunt u integreren met de meeste grote mediaspelers op dit moment, waaronder Brightcove en Ooyala.

Voor apparaten of platforms die momenteel geen SDK-ondersteuning hebben (of zelfs als ze dat wel hebben), kunt u de Media Collection-API implementeren, waarmee u RESTful-API-calls rechtstreeks van het apparaat/platform naar de Media Analytics-back-end maakt.

De onderstaande tabel bevat een lijst met de apparaten die momenteel worden ondersteund via onze Media SDK-implementatie en de Media Collection-API-implementatie. Zie [SDK&#39;s downloaden voor informatie over het downloaden van de meest recente versie van de SDK.](sdk-implement/download-sdks.md) Als een apparaat niet in de lijst wordt vermeld waarvoor u metingen wilt, neemt u contact op met de klantenservice of uw consultant voor oplossingen om de status van het apparaat te achterhalen.

|      | Media-SDK | Media Collection-API |
|---|:---:|:---:|
| **JavaScript-browser** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **iOS-apparaten** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Android-apparaten** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Unified Windows Platforms (UWP)** |  | ![](assets/icon-blue-check.png) |
| **Blackberry** |  | ![](assets/icon-blue-check.png) |
| **Apple TV (nieuw/verouderd)** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **ROKU (JS)** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **ROKU (native app)** |  | ![](assets/icon-blue-check.png) |
| **OSX** |  | ![](assets/icon-blue-check.png) |
| **Fire-tv** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Android-tv** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Chromecast** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Xbox One/360** |  | ![](assets/icon-blue-check.png) |
| **Sony PS3/PS4** |  | ![](assets/icon-blue-check.png) |
| **(Andere/nieuwe aangesloten apparaten)** |  | ![](assets/icon-blue-check.png) |

Zie voor Media SDK ook de [Ondersteuning voor minimale platformversie](./sdk-implement/setup/setup-overview.md#minimum-platform-version)

## Transport Layer Security {#transport-layer-security}

**TLS-kennisgeving -** Adobe heeft beveiligingscompatibiliteitsnormen waarvoor einde-levensduur van oudere beveiligingsprotocollen vereist is. Om te blijven voldoen aan de evoluerende normen van veiligheidsprotocollen is Adobe op weg naar van TLS 1.2 om de meest actuele en veilige versie te gebruiken. Vanaf 20 februari 2019 biedt Adobe alleen nog ondersteuning voor TLS 1.1 of hoger. Met deze wijziging verzamelt Adobe geen data meer van eindgebruikers met oudere apparaten of webbrowsers die gebruikmaken van TLS 1.0. Migratie naar TLS 1.2 biedt betere beveiliging. Het is belangrijk dat u de details doorloopt en de wijzigingen plant voor een vloeiende overgang.

>[!NOTE]
>
>TLS is momenteel het meest gebruikte veiligheidsprotocol in webbrowsers en andere toepassingen waarin data veilig over een netwerk worden uitgewisseld.

