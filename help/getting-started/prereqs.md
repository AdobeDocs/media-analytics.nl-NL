---
title: Meer informatie over vereisten voor streaming media
description: Aan de slag met Adobe Analytics Streaming Media. Leer wat u nodig hebt om Adobe Analytics for Streaming Media te implementeren.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: b022bed6b7be0cc97caaaf6b7bbc42474a57b400
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# Vereisten{#prerequisites}

Voer de volgende taken uit om Adobe Analytics voor Streaming Media te implementeren:

1. **Bevestig uw prijsmodel voor streamingmedia**<br>
Het huidige prijsmodel is gebaseerd op videostromen. Neem indien nodig contact op met uw verkoper of accountmanager om een nieuwe verkooporder te ondertekenen, aangezien de Streaming Media Analytics los van Adobe Analytics wordt verkocht.

1. **Bevestig dat je Adobe Analytics implementeert**<br>
Voor streamingmedia voor Adobe Analytics is ook een Adobe Analytics-basisimplementatie vereist. Zie [Adobe Analytics implementeren](https://experienceleague.adobe.com/docs/analytics/implementation/home.html) voor meer informatie .

1. **De URL van de mediatrackingserver ophalen**<br>
Vraag uw Adobe Analytics-vertegenwoordiger naar de URL van de mediatrackingserver. Dit is het 
`collection-api-server` URL voor de Mobile SDK, de JavaScript SDK, en de niet-inzameling-api volgende server voor Roku. Domeinnamen voor API-implementatie zijn: `[your_namespace].hb-api.omtrdc.net`.

1. **Download de huidige Media SDK of implementeer de vereiste extensies**<br>
Afhankelijk van het implementatiepad [de huidige SDK downloaden](download-sdks.md) voor web-, mobiele of overdekte platforms. De vereiste extensies moeten zijn geïmplementeerd om Adobe Analytics in te schakelen voor het stromen van media-extensiepaden.

1. **Adobe Analytics-rapporten inschakelen**<br>
Om rapporten in Analytics toe te laten en de inhoud en de gegevens te bekijken die u verzamelt, moet u rapporten in Analytics toelaten. Zie [Media-rapporten inschakelen](/help/reporting/media-reports-enable.md).

1. **Experience Cloud inschakelen**<br>


## Implementeer de Adobe Experience Platform Identity Service. {#implement-id}

De **Identiteitsservice** laat het gemeenschappelijke identificatiekader voor de Diensten van de Kern van Experience Cloud, oplossingen, en klantenattributen en publiek in de de kerndienst van Mensen toe. Dit werkt door een unieke, permanente id toe te wijzen aan een sitebezoeker. Wanneer uw organisatie de id-service implementeert, kunt u met deze id dezelfde sitebezoeker en de bijbehorende gegevens identificeren in verschillende Experience Cloud-oplossingen.

![ID Service-afbeelding](assets/mc_id_service_graphic.png)

De dienst van identiteitskaart kan verschillende oplossing-specifieke IDs (bijvoorbeeld, Analytics HULP) ook vervangen. Via de [Klant-id&#39;s en verificatiestatus](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) functionaliteit, laat de dienst van identiteitskaart u in uw eigen klant IDs tot de Experience Cloud overgaan. Houd er echter rekening mee dat de id-service alleen werkt met de oplossingen waarop u zich al hebt geabonneerd. Als u niet bent aangemeld voor toegang tot andere producten, biedt de id-service geen toegang.

De dienst van identiteitskaart is een integraal onderdeel van vele eigenschappen, verhogingen, en de diensten van Experience Cloud. De id-service biedt momenteel ondersteuning voor [Analytics](https://www.adobe.com/marketing-cloud/web-analytics.html) [Audience Manager,](https://www.adobe.com/marketing-cloud/data-management-platform.html) en [Doel.](https://www.adobe.com/marketing-cloud/testing-targeting.html)

Als u de id-service niet hebt geïmplementeerd, is het nu tijd om een migratiestrategie te overwegen. Voor meer informatie over het belang en de rol van de dienst van identiteitskaart, zie [Waarom de Identiteitsdienst op Uw Radar zou moeten zijn.](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

Voor meer informatie over de Experience Cloud-id raadpleegt u [Overzicht van Experience Cloud-id](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html) en [Adobe Experience Platform Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html).