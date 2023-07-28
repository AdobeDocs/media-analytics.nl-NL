---
title: Vereisten voor alleen Adobe Analytics-implementaties
description: Meer informatie over vereisten voor het gebruik van streaming media met alleen Adobe Analytics-implementaties
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: 8a0f2c0b367b48ee5ac94e7fc6bcd0eadafbc5d8
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 1%

---

# Vereisten voor Edge-implementaties

De voorwaarden die in deze sectie worden beschreven, gelden specifiek voor het implementeren van streaming media met Edge-implementaties.

1. **Voltooi de algemene voorwaarden**<br>
Of u nu Streaming Media implementeert voor implementaties die alleen in Adobe Analytics worden uitgevoerd of voor Edge-implementaties, let erop dat u voldoet aan de [algemene voorwaarden](/help/getting-started/prereqs.md).

1. **Bevestig dat u een Adobe-oplossing implementeert die compatibel is met Edge- en Streaming-media**<br>
Wanneer u Streaming Media met Edge implementeert, hebt u ook een werkende Customer Journey Analytics, Adobe Analytics, Adobe Journey Optimizer of een Real-time Customer Data Platform-implementatie nodig. Zie de volgende documentatiebronnen voor meer informatie:
   * [Customer Journey Analytics-hulplijn](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=en)
   * [Adobe Analytics implementeren](https://experienceleague.adobe.com/docs/analytics/implementation/home.html)
   * [Adobe Journey Optimizer-documentatie](https://experienceleague.adobe.com/docs/journey-optimizer.html)
   * [Real-time Customer Data Platform-documentatie](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html)

1. **De URL van de mediatrackingserver ophalen**<br>
Vraag uw Customer Journey Analytics-vertegenwoordiger naar de URL van de mediatrackingserver. <!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **Media Analytics installeren met Edge**<br>
Voer de stappen uit in [Media Analytics installeren met Experience Platform Edge](/help/implementation/edge/implementation-edge.md).