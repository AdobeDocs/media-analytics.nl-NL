---
title: Vereisten voor alleen Adobe Analytics-implementaties
description: Meer informatie over vereisten voor het gebruik van de verzameling streamingmedia met alleen Adobe Analytics-implementaties of Edge-implementaties
feature: Media Analytics, System Requirements
role: User, Admin, Data Engineer
exl-id: 7b042e45-e35a-43d6-b59e-282573c6a326
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---

# Vereisten voor Edge-implementaties

De voorwaarden die in deze sectie worden beschreven, gelden specifiek voor het implementeren van de Adobe Streaming Media Collection met Edge-implementaties.

1. **voltooi de algemene eerste vereisten**<br>
Of u de Streaming Inzameling van Media voor Adobe Analytics-slechts implementaties of voor de implementaties van Edge uitvoert, zorg ervoor dat u aan de [ algemene eerste vereisten ](/help/getting-started/prereqs.md) voldoet.

1. **bevestigt dat u een oplossing van de Adobe compatibel met Edge Network en de Streaming Inzameling van Media**<br> uitvoert
Wanneer u de verzameling streamingmedia met Edge implementeert, moet u ook over een werkende Customer Journey Analytics, Adobe Analytics, Adobe Journey Optimizer of een Real-time Customer Data Platform-implementatie beschikken. Zie de volgende documentatiebronnen voor meer informatie:
   * [ gids van de Customer Journey Analytics ](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=nl-NL)
   * [ voer Adobe Analytics ](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=nl-NL) uit
   * [ documentatie van Adobe Journey Optimizer ](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=nl-NL)
   * [ documentatie van Real-time Customer Data Platform ](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html?lang=nl-NL)

1. **verkrijg media het volgen server URL**<br>
Vraag uw Customer Journey Analytics-vertegenwoordiger naar de URL van de mediatrackingserver. <!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **voer de Streaming Inzameling van Media uit gebruikend de Edge Network**<br>
Volg de stappen in [ uitvoeren de Streaming Inzameling van Media gebruikend de Edge Network ](/help/implementation/edge/implementation-edge.md).
