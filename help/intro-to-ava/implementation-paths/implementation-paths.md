---
title: Welke paden voor het implementeren van streaming media zijn beschikbaar?
description: Meer informatie over implementatiepaden voor Adobe Streaming Media, waaronder Adobe Launch.
exl-id: eee70e62-ba45-440a-8ce1-e151b66d2c1f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 1%

---

# Implementatiepaden {#implementation-paths}

Voor elk implementatiepad moeten klanten contact opnemen met hun verkoper/accountmanager om een nieuwe verkooporder te ondertekenen omdat de Streaming Media Analytics een unieke SKU heeft en wijzigingen doorvoert van een prijsmodel dat is gebaseerd op serveraanroepen naar een model dat is gebaseerd op videostreams.

* **Adobe Starten met de extensie Adobe Media Analytics**

   Adobe Launch is de volgende generatie oplossing voor tagbeheer van Adobe. De lancering verstrekt een eenvoudige manier om alle analytische, marketing, en reclame markeringen noodzakelijk op te stellen en te beheren om relevante klantenervaringen te drijven. Als u uw eigen integraties met Launch wilt maken en onderhouden, gebruikt u extensies. Een extensie is een JavaScript-, HTML- en CSS-pakket dat de functionaliteit van de opstartinterface en de client uitbreidt. Voor meer informatie, zie [de Gids van de Gebruiker van het Experience Platform Launch](https://experienceleague.adobe.com/docs/launch/using/overview.html)

   De extensie Adobe Media Analytics (MA) voegt de kern-JavaScript Media SDK (Media 2.x SDK) toe voor audio en video. Deze extensie biedt de functionaliteit voor het toevoegen van de tracker `MediaHeartbeat` aan een opstartsite of -project.

   Voor het starten van Adobe met de extensie Media Analytics is het volgende vereist:
   * Je moet een Adobe Experience Cloud-klant zijn.
   * U moet de code voor Starten of DTM-insluiten op uw webpagina&#39;s implementeren.
   * [Extensie Analytics](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html)
   * [Experience Cloud ID-extensie](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)


* **Client Side -** Dit zijn integratie van alleen Media Analytics. U kunt kiezen voor de integratie van de SDK van de videorectie en/of de API voor mediagroep. Dit pad kan worden gebruikt voor elke videospeler, inclusief client- en/of OVP-spelers zoals Brightcove, Ooyala, het Platform enzovoort.

   Als Media Analytics uw voorgenomen weg is, zie [de Implementatie van SDK van Media](/help/sdk-implement/setup/setup-overview.md) en [de Inzameling API van Media.](/help/media-collection-api/mc-api-overview.md)

   >[!IMPORTANT]
   >
   >Als klanten Media Analytics willen gebruiken, moeten ze ook Adobe Analytics gebruiken.

* **Adobe Primetime -** Adobe Primetime is een Adobe Experience Cloud-oplossing waarmee programmeurs van inhoud en distributeurs media op elk aangesloten scherm kunnen monetiseren.

   Primetime elimineert de ingewikkeldheid van het bereiken van, het monetiseren van, en het activeren van globaal publiek over apparaten door een modulair platform voor videopublicatie, reclame, verpersoonlijking, en analyses te verstrekken. Bovendien biedt Primetime oplossingen en waarde rond het volgende:

   * Ondersteuning voor het nauwkeurig meten van de inhoudstypen Lineair en VOD.
   * Ondersteuning voor het meten en afbreken met (of zonder) dynamische invoeging.
   * Dankzij het naadloze invoegmodel van TVSDK kunt u analyses maken die het afspelen van de advertentie rechtstreeks meten, waardoor de nauwkeurigheid toeneemt.
   * Robuuste set gebeurtenissen en metagegevens om de nauwkeurigheid van alle problemen met QoS-buffering of mobiele connectiviteitsonderbrekingen en interacties van eindgebruikers, zoals zoeken, pauzeren en achtergronden op mobiele apparaten, te garanderen.

<!--
   * Integrated support for Nielsen DTVR (linear) with ID3 metadata and DCR with CMS metadata.
-->

TVSDK is al geïntegreerd met de Media Analtyics (Heartbeats) SDK, waardoor de implementatie voor elk ondersteund platform veel eenvoudiger en sneller verloopt. <!--Primetime also supports the partnership with Nielsen.--> Als u Primetime wilt gebruiken, volgt u dezelfde richtlijnen en voorwaarden die u in de  [client-](/help/intro-to-ava/implementation-paths/client-side-path.md) side versie hebt gevonden, samen met de volgende documenten voor uw platform(s):  [Primetime gebruikershandleiding.](https://helpx.adobe.com/nl/primetime/user-guide.html)

Neem ook contact op met uw verkoper/accountmanager om te bespreken wat u moet doen om TVSDK te kopen.
