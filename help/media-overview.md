---
title: Overzicht van invoegtoepassing voor Adobe streaming media
description: Gebruik de invoegtoepassing voor het streamen van mediaconzameling voor een krachtig inzicht in inhoud, audio en advertenties.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 9%

---

# Overzicht van invoegtoepassing voor Adobe streaming media

![Banner](./assets/media_analytics_banner.png)

De invoegtoepassing voor het streamen van media-Adobe biedt krachtige gereedschappen voor het verzamelen, meten en aanpassen van inhoud voor streaming media, zoals audio, video en advertenties voor streaming media providers. U kunt streaming media metriek met mogelijkheden zoals Audience Analytics, Mobiel, of de Analyse van het Apparaat combineren.

Streaming mediagegevens kunnen eenvoudig worden geïntegreerd in de volgende Adobe Experience Platform-producten:

* Adobe Analytics

* Customer Journey Analytics

* Adobe Journey Optimizer

* Real-Time Customer Data Platform

>[!IMPORTANT]
>
>Om het stromen media inzameling uit te voeren, contacteer uw Vertegenwoordiger van de Adobe of het Team van de Rekening van de Adobe om ervoor te zorgen de Streaming Invoegsel van de Inzameling van Media deel van uw productportefeuille uitmaakt.

## Belangrijkste kenmerken

De voordelen van de invoegtoepassing voor het streamen van media omvatten real-time bewaking, gedetailleerde analyse, actioneerbare inzichten, mogelijkheden voor monetisering en meer.

* **Analyse in realtime**: Maak beslissingen in real time, uitvoerbaar met behulp van prestatiekernwaarden zoals het mediakanaal, op meerdere kanalen.

  Met de Invoegtoepassing voor de verzameling van streaming media krijgt u bijna realtime, gedetailleerde details over de duur, stops en het begin waarmee u video- en audiomeetgegevens kunt evalueren en combineren. Met deze inzichten kunt u de kijkgewoonten en de luistergewoonten van uw klanten begrijpen en de betrokkenheid met zeer persoonlijke aanbevelingen verhogen.

* **Drive-service**: Gebruik gebruikers volledig door minder buffergebeurtenissen en door te begrijpen waar en wanneer advertenties binnen inhoud moeten worden afgespeeld voor een vloeiende, minder opdringerige ervaring die herhaalde bezoeken mogelijk maakt.

* **Holistisch beeld**: Combineer meerdere gegevenspunten voor al uw inhoudsdistributeurs om een volledig beeld van al uw media activiteit te krijgen. Meet de betrokkenheid en de weergaven/luistert over alle mogelijke kanalen.

  Met de invoegtoepassing voor de verzameling van streaming media kunt u de volledige reis van de klant over uw site en streaming apps volgen om het pad en de interesses van de klant te visualiseren en verbeterde aanbevelingen te bieden en de ervaringen van de klant aan te passen.  Met mediameting kunt u uw data indelen in meerdere dimensies en segmenten, en zo alle metadata vastleggen die u nodig hebt voor een volledige en gedetailleerde analyse. Vervolgens kunt u data analyseren en succescriteria toewijzen aan volledig verbruikte media, gemiddelde bestede tijd en voltooide advertenties.

* **Vitale cijfers**: Metrisch met betrekking tot vitale leveringsmetriek met betrekking tot de Kwaliteit van Ervaring (QoE) zoals gelaten vallen kaders, tijd doorgebrachte het bufferen, en gemiddelde bitsnelheid meten.

* **Meer granulariteit**: Evalueer het weergavegedrag op het meest korrelige niveau, inclusief de individuele bezoekerstijd van de dag, gelijktijdige viewers of listeners per minuut en de gemiddelde duur waarop de inhoud is verbruikt.

* **Nauwkeurige meting**: Meet op de verschillende apparaten die worden gebruikt voor mediaconsumptie, zoals OTT, smartphone, tablet, desktop en nog veel meer, om de betrokkenheidspatronen en -gewoonten van gebruikers te volgen.

* **Segmentering**: Pas classificaties toe op uw spelers, apparaten, genres, hoofdstukken en laat zien hoe elk een invloed heeft op uw algemene weergaven/luistert en de betrokkenheid van klanten bij inhoud, audio, advertenties en gecombineerde inhoud.


## Hoe werkt het

Gegevens voor het bijhouden van streaming media worden verzameld bij een speler met de Media for Edge Network SDK/Extension, Media Extension with Tags, Media SDKs, Media Edge API of de Media Collection API.

Alle gegevens in korrelvorm (maximaal 10 seconden) worden naar de Media Analytics Service of Experience Edge verzonden (afhankelijk van de [implementatiemethode](/help/implementation/overview.md) u kiest), die de gegevens voor elke afzonderlijke afspeelsessie verzamelen en verwerken.

Nadat een afspeelsessie is beëindigd, worden de gegevens voor het bijhouden van de gegevens naar Adobe Analytics of Customer Journey Analytics verzonden voor opslag en rapportage.

>[!NOTE]
>
>Met de implementaties van de Customer Journey Analytics, kunnen de gegevens naar Customer Journey Analytics of gebruikend Ervaring Edge of het gebruiken van de Verbinding van Gegevens van de Analyse (ADC) worden verzonden.


Zie voor meer informatie over de verschillende implementatiemethoden [Implementeer de invoegtoepassing voor het streamen van media-verzamelingen voor Adobe Analytics of Customer Journey Analytics](/help/implementation/overview.md).
