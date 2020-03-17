---
title: Vereisten
description: null
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Vereisten{#prerequisites}

## Besluiten {#decision}

Voordat u begint met het volgen van de implementatie, moet u enkele beslissingen nemen over de implementatie die het meest zinvol is voor uw situatie:

* **Media Analytics -** De meest recente Media SDK&#39;s gebruiken (de standaard, aanbevolen implementatie) en/of de Media Collection API (RESTful)
* **Mijlpaal -** De oudere implementatie voor het bijhouden van Adobe
* **API&#39;s voor gegevensinvoeging -** Tekstspatiëring implementeren zonder gebruik te maken van Media SDK&#39;s

## Taken {#prereq-tasks}

Voor een implementatie van *Media Analytics* , zijn hier de taken u moet voltooien alvorens u begint:

1. **Schakel Experience Cloud in.**

   U moet de identiteitsservice van het Adobe Experience Platform implementeren.

   De identiteitsdienst laat het gemeenschappelijke identificatiekader voor de Ervaring de Diensten van de Kern van de Wolk, oplossingen, en klantenattributen en publiek in de de kerndienst van Mensen toe. Dit werkt door een unieke, permanente id toe te wijzen aan een sitebezoeker. Wanneer uw organisatie de id-service implementeert, kunt u met deze id dezelfde sitebezoeker en hun gegevens identificeren in verschillende Experience Cloud-oplossingen.

   ![](assets/mc_id_service_graphic.png)

   De dienst van identiteitskaart kan verschillende oplossing-specifieke IDs (bijvoorbeeld, Analytics HULP) ook vervangen. Via de [klant-id&#39;s en de verificatiestatus](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-authenticated-state.html) kunt u met de id-service uw eigen klant-id&#39;s doorgeven aan de Experience Cloud. Houd er echter rekening mee dat de id-service alleen werkt met de oplossingen waarop u zich al hebt geabonneerd. Als u niet bent aangemeld voor toegang tot andere producten, biedt de id-service geen toegang.

   De id-service is een integraal onderdeel van vele functies, verbeteringen en services van de Experience Cloud. Momenteel ondersteunt de id-service [Analytics,](https://www.adobe.com/marketing-cloud/web-analytics.html) [Audience Manager](https://www.adobe.com/marketing-cloud/data-management-platform.html) en [Target.](https://www.adobe.com/marketing-cloud/testing-targeting.html)

   >[!IMPORTANT]
   >
   >Als u wilt deelnemen aan de Adobe Experience Cloud Device Co-op, is de Experience Cloud ID-service vereist.

   Als u de id-service niet hebt geïmplementeerd, is het nu tijd om een migratiestrategie te overwegen. Voor meer informatie over het belang en de rol van de dienst van identiteitskaart, zie [waarom de Dienst van de Identiteit op Uw Radar zou moeten zijn.](https://blogs.adobe.com/digitalmarketing/analytics/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   >[!IMPORTANT]
   >
   >Bij gebrek aan om het even welke gebruiker - identiteitskaart die op media-specifieke vraag aanwezig is, zullen de standaardanalytische Methoden [van identiteitskaart van de](https://docs-author.corp.adobe.com/content/help/en/analytics/implementation/javascript-implementation/unique-visitors/visid-fallback.html) Fallback van de Analyse van toepassing zijn.

   Meer informatie over de Experience Cloud ID vindt u in het overzicht [Experience Cloud ID,](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-overview.html) en de [Adobe Experience Platform Identity Service.](https://marketing.adobe.com/resources/help/en_US/mcvid/)

1. **Schakel Adobe Analytics Reports in.**

   Als u rapporten wilt inschakelen in Analytics en de inhoud en advertentiegegevens wilt zien die u verzamelt, raadpleegt u [Media Reports enablement.](/help/media-reports/media-reports-enable.md)

