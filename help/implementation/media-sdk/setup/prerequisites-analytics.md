---
title: Vereisten voor alleen Adobe Analytics-implementaties
description: Meer informatie over de vereisten voor het gebruik van de verzameling streamingmedia met alleen Adobe Analytics-implementaties
feature: Media Analytics, System Requirements
role: User, Admin, Data Engineer
exl-id: f94a5339-f777-44ec-ba79-0a1986c52225
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# Vereisten voor alleen Adobe Analytics-implementaties

De voorwaarden die in deze sectie worden beschreven zijn specifiek voor het implementeren van de streamingmedia-verzameling met implementaties die alleen gebruikmaken van Adobe-Analytics (wanneer u geen Edge gebruikt).

1. **voltooi de algemene eerste vereisten**<br>
Of u de Streaming Inzameling van Media voor Adobe Analytics-slechts implementaties of voor de implementaties van Edge uitvoert, zorg ervoor dat u aan de [ algemene eerste vereisten ](/help/getting-started/prereqs.md) voldoet.

1. **Bevestig dat u een implementatie van Adobe Analytics**<br> hebt
Wanneer u de verzameling streamingmedia implementeert met een alleen-analytische implementatie, is ook een Adobe Analytics-basisimplementatie vereist. Zie [ Adobe Analytics ](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=nl-NL) voor meer informatie uitvoeren.

1. **verkrijg media het volgen server URL**<br>
Vraag uw Adobe Analytics-vertegenwoordiger naar de URL van de mediatrackingserver. Dit is de `collection-api-server` URL voor Mobile SDK, de JavaScript SDK, en de niet-inzameling-api die server voor Roku volgen. Domeinnamen voor API-implementatie zijn: `[your_namespace].hb-api.omtrdc.net` .

1. **Download huidige Media SDK of voer de vereiste Uitbreidingen uit**<br>
Afhankelijk van de implementatieweg, [ download huidige SDK ](/help/getting-started/download-sdks.md) voor Web, mobiel, of over-de-hoogste platforms. De vereiste extensies moeten worden geïmplementeerd om de paden voor het streamen van media-verzamelingspaden in te schakelen.

1. **laat de Rapporten van Adobe Analytics**<br> toe
Om rapporten in Analytics toe te laten en de inhoud en de gegevens te bekijken die u verzamelt, moet u rapporten in Analytics toelaten. Zie [ Media meldt enablement ](/help/reporting/media-reports-enable.md).
