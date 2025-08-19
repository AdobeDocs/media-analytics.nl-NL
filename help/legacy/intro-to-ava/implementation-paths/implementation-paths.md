---
title: Welke paden voor het implementeren van streaming media zijn beschikbaar?
description: Leer meer over Adobe Streaming Media-implementatiepaden, waaronder Adobe Experience Platform Data Collection.
exl-id: eee70e62-ba45-440a-8ce1-e151b66d2c1f
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 4%

---

# Implementatiepaden {#implementation-paths}

**DEZE INHOUD WERD VERPLAATST NAAR HET HUIDIGE DOSSIER VAN DE UITVOERINGSPADEN**

Voor elk implementatiepad moeten klanten contact opnemen met hun verkoper of Adobe-accountteam om een nieuwe verkooporder te ondertekenen, aangezien Customer Journey Analytics Streaming Media Collection en Adobe Analytics voor Streaming Media een unieke SKU hebben en wijzigingen aanbrengen van een prijsmodel op basis van serveraanroepen naar een model op basis van videostreams.

## Adobe Experience Platform Data Collection met de extensie Adobe Media Analytics

>[!NOTE]
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Als gevolg hiervan zijn er verschillende terminologiewijzigingen in de productdocumentatie doorgevoerd. Raadpleeg het volgende [ document ](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=nl-NL) voor een geconsolideerde referentie van de terminologiewijzigingen.


Tags in Adobe Experience Platform zijn de volgende generatie mogelijkheden voor tagbeheer van Adobe. Met labels kunnen klanten eenvoudig alle analytische, marketing- en advertentietags implementeren en beheren die nodig zijn om relevante klantervaringen te stimuleren. Tags worden aan Adobe Experience Cloud-klanten aangeboden als een inbegrepen functie voor het toevoegen van waarden.

Tags stellen iedereen in staat zijn eigen integraties te maken en te onderhouden, zogenaamde extensies. Deze extensies zijn beschikbaar voor Adobe Experience Cloud-klanten in een app-store-ervaring, zodat ze hun tags snel kunnen installeren, configureren en implementeren.

Een extensie is een pakket code (JavaScript, HTML en CSS) dat de functionaliteit voor tags uitbreidt. Ontwikkel, beheer, en werk uw integratie bij gebruikend een vrijwel zelfbedienings interface. U kunt aan uitbreidingen denken aangezien apps u gebruikt om uw taken te bereiken.Voor meer informatie, zie het *overzicht van Markeringen* artikel in de [ Documentatie van Adobe Experience Platform ](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=nl-NL)

De extensie Adobe Media Analytics (MA) voegt de core JavaScript Media SDK (Media 2.x SDK) toe voor audio en video. Deze extensie biedt de functionaliteit voor het toevoegen van de `MediaHeartbeat` tracker-instantie aan een gegevensverzamelingssite of -project.

Voor Adobe Data Collection met de extensie Media Analytics is het volgende vereist:
* Je moet een Adobe Experience Cloud-klant zijn.
* U moet gegevensverzameling of DTM-insluitcode op uw webpagina&#39;s implementeren.
* [ Uitbreiding Analytics ](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=nl-NL)
* [ de Uitbreiding van identiteitskaart van Experience Cloud ](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=nl-NL)


## Client-zijde

Dit zijn integratie van alleen Media Analytics. U kunt kiezen voor de integratie van de videokaart-SDK en/of de mediagroep-API. Dit pad kan worden gebruikt voor elke videospeler, inclusief client- en/of OVP-spelers zoals Brightcove, Ooyala, het Platform enzovoort.

Als Analytics van Media uw voorgenomen weg is, zie de [ Implementatie van Media SDK ](/help/legacy/setup/legacy-setup-overview.md) en [ de Inzameling API van Media.](/help/implementation/media-collection-api/mc-api-overview.md)

>[!IMPORTANT]
>Als klanten Media Analytics willen gebruiken, moeten ze ook Adobe Analytics gebruiken.

## Adobe Primetime

Adobe Primetime is een Adobe Experience Cloud-oplossing waarmee programmeurs van inhoud en distributeurs media op elk aangesloten scherm kunnen monetiseren.

Primetime elimineert de ingewikkeldheid van het bereiken van, het monetiseren van, en het activeren van globaal publiek over apparaten door een modulair platform voor videopublicatie, reclame, verpersoonlijking, en analyses te verstrekken. Bovendien biedt Primetime oplossingen en waarde rond het volgende:

* Ondersteuning voor het nauwkeurig meten van de inhoudstypen Lineair en VOD.
* Ondersteuning voor het meten en afbreken met (of zonder) dynamische invoeging.
* Dankzij het naadloze invoegmodel van TVSDK kunt u analyses maken die het afspelen van de advertentie rechtstreeks meten, waardoor de nauwkeurigheid toeneemt.
* Robuuste set gebeurtenissen en metagegevens om de nauwkeurigheid van alle problemen met QoS-buffering of mobiele connectiviteitsonderbrekingen en interacties van eindgebruikers, zoals zoeken, pauzeren en achtergronden op mobiele apparaten, te garanderen.
* Geïntegreerde ondersteuning voor Nielsen DTVR (lineair) met ID3-metagegevens en DCR met CMS-metagegevens.


TVSDK is al geïntegreerd met de Media Analtyics (Heartbeats) SDK, waardoor de implementatie voor elk ondersteund platform veel eenvoudiger en sneller verloopt. Aan hefboomwerking Primetime, volg de zelfde richtlijnen en de eerste vereisten die in [ worden gevonden client-kant ](/help/legacy/intro-to-ava/implementation-paths/client-side-path.md) samen met de volgende documenten voor uw platform(s): [ Gids van de Gebruiker Primetime.](https://helpx.adobe.com/nl/primetime/user-guide.html)

Neem ook contact op met uw verkoper/accountmanager om te bespreken wat u moet doen om TVSDK aan te schaffen.
