---
title: Meer informatie over vereisten voor streamingmedia
description: Aan de slag met Adobe Analytics Streaming Media. Leer wat u nodig hebt om Adobe Analytics for Streaming Media te implementeren.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: '"Media Analytics, System Requirements"'
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# Vereisten{#prerequisites}

## Besluiten {#decision}

Voordat u begint met het volgen van de implementatie, moet u enkele beslissingen nemen over de implementatie die het meest zinvol is voor uw situatie:

* **Media Analytics -** De nieuwste media SDK&#39;s (de standaard, aanbevolen implementatie) en/of de Media Collection API (RESTful) gebruiken
* **Mijlpaal -** De oudere implementatie voor het bijhouden van Adobe
* **API&#39;s voor het invoegen van gegevens -** Tekstspatiëring implementeren zonder gebruik te maken van Media SDK&#39;s

## Taken {#prereq-tasks}

Voor een *Media Analytics* implementatie, zijn hier de taken u moet voltooien alvorens u begint:

1. **Experience Cloud inschakelen.**

   U moet de Adobe Experience Platform Identity Service implementeren.

   De Dienst van de Identiteit laat het gemeenschappelijke identificatiekader voor de Diensten van de Kern van de Experience Cloud, oplossingen, en klantenattributen en publiek in de de kerndienst van Mensen toe. Dit werkt door een unieke, permanente id toe te wijzen aan een sitebezoeker. Wanneer uw organisatie de id-service implementeert, kunt u met deze id dezelfde sitebezoeker en de bijbehorende gegevens identificeren in verschillende Experience Cloud-oplossingen.

   ![](assets/mc_id_service_graphic.png)

   De dienst van identiteitskaart kan verschillende oplossing-specifieke IDs (bijvoorbeeld, Analytics HULP) ook vervangen. Via de [Klanten-id&#39;s en verificatiestatus](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html)-functionaliteit kunt u met de id-service uw eigen klant-id&#39;s doorgeven aan de Experience Cloud. Houd er echter rekening mee dat de id-service alleen werkt met de oplossingen waarop u zich al hebt geabonneerd. Als u niet bent aangemeld voor toegang tot andere producten, biedt de id-service geen toegang.

   De id-service is een integraal onderdeel van vele huidige en toekomstige functies, verbeteringen en services voor Experience Cloud. De id-service biedt momenteel ondersteuning voor [Analytics,](https://www.adobe.com/marketing-cloud/web-analytics.html) [Audience Manager,](https://www.adobe.com/marketing-cloud/data-management-platform.html) en [Target.](https://www.adobe.com/marketing-cloud/testing-targeting.html)

   >[!IMPORTANT]
   >
   >Als u wilt deelnemen aan de Adobe Experience Cloud Device Co-op, is de Experience Cloud-id-service vereist.

   Als u de id-service niet hebt geïmplementeerd, is het nu tijd om een migratiestrategie te overwegen. Voor meer informatie over het belang en de rol van de dienst van identiteitskaart, zie [Waarom de Dienst van de Identiteit op Uw Radar zou moeten zijn.](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   Voor extra informatie over Experience Cloud ID, zie [Overzicht van identiteitskaart van de Experience Cloud,](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html) en [de Dienst van de Identiteit van Adobe Experience Platform](https://experienceleague.adobe.com/docs/id-service/using/home.html).

1. **Adobe Analytics-rapporten inschakelen.**

   Als u rapporten wilt inschakelen in Analytics en de inhoud en advertentiegegevens wilt zien die u verzamelt, raadpleegt u [Media-rapporten inschakelen.](/help/media-reports/media-reports-enable.md)
