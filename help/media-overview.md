---
title: Overzicht van Adobe Analytics voor Streaming Media
description: Gebruik de Analyse van de Media van de Streaming om krachtig inzicht voor inhoud, audio, en reclame te krijgen.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 984f058fda15b1c5e960e4c8d8e2378308d2b541
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 8%

---

# Overzicht van Adobe Analytics voor Streaming Media

![Banner](./assets/media_analytics_banner.png)

Adobe Analytics for Streaming Media is een invoegtoepassing voor Adobe Analytics en Customer Journey Analytics die krachtige meetgereedschappen voor audio, video en advertenties biedt. Met Analytics voor Streaming Media krijgt u bijna real-time, gedetailleerde details over de duur, stops en het begin waarmee u video- en audiomeetgegevens kunt evalueren en combineren. Met deze inzichten kunt u de kijkgewoonten en de luistergewoonten van uw klanten begrijpen en de betrokkenheid met zeer persoonlijke aanbevelingen verhogen.

Met Adobe Analytics for Streaming Media kunt u de volledige reis van de klant over uw site en streaming apps volgen. U kunt de meetgegevens van streaming media combineren met andere Adobe Analytics-mogelijkheden, zoals Audience Analytics, Mobiel of Apparaatanalyse. De meetgegevens kunnen eenvoudig worden geïntegreerd in Adobe Analytics Reports en andere Adobe Experience Platform-producten. Met mediameting kunt u uw data indelen in meerdere dimensies en segmenten, en zo alle metadata vastleggen die u nodig hebt voor een volledige en gedetailleerde analyse. Vervolgens kunt u data analyseren en succescriteria toewijzen aan volledig verbruikte media, gemiddelde bestede tijd en voltooide advertenties.

U kunt vitale leveringsmetriek met betrekking tot de Kwaliteit van Ervaring (QoE) zoals gelaten vallen kaders, tijd doorgebrachte het als buffer optreden voor, en gemiddelde bitrate meten. En de metriek kan met uw website of toepassingsgegevens worden gecombineerd om het klantenweg en de rente-te visualiseren - om verbeterde aanbevelingen te verstrekken en klantenervaringen te personaliseren gebruikend Adobe Experience Platform.

>[!IMPORTANT]
>
>Als u Adobe Analytics Streaming Media wilt implementeren, neemt u contact op met uw Adobe-verkoper of Adobe-accountteam om ervoor te zorgen dat Streaming Media deel uitmaakt van uw productportfolio.


## Hoe werkt het

Gegevens voor het bijhouden van streaming media worden verzameld bij een speler met de Media for Edge Network SDK/Extension, Media Extension with Tags, Media SDKs, Media Edge API of de Media Collection API.

Alle korrelgegevens (maximaal 10 seconden) worden naar de Media Analytics Service of Experience Edge verzonden (afhankelijk van de [uitvoeringsmethode](/help/implementation/overview.md) u kiest), die de gegevens voor elke afzonderlijke afspeelsessie verzamelen en verwerken.

Nadat een afspeelsessie is beëindigd, worden de gegevens voor het bijhouden van de gegevens naar Adobe Analytics of Customer Journey Analytics verzonden voor opslag en rapportage.

>[!NOTE]
>
>Met Customer Journey Analytics-implementaties kunnen gegevens naar Customer Journey Analytics worden verzonden met Experience Edge of met ADC (Analytics Data Connector).


Zie [Streaming media implementeren voor Adobe Analytics of Customer Journey Analytics](/help/implementation/overview.md) voor meer informatie .

## Functies

Adobe-analysemogelijkheden voor de voordelen van streaming media zijn onder andere realtime bewaking, gedetailleerde analyse, inzichten die in actie kunnen worden gebracht en monetiseringsmogelijkheden.

* **Analyse in realtime**: Maak real-time, uitvoerbare besluiten gebruikend zeer belangrijke prestatiesmetriek zoals media begin, over veelvoudige kanalen.

* **Drive-service**: Gebruik gebruikers volledig door minder buffergebeurtenissen en door te begrijpen waar en wanneer advertenties binnen inhoud moeten worden afgespeeld voor een vloeiende, minder opdringerige ervaring die herhaalde bezoeken mogelijk maakt.

* **Holistisch beeld**: Combineer veelvoudige gegevenspunten over al uw inhoudsverdelers om een volledige mening van al uw media activiteit te krijgen. Meet de betrokkenheid en weergaven en luistert via alle mogelijke kanalen via de Federated Analytics-functie.

* **Meer granulariteit**: Evalueer het bekijken gedrag op het meest korrelige niveau, met inbegrip van individuele bezoekerstijd van dag, gezamenlijke kijkers of luisteraars door minuut, en gemiddelde duur de inhoud werd verbruikt.

* **Nauwkeurige meting**: Meet over de veelvoudige apparaten die voor media consumptie, met inbegrip van OTT, smartphone, tablet, Desktop, en meer worden gebruikt, om de patronen en gewoonten van de gebruikersbetrokkenheid te controleren.

* **Segmentering**: U past classificaties toe op uw spelers, apparaten, genres, hoofdstukken en laat zien hoe elk een invloed heeft op uw algemene weergaven/luistert en de betrokkenheid van de klant bij inhoud, audio, advertenties en gecombineerde inhoud.
