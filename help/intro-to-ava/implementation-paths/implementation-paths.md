---
title: Implementatiepaden
description: null
uuid: 8400c938-e77e-4c88-b23b-5f5977a5316c
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Implementatiepaden {#implementation-paths}

Media Analytics (Heartbeats) is de gestandaardiseerde videooplossing van Adobe. Het is in de plaats gekomen van het oudere mijlpaalmodel van Adobe.

Voor elk van deze implementatiepaden moeten klanten contact opnemen met hun verkoper/accountmanager om een nieuwe verkooporder te ondertekenen aangezien Media Analytics een unieke SKU heeft en wijzigingen doorvoert van een prijsmodel dat is gebaseerd op serveraanroepen naar een model dat is gebaseerd op videostreams:

* **Client Side -** Dit zijn integratie van alleen Media Analytics. U kunt kiezen voor de integratie van de SDK van de videorectie en/of de API voor mediagroep. Dit pad kan worden gebruikt voor elke videospeler, inclusief client- en/of OVP-spelers zoals Brightcove, Ooyala, het Platform enzovoort.

   Als Media Analytics het bedoelde pad is, raadpleegt u de [Media SDK-implementatie](/help/sdk-implement/setup/setup-overview.md) en de [Media Collection-API.](/help/media-collection-api/mc-api-overview.md)

   >[!IMPORTANT]
   >
   >Als klanten Media Analytics willen gebruiken, moeten ze ook Adobe Analytics gebruiken.

* **Adobe Experience Platform Launch -** Adobe Experience Platform Launch, het vervolgproduct voor Dynamic Tag Management, beschikt over een Media Analytics Launch Extension die het implementeren van video tracking in uw spelers mogelijk maakt.

   Meer informatie over het starten van het Experience Platform vindt u hier: [Adobe Media Analytics for Audio and Video Extension](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)
* **Adobe Primetime -** Adobe Primetime is een Adobe Experience Cloud-oplossing waarmee programmeurs van inhoud en distributeurs media kunnen monetiseren op elk verbonden scherm.

   Primetime elimineert de ingewikkeldheid van het bereiken van, het monetiseren van, en het activeren van globaal publiek over apparaten door een modulair platform voor videopublicatie, reclame, verpersoonlijking, en analyses te verstrekken. Bovendien biedt Primetime oplossingen en waarde rond het volgende:

   * Ondersteuning voor het nauwkeurig meten van de inhoudstypen Lineair en VOD.
   * Ondersteuning voor het meten en afbreken met (of zonder) dynamische invoeging.
   * Dankzij het naadloze invoegmodel van TVSDK kunt u analyses maken die het afspelen van de advertentie rechtstreeks meten, waardoor de nauwkeurigheid toeneemt.
   * Robuuste set gebeurtenissen en metagegevens om de nauwkeurigheid van alle problemen met QoS-buffering of mobiele connectiviteitsonderbrekingen en interacties van eindgebruikers, zoals zoeken, pauzeren en achtergronden op mobiele apparaten, te garanderen.
<!--
   * Integrated support for Nielsen DTVR (linear) with ID3 metadata and DCR with CMS metadata.
-->

TVSDK is al geïntegreerd met de Media Analtyics (Heartbeats) SDK, waardoor de implementatie voor elk ondersteund platform veel eenvoudiger en sneller verloopt. <!--Primetime also supports the partnership with Nielsen.--> Als u Primetime wilt gebruiken, volgt u dezelfde richtlijnen en voorwaarden die u voor uw platform(s) hebt gevonden aan de [clientzijde](/help/intro-to-ava/implementation-paths/client-side-path.md) , samen met de volgende documenten: Gebruikershandleiding voor [primetime.](https://helpx.adobe.com/primetime/user-guide.html)

Neem ook contact op met uw verkoper/accountmanager om te bespreken wat u moet doen om TVSDK te kopen.
