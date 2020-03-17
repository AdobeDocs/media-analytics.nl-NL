---
title: Audio en video meten in Adobe Analytics
description: 'Adobe Analytics for Media (ook wel Media Analytics genoemd) biedt clients robuuste media-metingen voor inhoud, audio en advertenties. '
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
translation-type: tm+mt
source-git-commit: 689b7d4ce632d3ddba6704bb8040eec52bfc326f

---


# Audio en video meten in Adobe Analytics{#measuring-audio-and-video-in-adobe-analytics}

![Banner](./assets/media_analytics_banner.png)

>[!IMPORTANT]
>
>De documentatie die hier wordt geleverd, is specifiek voor clients die versie 1.5 of hoger van de SDK *van Adobe* Media gebruiken voor hartslagmeting, of de nieuwere API *voor* Media Collection van Adobe voor hartslagmeting. Het omvat geen instructies rond de erfenisMijlestone videoimplementatie. We moedigen alle klanten aan om over te stappen op het toepassen van één of beide van de nieuwste oplossingen voor mediatracering, zodat ze kunnen profiteren van verbeteringen en uitgebreide metingen. U kunt de [voordelen van de overgang naar de nieuwste oplossingen](media-overview.md#heartbeat-versus-milestone-benefits) hieronder bekijken. Hoewel we de mijlpaalmethode voor het bijhouden van video&#39;s blijven ondersteunen, zijn er geen geplande updates, oplossingen of verbeteringen aan functies. Neem contact op met uw accountmanager van Adobe als u nog vragen hebt.

## Overzicht {#overview}

Adobe Analytics for Media (ook wel Media Analytics genoemd) is een invoegtoepassing voor de basisanalysemogelijkheden die clients een robuuste mediummeting biedt voor inhoud, audio en advertenties. Media Analytics biedt klanten veel voordelen om real-time bewaking, gedetailleerde analyse, actioneerbare inzichten en mogelijkheden voor monetisering mogelijk te maken.

Het volgen van media wordt toegelaten door één van beiden van het volgende:

* **Media SDK -** integreert met de meest gebruikte mediaspelers.
* **Media Collection API -** (RESTful API) integreert met spelers waarvoor geen SDK steun (of met spelers waarvoor geen integratie SDK wordt gewenst) is.

Met Adobe Analytics for Media kunnen klanten de volledige reis van hun klanten over hun site volgen, inclusief mediaconsumptie. Deze maatregelen zijn eenvoudig geïntegreerd in Analytics-rapporten en andere Experience Cloud-producten. Met mediummeting kunt u uw gegevens in meerdere dimensies en segmenten segmenteren en alle metagegevens vastleggen die u nodig hebt voor een volledige, gedetailleerde analyse en om succescriteria toe te wijzen aan volledig verbruikte media, gemiddelde doorgebrachte tijd en voltooide advertenties.

De media oplossingen meten niet alleen vitale leveringsmetriek met betrekking tot QoS, zoals gelaten vallen kaders, tijd doorgebrachte het als buffer optreden voor, en gemiddelde bitrate. Ze kunnen ook worden gecombineerd met uw website- of toepassingsgegevens om de stroom van de klant en zijn belangen te visualiseren, zodat u beter aanbevelingen kunt doen en uw ervaringen kunt aanpassen via de Adobe Experience Cloud.

## Voordelen {#benefits}

De mediametingoplossingen van Adobe bieden onder andere de volgende voordelen:

* **Tijdige analyse -** maak real-time, uitvoerbare besluiten gebruikend zeer belangrijke prestatiesmetriek (b.v., duur) over veelvoudige kanalen. Gebeurtenissen met betrekking tot de hoofdinhoud worden gemeten met tussenpozen van **10 seconden** om alle activiteit vast te leggen zoals deze plaatsvindt. Gebeurtenissen voor het bijhouden van toevoegingen vinden plaats met een interval van **1 seconde** .
* **De betrokkenheid van de aandrijving -** verbind gebruikers volledig door minder het bufferen gebeurtenissen en door inzicht waar en wanneer de advertenties binnen inhoud moeten spelen om een vlotte, minder opdringerige ervaring te verstrekken die gebruikers terugbrengt en herhaalde bezoeken levert.
* **Holistisch beeld -** Combineer veelvoudige gegevenspunten over al uw inhoudsverdelers om een volledig overzicht van al uw media activiteit te krijgen, en meet betrokkenheid en meningen/luistert over alle mogelijke kanalen door de [Federated Analytics](/help/federated-analytics.md) eigenschap.
* **Meer granulariteit: evalueer het** bekijken gedrag op het meest korrelige niveau, met inbegrip van individuele bezoekerstijd van dag, gezamenlijke kijkers/luisteraars door minuut, en gemiddelde duur de inhoud werd verbruikt.
* **Nauwkeurige meting -** Meet over de veelvoudige apparaten die voor media consumptie, met inbegrip van OTT, smartphone, tablet, Desktop, en meer worden gebruikt, om de patronen en gewoonten van de gebruikersbetrokkenheid te controleren.
* **Segmentering -** Pas classificaties toe op uw spelers, apparaten, genres, hoofdstukken en laat zien hoe elk een invloed heeft op uw algemene meningen/luistert en klantenbetrokkenheid bij inhoud, audio, advertenties, en gecombineerde.

## Voordelen van hartslag versus mijlpaal {#heartbeat-versus-milestone-benefits}

Adobe Analytics for Media kan op twee manieren worden gemeten: de oudere methode van de Mijlpaal (video slechts) en de huidige methode Heartbeats (audio en video, die in zowel Media SDK als de Inzameling API van Media wordt omvat). De methode Heartbeats heeft de voorkeur en we raden alle clients aan naar deze versie te gaan als ze dat nog niet hebben gedaan, om de hieronder beschreven voordelen te benutten.

De oudere methode van Milestone is gebaseerd op individuele servervraag aan de server van Analytics, voor videobegin, kwartielen, duur, en voltooit. De methode Heartbeats biedt een robuustere oplossing voor mediatracering waarmee de belangrijkste inhoud met intervallen van 10 seconden wordt gemeten voor verbeterde, gestandaardiseerde meetgegevens. Daarnaast heeft Adobe lessen geleerd van onze mijlpaalmethode om een vloeiender, gestroomlijnd implementatieproces te bieden via de Media SDK of de Media Collection API die door Heartbeats wordt gebruikt.

Enkele vele voordelen van de methode Heartbeats omvatten:

* **Gestroomlijnd implementatieproces -** Wijs variabelen gemakkelijker toe via de speler-API en valideer implementaties via Adobe Debug Tool om ervoor te zorgen dat alle benodigde variabelen correct worden bijgehouden.
* **Automatische integratie** in de cloud van Adobe Experience - Profiteer van de automatische integratie met de Adobe Experience Cloud-id via Experience Cloud-id, deel uw mediapubliek, wijs deze aan en voer op basis van gebruikersvoorkeuren mediumaanbevelingen uit.
* **Gedeelde gegevens door Federale Analytics -** Capitalize op onze industrie-eerste media delend mogelijkheden, om gegevens holistisch over al uw media distributie partners-exploitanten, programmeurs, en verdelers te evalueren.
* **Gestandaardiseerde oplossing voor alle platforms -** Zorg voor consistente, gestandaardiseerde variabelen voor al uw media en platforms, zodat een efficiëntere vergelijking tussen campagne, apparaat en leverancier mogelijk is.
* **Gedownloade inhoud bijhouden -** Media-inhoud (video en audio) bijhouden die op een apparaat wordt gedownload en afgespeeld, ongeacht de connectiviteit ervan.

### Vergelijkingstabel

|  | Video-analyse - Mijlpaal | Media Analytics - Heartbeats |
|---|---|---|
| **Media-gebeurtenissen** | Standaardgebeurtenissen op hoog niveau | Gedetailleerde en aangepaste gebeurtenissen om de 10 jaar voor de hoofdinhoud, elke 1 seconden voor advertenties |
| **Metriek en afmetingen** | Verschillen tussen leveranciers, niet-gestandaardiseerde meeteenheden en afmetingen | Duidelijke, Gestandaardiseerde Metriek, Afmetingen, en Benchmarks over Verkopers |
| **Integraties met Adobe-producten** | Afzonderlijke sessies met sommige toewijzingen en integratie | Created Experience Cloud ID gekoppeld aan de volledige Adobe Experience Cloud voor eenvoudige kruisanalyse |
| **Prijzen** | Op elke serveroproep bijgehouden en gefactureerd | Transparant bijhouden via mediastream (één) |
| **Implementatie en ondersteuning** | Langere integratie met beperkte ondersteuning voor oudere versies en geen upgrades | Gestroomlijnde configuratie met doorlopende updates en verbeteringen |
| **Delen van partners** | N.v.t. | Federatieve analyse en gecertificeerde meetgegevens |
| **Geavanceerd bijhouden** | N.v.t. | Foutherstel bijhouden en gelijktijdige viewers |

## Ondersteunde apparaten {#devices-supported}

Adobe Analytics for Media heeft zich samen met de branche ontwikkeld om krachtige gereedschappen voor gegevensverzameling te bieden, zodat elke mediastream wordt verzameld en gerapporteerd op alle relevante apparaten. Onze Media SDK is ontwikkeld voor alle meest gebruikte apparaten, waaronder:

* iOS- en Android-smartphones en -tablets
* OTT-apparaten voor ROKU, AppleTV, FireTV en Android TV
* JavaScript-browser voor bureaublad en laptop

SDK&#39;s worden routinematig bijgewerkt wanneer nieuwe versies van apparaten worden uitgebracht. Met deze SDK&#39;s kunt u de integratie tot stand brengen met de meeste van de grootste mediaspelers op dit moment, waaronder Brightcove en Ooyala.

Voor apparaten of platforms die momenteel geen SDK-ondersteuning hebben (of zelfs als dat wel het geval is), kunt u de API voor mediagroep implementeren, waarmee u RESTful-API-aanroepen rechtstreeks van het apparaat/platform naar de achtergrond voor Media Analytics maakt.

De onderstaande tabel bevat een lijst met de apparaten die momenteel worden ondersteund via de implementatie van de Media SDK en de implementatie van de Media Collection API. Zie SDK&#39;s [downloaden voor informatie over het downloaden van de meest recente versie van de SDK.](sdk-implement/download-sdks.md) Als er een apparaat is dat niet in de lijst wordt vermeld waarop u meting zoekt, gelieve de klantenzorg of uw oplossingsadviseur voor de status van dat apparaat te contacteren.

|      | Media SDK | Media Collection-API |
|---|:---:|:---:|
| **JavaScript-browser** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **iOS-apparaten** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Android-apparaten** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Verenigde Platforms van Vensters (UWP)** |  | ![](assets/icon-blue-check.png) |
| **Blackberry** |  | ![](assets/icon-blue-check.png) |
| **Apple TV (nieuw/verouderd)** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **ROKU (JS)** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **ROKU (native app)** |  | ![](assets/icon-blue-check.png) |
| **OSX** |  | ![](assets/icon-blue-check.png) |
| **Fire TV** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Android-tv** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Chromecast** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Xbox One/360** |  | ![](assets/icon-blue-check.png) |
| **Sony PS3/PS4** |  | ![](assets/icon-blue-check.png) |
| **(Andere/nieuwe aangesloten apparaten)** |  | ![](assets/icon-blue-check.png) |

Voor Media SDK, zie ook de [Minimale Steun van de Versie van het Platform](./sdk-implement/setup/setup-overview.md#minimum-platform-version)

## Transport Layer Security {#transport-layer-security}

**TLS-kennisgeving —** Adobe heeft beveiligingscompatibiliteitsnormen die het einde van de levensduur van oudere beveiligingsprotocollen vereisen. Om te blijven voldoen aan de evoluerende normen van het veiligheidsprotocol, beweegt Adobe zich op weg naar het gebruik van TLS 1.2, om de meest bijgewerkte en veilige versie in gebruik te hebben. Vanaf 20 februari 2019 biedt Adobe alleen ondersteuning voor TLS 1.1 of hoger. Met deze wijziging verzamelt Adobe geen gegevens meer van eindgebruikers met oudere apparaten of webbrowsers die TLS 1.0 gebruiken. Migratie naar TLS 1.2 biedt betere beveiliging. Het is belangrijk dat u de details doorloopt en de wijzigingen uitwerkt voor een vloeiende overgang.

>[!NOTE]
>
>TLS is momenteel het wijdst opgestelde veiligheidsprotocol dat in Webbrowsers en andere toepassingen wordt gebruikt die gegevens vereisen om veilig over een netwerk worden geruild.

