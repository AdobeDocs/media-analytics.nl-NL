---
title: Overzicht van Adobe Analytics voor Streaming Media
description: Gebruik de Analyse van de Media van de Streaming om krachtig inzicht voor inhoud, audio, en reclame te krijgen.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b12e6547ef32bfad7e8d6787a26d6467bcfeb23c
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 9%

---

# Overzicht van Adobe Analytics voor Streaming Media

![Banner](./assets/media_analytics_banner.png)

Adobe Analytics for Streaming Media biedt krachtige meetgereedschappen voor audio, video en advertenties. U kunt de meetgegevens van streaming media combineren met andere Adobe Analytics-mogelijkheden, zoals Audience Analytics, Mobiel of Apparaatanalyse.

Streaming media kunnen worden aangeschaft als invoegtoepassing voor Adobe Analytics<!-- update this when SKUs are available for other AEP products -->en Streaming media-meetgegevens kunt u eenvoudig integreren in de volgende Adobe Experience Platform-producten:

* Adobe Analytics

* Customer Journey Analytics

* Adobe Journey Optimizer

* Real-Time Customer Data Platform

>[!IMPORTANT]
>
>Als u Adobe Analytics Streaming Media wilt implementeren, neemt u contact op met uw Adobe-verkoper of Adobe-accountteam om ervoor te zorgen dat Streaming Media deel uitmaakt van uw productportfolio.

## Belangrijkste kenmerken

De voordelen van Adobe Analytics voor Streaming Media zijn real-time bewaking, gedetailleerde analyse, inzichten die in actie kunnen worden gebracht, mogelijkheden voor monetisering en meer.

* **Analyse in realtime**: Maak beslissingen in real time, uitvoerbaar met behulp van prestatiekernwaarden zoals het mediakanaal, op meerdere kanalen.

  Met Analytics voor Streaming Media krijgt u bijna real-time, gedetailleerde details over de duur, stops en het begin waarmee u video- en audiomeetgegevens kunt evalueren en combineren. Met deze inzichten kunt u de kijkgewoonten en de luistergewoonten van uw klanten begrijpen en de betrokkenheid met zeer persoonlijke aanbevelingen verhogen.

* **Drive-service**: Gebruik gebruikers volledig door minder buffergebeurtenissen en door te begrijpen waar en wanneer advertenties binnen inhoud moeten worden afgespeeld voor een vloeiende, minder opdringerige ervaring die herhaalde bezoeken mogelijk maakt.

* **Holistisch beeld**: Combineer meerdere gegevenspunten voor al uw inhoudsdistributeurs om een volledig beeld van al uw media activiteit te krijgen. Meet de betrokkenheid en de weergaven/luistert over alle mogelijke kanalen.

  Met Adobe Analytics for Streaming Media kunt u de volledige reis van de klant over uw site en streaming apps volgen om het pad en de interesses van de klant te visualiseren en verbeterde aanbevelingen te bieden en de ervaringen van de klant aan te passen.  Met mediameting kunt u uw data indelen in meerdere dimensies en segmenten, en zo alle metadata vastleggen die u nodig hebt voor een volledige en gedetailleerde analyse. Vervolgens kunt u data analyseren en succescriteria toewijzen aan volledig verbruikte media, gemiddelde bestede tijd en voltooide advertenties.

* **Vitale cijfers**: Metrisch met betrekking tot vitale leveringsmetriek met betrekking tot de Kwaliteit van Ervaring (QoE) zoals gelaten vallen kaders, tijd doorgebrachte het bufferen, en gemiddelde bitsnelheid meten.

* **Meer granulariteit**: Evalueer het weergavegedrag op het meest korrelige niveau, inclusief de individuele bezoekerstijd van de dag, gelijktijdige viewers of listeners per minuut en de gemiddelde duur waarop de inhoud is verbruikt.

* **Nauwkeurige meting**: Meet op de verschillende apparaten die worden gebruikt voor mediaconsumptie, zoals OTT, smartphone, tablet, desktop en nog veel meer, om de betrokkenheidspatronen en -gewoonten van gebruikers te volgen.

* **Segmentering**: Pas classificaties toe op uw spelers, apparaten, genres, hoofdstukken en laat zien hoe elk een invloed heeft op uw algemene weergaven/luistert en de betrokkenheid van klanten bij inhoud, audio, advertenties en gecombineerde inhoud.


## Hoe werkt het

Gegevens voor het bijhouden van streaming media worden verzameld bij een speler met de Media for Edge Network SDK/Extension, Media Extension with Tags, Media SDKs, Media Edge API of de Media Collection API.

Alle korrelgegevens (maximaal 10 seconden) worden naar de Media Analytics Service of Experience Edge verzonden (afhankelijk van de [implementatiemethode](/help/implementation/overview.md) u kiest), die de gegevens voor elke afzonderlijke afspeelsessie verzamelen en verwerken.

Nadat een afspeelsessie is beëindigd, worden de gegevens voor het bijhouden van de gegevens naar Adobe Analytics of Customer Journey Analytics verzonden voor opslag en rapportage.

>[!NOTE]
>
>Met Customer Journey Analytics-implementaties kunnen gegevens naar Customer Journey Analytics worden verzonden met Experience Edge of met ADC (Analytics Data Connector).


Zie voor meer informatie over de verschillende implementatiemethoden [Streaming media implementeren voor Adobe Analytics of Customer Journey Analytics](/help/implementation/overview.md).
