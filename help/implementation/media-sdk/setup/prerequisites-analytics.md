---
title: Vereisten voor alleen Adobe Analytics-implementaties
description: Meer informatie over vereisten voor het gebruik van streaming media met alleen Adobe Analytics-implementaties
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: c4d058ee82f4995f42bfe21c0442004f1f7ea4af
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---

# Vereisten voor alleen Adobe Analytics-implementaties

De voorwaarden die in deze sectie worden beschreven, gelden specifiek voor het implementeren van streamingmedia met alleen Adobe-Analytics-implementaties (wanneer u Edge niet gebruikt).

1. **Voltooi de algemene voorwaarden**<br>
Of u nu Streaming Media implementeert voor implementaties die alleen in Adobe Analytics worden uitgevoerd of voor Edge-implementaties, let erop dat u voldoet aan de [algemene voorwaarden](/help/getting-started/prereqs.md).

1. **Bevestig dat u een Adobe Analytics-implementatie hebt**<br>
Bij de implementatie van Streaming Media met een implementatie die alleen voor Analytics geldt, is ook een Adobe Analytics-basisimplementatie vereist. Zie [Adobe Analytics implementeren](https://experienceleague.adobe.com/docs/analytics/implementation/home.html) voor meer informatie .

1. **De URL van de mediatrackingserver ophalen**<br>
Vraag uw Adobe Analytics-vertegenwoordiger naar de URL van de mediatrackingserver. Dit is het `collection-api-server` URL voor de Mobile SDK, de JavaScript SDK, en de niet-inzameling-api volgende server voor Roku. Domeinnamen voor API-implementatie zijn: `[your_namespace].hb-api.omtrdc.net`.

1. **Download de huidige Media SDK of implementeer de vereiste extensies**<br>
Afhankelijk van het implementatiepad [de huidige SDK downloaden](/help/getting-started/download-sdks.md) voor web-, mobiele of overdekte platforms. De vereiste extensies moeten zijn geïmplementeerd om Adobe Analytics in te schakelen voor het stromen van media-extensiepaden.

1. **Adobe Analytics-rapporten inschakelen**<br>
Om rapporten in Analytics toe te laten en de inhoud en de gegevens te bekijken die u verzamelt, moet u rapporten in Analytics toelaten. Zie [Media-rapporten inschakelen](/help/reporting/media-reports-enable.md).
