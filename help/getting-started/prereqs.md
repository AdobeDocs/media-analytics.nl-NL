---
title: Meer informatie over de vereisten voor de invoegtoepassing Adobe Streaming Media Collection
description: Ga aan de slag met de invoegtoepassing voor het streamen van media-verzamelingen. Leer wat u nodig hebt voor de implementatie.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: 240fa48bdc738425e04cd29c27625c7dd612ff18
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# Vereisten {#prerequisites}

Voordat u begint met het implementeren van de invoegtoepassing voor het streamen van media-Adobe, moet u de volgende taken uitvoeren:

1. **Overzicht van de invoegtoepassing voor het streamen van media**<br>
Voordat u begint met het implementeren van de invoegtoepassing voor het streamen van media, bekijkt u de [Overzicht van de invoegtoepassing voor streaming media](/help/media-overview.md) om ervoor te zorgen dat het aan uw behoeften voldoet.

1. **Je prijsmodel bevestigen**<br>
Het huidige prijsmodel voor de Adobe die toe:voegen-on van de Inzameling van Media stroomt is gebaseerd op videostromen. Neem indien nodig contact op met uw verkoper of accountteam van de Adobe, omdat de add-on apart wordt verkocht voor Adobe Analytics en Adobe Experience Platform.

1. **Adobe Analytics-rapporten inschakelen**<br>
Om rapporten in Analytics of Customer Journey Analytics toe te laten en de inhoud en de gegevens te bekijken die u verzamelt, moet u rapporten toelaten. Zie [Media-rapporten inschakelen](/help/reporting/media-reports-enable.md).

1. **Implementeer de Adobe Experience Platform Identity Service in Experience Cloud**

   De **Identiteitsservice** laat het gemeenschappelijke identificatiekader voor de Diensten van de Kern van de Experience Cloud, oplossingen, en klantenattributen en publiek in de de kerndienst van Mensen toe. Dit werkt door een unieke, permanente id toe te wijzen aan een sitebezoeker. Wanneer uw organisatie de id-service implementeert, kunt u met deze id dezelfde sitebezoeker en de bijbehorende gegevens identificeren in verschillende Experience Cloud-oplossingen.

   ![ID Service-afbeelding](assets/mc_id_service_graphic.png)

   De dienst van identiteitskaart kan verschillende oplossing-specifieke IDs (bijvoorbeeld, Analytics HULP) ook vervangen. Via de [Klant-id&#39;s en verificatiestatus](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) functionaliteit, laat de dienst van identiteitskaart u in uw eigen klant IDs tot het Experience Cloud overgaan. Houd er echter rekening mee dat de id-service alleen werkt met de oplossingen waarop u zich al hebt geabonneerd. Als u niet bent aangemeld voor toegang tot andere producten, biedt de id-service geen toegang.

   De dienst van identiteitskaart is een integraal onderdeel van vele eigenschappen van het Experience Cloud, verhogingen, en de diensten. De id-service ondersteunt momenteel [Analytics](https://www.adobe.com/marketing-cloud/web-analytics.html) [Audience Manager,](https://www.adobe.com/marketing-cloud/data-management-platform.html) en [Doel.](https://www.adobe.com/marketing-cloud/testing-targeting.html)

   Als u de id-service niet hebt geïmplementeerd, is het nu tijd om een migratiestrategie te overwegen. Voor meer informatie over het belang en de rol van de dienst van identiteitskaart, zie [Waarom de Identiteitsdienst op Uw Radar zou moeten zijn.](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   Zie voor meer informatie over de Experience Cloud-id [Overzicht van Experience Cloud-id](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html) en [Adobe Experience Platform Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html).

1. **Aanvullende voorwaarden voor uw implementatiemethode weergeven**

   Afhankelijk van hoe u van plan bent om het Streaming Invoegsel van de Inzameling van Media uit te voeren, bekijk de eerste vereisten voor één van beiden van de volgende implementatiemethodes:

   * [Vereisten voor alleen Adobe Analytics-implementaties](/help/implementation/media-sdk/setup/prerequisites-analytics.md)

   * [Vereisten voor Edge-implementaties](/help/implementation/edge/prerequisites-edge.md)

   Gebruik de [Overzicht van implementatie](/help/implementation/overview.md) om te bepalen welke implementatiemethode geschikt is voor u.
