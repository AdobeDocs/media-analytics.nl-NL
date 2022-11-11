---
title: Welke paden voor het implementeren van streaming media zijn beschikbaar?
description: Meer informatie over implementatiepaden voor Adobe Streaming Media, waaronder Adobe Experience Platform-gegevensverzameling.
exl-id: eee70e62-ba45-440a-8ce1-e151b66d2c1f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 0%

---

# Implementatiepaden {#implementation-paths}

**DEZE INHOUD IS VERPLAATST NAAR HET HUIDIGE BESTAND MET IMPLEMENTATIEPADEN**

Voor elk implementatiepad moeten klanten contact opnemen met hun verkoper/accountmanager om een nieuwe verkooporder te ondertekenen omdat de Streaming Media Analytics een unieke SKU heeft en wijzigingen doorvoert van een prijsmodel dat is gebaseerd op serveraanroepen naar een model dat is gebaseerd op videostreams.

## Adobe Experience Platform Data Collection met de uitbreiding van de Analytics van Adobe Media

>[!NOTE]
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=en) voor een geconsolideerde referentie van de terminologische wijzigingen.


Tags in Adobe Experience Platform zijn de volgende generatie mogelijkheden voor tagbeheer van Adobe. Met labels kunnen klanten eenvoudig alle analytische, marketing- en advertentietags implementeren en beheren die nodig zijn om relevante klantervaringen te stimuleren. Tags worden aan Adobe Experience Cloud-klanten aangeboden als een inbegrepen functie voor het toevoegen van waarden.

Tags stellen iedereen in staat zijn eigen integraties te maken en te onderhouden, zogenaamde extensies. Deze extensies zijn beschikbaar voor Adobe Experience Cloud-klanten in een app-store-ervaring, zodat ze hun tags snel kunnen installeren, configureren en implementeren.

Een extensie is een pakket code (JavaScript, HTML en CSS) dat de functionaliteit voor tags uitbreidt. Ontwikkel, beheer, en werk uw integratie bij gebruikend een vrijwel zelfbedienings interface. U kunt extensies beschouwen als toepassingen die u gebruikt om uw taken uit te voeren. Zie de *Overzicht van codes* in het [Adobe Experience Platform-documentatie](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html)

De extensie Adobe Media Analytics (MA) voegt de kern-JavaScript Media SDK (Media 2.x SDK) toe voor audio en video. Deze extensie biedt de functionaliteit voor het toevoegen van de `MediaHeartbeat` tracker-instantie naar een gegevensverzamelingssite of -project.

Voor gegevensverzameling Adobe met de extensie Media Analytics is het volgende vereist:
* Je moet een Adobe Experience Cloud-klant zijn.
* U moet gegevensverzameling of DTM-insluitcode op uw webpagina&#39;s implementeren.
* [Extensie Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html)
* [Experience Cloud ID-extensie](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html)


## Client-zijde

Dit zijn integratie van alleen Media Analytics. U kunt kiezen voor de integratie van de SDK van de videorectie en/of de API voor mediagroep. Dit pad kan worden gebruikt voor elke videospeler, inclusief client- en/of OVP-spelers zoals Brightcove, Ooyala, het Platform enzovoort.

Als Media Analytics uw voorgenomen weg is, zie [Implementatie van SDK voor media](/help/implementation/media-sdk/setup/setup-overview.md) en de [Media Collection API.](/help/media-collection-api/mc-api-overview.md)

>[!IMPORTANT]
>Als klanten Media Analytics willen gebruiken, moeten ze ook Adobe Analytics gebruiken.

## Adobe Primetime

Adobe Primetime is een Adobe Experience Cloud-oplossing waarmee programmeurs en distributeurs van inhoud media op elk aangesloten scherm kunnen monetiseren.

Primetime elimineert de ingewikkeldheid van het bereiken van, het monetiseren van, en het activeren van globaal publiek over apparaten door een modulair platform voor videopublicatie, reclame, verpersoonlijking, en analyses te verstrekken. Bovendien biedt Primetime oplossingen en waarde rond het volgende:

* Ondersteuning voor het nauwkeurig meten van de inhoudstypen Lineair en VOD.
* Ondersteuning voor het meten en afbreken met (of zonder) dynamische invoeging.
* Dankzij het naadloze invoegmodel van TVSDK kunt u analyses maken die het afspelen van de advertentie rechtstreeks meten, waardoor de nauwkeurigheid toeneemt.
* Robuuste set gebeurtenissen en metagegevens om de nauwkeurigheid van alle problemen met QoS-buffering of mobiele connectiviteitsonderbrekingen en interacties van eindgebruikers, zoals zoeken, pauzeren en achtergronden op mobiele apparaten, te garanderen.
* Geïntegreerde ondersteuning voor Nielsen DTVR (lineair) met ID3-metagegevens en DCR met CMS-metagegevens.


TVSDK is al geïntegreerd met de Media Analtyics (Heartbeats) SDK, waardoor de implementatie voor elk ondersteund platform veel eenvoudiger en sneller verloopt. Volg dezelfde richtlijnen en voorwaarden als in [Client-kant](/help/intro-to-ava/implementation-paths/client-side-path.md) samen met de volgende documenten voor uw platform(s): [Primetime gebruikershandleiding.](https://helpx.adobe.com/nl/primetime/user-guide.html)

Neem ook contact op met uw verkoper/accountmanager om te bespreken wat u moet doen om TVSDK te kopen.
