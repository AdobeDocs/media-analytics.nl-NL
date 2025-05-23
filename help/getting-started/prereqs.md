---
title: Meer informatie over de vereisten voor de Adobe Streaming Media Collection
description: Aan de slag met de streamingmedia-collectie. Leer wat u nodig hebt voor de implementatie.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 0%

---

# Vereisten {#prerequisites}

Voordat u de Adobe Streaming Media Collection gaat implementeren, moet u de volgende taken uitvoeren:

1. **herzie het Streaming overzicht van de Inzameling van Media**<br>
Alvorens u begint de Streaming Inzameling van Media uit te voeren, herzie het [ Streaming overzicht van de Inzameling van Media ](/help/media-overview.md) om ervoor te zorgen het aan uw behoeften voldoet.

1. **bevestigt uw het tarief model**<br>
Het huidige prijsmodel voor de Adobe die toe:voegen-on van de Inzameling van Media stroomt is gebaseerd op videostromen. Neem indien nodig contact op met uw verkoper of accountteam van de Adobe, omdat de add-on apart wordt verkocht voor Adobe Analytics en Adobe Experience Platform.

1. **laat de Rapporten van Adobe Analytics**<br> toe
Om rapporten in Analytics of Customer Journey Analytics toe te laten en de inhoud en de gegevens te bekijken die u verzamelt, moet u rapporten toelaten. Zie [ Media meldt enablement ](/help/reporting/media-reports-enable.md).

1. **voer de Dienst van de Identiteit van Adobe Experience Platform in Experience Cloud uit**

   De **Dienst van de Identiteit** laat het gemeenschappelijke identificatiekader voor de Diensten van de Kern van de Experience Cloud, oplossingen, en klantenattributen en publiek in de de kerndienst van Mensen toe. Dit werkt door een unieke, permanente id toe te wijzen aan een sitebezoeker. Wanneer uw organisatie de id-service implementeert, kunt u met deze id dezelfde sitebezoeker en de bijbehorende gegevens identificeren in verschillende Experience Cloud-oplossingen.

   ![ grafisch van de Dienst van identiteitskaart ](assets/mc_id_service_graphic.png)

   De dienst van identiteitskaart kan verschillende oplossing-specifieke IDs (bijvoorbeeld, Analytics HULP) ook vervangen. Door [ identiteitskaarts van de Klant en de Status van de Authentificatie ](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=nl-NL) functionaliteit, laat de dienst van identiteitskaart u in uw eigen klant IDs tot het Experience Cloud overgaan. Houd er echter rekening mee dat de id-service alleen werkt met de oplossingen waarop u zich al hebt geabonneerd. Als u niet bent aangemeld voor toegang tot andere producten, biedt de id-service geen toegang.

   De dienst van identiteitskaart is een integraal onderdeel van vele eigenschappen van het Experience Cloud, verhogingen, en de diensten. Momenteel, steunt de dienst van identiteitskaart [ Analytics, ](https://www.adobe.com/marketing-cloud/web-analytics.html) [ Audience Manager, ](https://www.adobe.com/marketing-cloud/data-management-platform.html) en [ Doel.](https://www.adobe.com/marketing-cloud/testing-targeting.html)

   Als u de id-service niet hebt geïmplementeerd, is het nu tijd om een migratiestrategie te overwegen. Voor meer informatie over het belang en de rol van de dienst van identiteitskaart, zie [ waarom de Dienst van de Identiteit op Uw Radar zou moeten zijn.](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   Voor extra informatie over Experience Cloud identiteitskaart, zie [ het Overzicht van identiteitskaart van het Experience Cloud, ](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=nl-NL) en [ de Dienst van de Identiteit van Adobe Experience Platform ](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=nl-NL).

1. **de extra eerste vereisten van de Mening voor uw implementatiemethode**

   Afhankelijk van hoe u van plan bent om de het stromen Inzameling van Media uit te voeren, bekijk de eerste vereisten voor één van beiden van de volgende implementatiemethodes:

   * [Vereisten voor alleen Adobe Analytics-implementaties](/help/implementation/media-sdk/setup/prerequisites-analytics.md)

   * [Vereisten voor Edge-implementaties](/help/implementation/edge/prerequisites-edge.md)

   Gebruik het [ overzicht van de Implementatie ](/help/implementation/overview.md) om te bepalen welke implementatiemethode voor u juist is.
