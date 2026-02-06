---
title: Meer informatie over vereisten voor Adobe-streaming-mediaservices
description: Ga aan de slag met de streaming media services. Leer wat u nodig hebt voor de implementatie.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: "Streaming Media, Workspace Basics"
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# Vereisten {#prerequisites}

Voer de volgende taken uit voordat u de Adobe-streaming-mediaservices gaat implementeren:

1. **herzie het Adobe stromen media de diensten overzicht**<br>
Alvorens u begint het stromen de media diensten uit te voeren, herzie [&#x200B; het stromen van Adobe media de diensten overzicht &#x200B;](/help/media-overview.md) om ervoor te zorgen het aan uw behoeften voldoet.

1. **bevestigt uw het tarief model**<br>
Het huidige prijsmodel voor de invoegtoepassing Customer Journey Analytics Streaming Media Collection en de Adobe Analytics voor Streaming Media Add-on is gebaseerd op videostreams. Neem indien nodig contact op met uw verkoper of Adobe-accountteam, omdat de add-on apart wordt verkocht voor Adobe Analytics en Adobe Experience Platform.

1. **laat de Rapporten van Adobe Analytics**<br> toe
Als u rapporten wilt inschakelen in Analytics of Customer Journey Analytics en om de inhoud en de gegevens te bekijken die u verzamelt, moet u rapporten inschakelen. Zie [&#x200B; Media meldt enablement &#x200B;](/help/reporting/media-reports-enable.md).

1. **voer de Dienst van de Identiteit van Adobe Experience Platform in Experience Cloud uit**

   De **Dienst van de Identiteit** laat het gemeenschappelijke identificatiekader voor de Diensten van de Kern van Experience Cloud, oplossingen, en klantenattributen en publiek in de de kerndienst van Mensen toe. Dit werkt door een unieke, permanente id toe te wijzen aan een sitebezoeker. Wanneer uw organisatie de id-service implementeert, kunt u met deze id dezelfde sitebezoeker en de bijbehorende gegevens identificeren in verschillende Experience Cloud-oplossingen.

   ![&#x200B; grafisch van de Dienst van identiteitskaart &#x200B;](assets/mc_id_service_graphic.png)

   De dienst van identiteitskaart kan verschillende oplossing-specifieke IDs (bijvoorbeeld, Analytics HULP) ook vervangen. Door [&#x200B; identiteitskaarts van de Klant en de Status van de Authentificatie &#x200B;](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) functionaliteit, laat de dienst van identiteitskaart u in uw eigen klant IDs tot Experience Cloud overgaan. Houd er echter rekening mee dat de id-service alleen werkt met de oplossingen waarop u zich al hebt geabonneerd. Als u niet bent aangemeld voor toegang tot andere producten, biedt de id-service geen toegang.

   De dienst van identiteitskaart is een integraal onderdeel van vele eigenschappen, verhogingen, en de diensten van Experience Cloud. Momenteel, steunt de dienst van identiteitskaart [&#x200B; Analytics, &#x200B;](https://www.adobe.com/marketing-cloud/web-analytics.html) [&#x200B; Audience Manager, &#x200B;](https://www.adobe.com/marketing-cloud/data-management-platform.html) en [&#x200B; Doel.](https://www.adobe.com/marketing-cloud/testing-targeting.html)

   Als u de id-service niet hebt geïmplementeerd, is het nu tijd om een migratiestrategie te overwegen. Voor meer informatie over het belang en de rol van de dienst van identiteitskaart, zie [&#x200B; waarom de Dienst van de Identiteit op Uw Radar zou moeten zijn.](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   Voor extra informatie over identiteitskaart van Experience Cloud, zie [&#x200B; het Overzicht van identiteitskaart van Experience Cloud, &#x200B;](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html) en [&#x200B; de Dienst van de Identiteit van Adobe Experience Platform &#x200B;](https://experienceleague.adobe.com/docs/id-service/using/home.html).

1. **de extra eerste vereisten van de Mening voor uw implementatiemethode**

   Afhankelijk van hoe u de het stromen media diensten wilt uitvoeren, bekijk de eerste vereisten voor één van beiden van de volgende implementatiemethodes:

   * [Vereisten voor alleen Adobe Analytics-implementaties](/help/implementation/media-sdk/setup/prerequisites-analytics.md)

   * [Vereisten voor Edge-implementaties](/help/implementation/edge/prerequisites-edge.md)

   Gebruik het [&#x200B; overzicht van de Implementatie &#x200B;](/help/implementation/overview.md) om te bepalen welke implementatiemethode voor u juist is.
