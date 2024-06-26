---
title: Vereisten voor alleen Adobe Analytics-implementaties
description: Meer informatie over vereisten voor het gebruik van de invoegtoepassing voor het streamen van media-verzamelingen met alleen Adobe Analytics-implementaties of Edge-implementaties
feature: Media Analytics, System Requirements
role: User, Admin, Data Engineer
exl-id: 7b042e45-e35a-43d6-b59e-282573c6a326
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# Vereisten voor Edge-implementaties

De eerste vereisten die in deze sectie worden beschreven zijn specifiek voor het implementeren van de Adobe Streaming Media Collection Add-on met Edge-implementaties.

1. **Voltooi de algemene voorwaarden**<br>
Of u de Invoegtoepassing van de Inzameling van de Media van de Streaming voor Adobe Analytics-Enige implementaties of voor de implementaties van Edge uitvoert, zorg ervoor dat u voldoet aan [algemene voorwaarden](/help/getting-started/prereqs.md).

1. **Bevestig dat u een oplossing van de Adobe compatibel met Edge Network en de Streaming Invoegtoepassing van de Inzameling van Media uitvoert**<br>
Wanneer u de invoegtoepassing voor het streamen van media-verzamelingen implementeert met Edge, moet u ook over een werkende Customer Journey Analytics, Adobe Analytics, Adobe Journey Optimizer of een Real-time Customer Data Platform-implementatie beschikken. Zie de volgende documentatiebronnen voor meer informatie:
   * [Hulplijn Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=en)
   * [Adobe Analytics implementeren](https://experienceleague.adobe.com/docs/analytics/implementation/home.html)
   * [Adobe Journey Optimizer-documentatie](https://experienceleague.adobe.com/docs/journey-optimizer.html)
   * [Real-time Customer Data Platform-documentatie](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html)

1. **De URL van de mediatrackingserver ophalen**<br>
Vraag uw Customer Journey Analytics-vertegenwoordiger naar de URL van de mediatrackingserver. <!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **Implementeer de invoegtoepassing voor het streamen van media-verzamelingen met de Edge Network**<br>
Voer de stappen uit in [Implementeer de invoegtoepassing voor het streamen van media-verzamelingen met de Edge Network](/help/implementation/edge/implementation-edge.md).
