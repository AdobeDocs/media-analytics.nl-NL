---
title: Vereisten voor alleen Adobe Analytics-implementaties
description: Meer informatie over de vereisten voor het gebruik van de invoegtoepassing voor het streamen van media-verzamelingen met alleen Adobe Analytics-implementaties
feature: Media Analytics, System Requirements
role: User, Admin, Data Engineer
exl-id: f94a5339-f777-44ec-ba79-0a1986c52225
source-git-commit: 240fa48bdc738425e04cd29c27625c7dd612ff18
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Vereisten voor alleen Adobe Analytics-implementaties

De eerste vereisten die in deze sectie worden beschreven zijn specifiek voor het implementeren van de invoegtoepassing voor het streamen van media-verzameling met implementaties die alleen gebruikmaken van Adobe-Analytics (wanneer u geen Edge gebruikt).

1. **Voltooi de algemene voorwaarden**<br>
Of u de Invoegtoepassing van de Inzameling van de Media van de Streaming voor Adobe Analytics-Enige implementaties of voor de implementaties van Edge uitvoert, zorg ervoor dat u voldoet aan [algemene voorwaarden](/help/getting-started/prereqs.md).

1. **Bevestig dat u een Adobe Analytics-implementatie hebt**<br>
Wanneer u de invoegtoepassing voor het streamen van media-verzamelingen implementeert met een alleen-analytische implementatie, is ook een Adobe Analytics-basisimplementatie vereist. Zie [Adobe Analytics implementeren](https://experienceleague.adobe.com/docs/analytics/implementation/home.html) voor meer informatie .

1. **De URL van de mediatrackingserver ophalen**<br>
Vraag uw Adobe Analytics-vertegenwoordiger naar de URL van de mediatrackingserver. Dit is het `collection-api-server` URL voor Mobile SDK, JavaScript SDK, en de niet inzameling-api het volgen server voor Roku. Domeinnamen voor API-implementatie zijn: `[your_namespace].hb-api.omtrdc.net`.

1. **Download de huidige Media SDK of implementeer de vereiste extensies**<br>
Afhankelijk van het implementatiepad [de huidige SDK downloaden](/help/getting-started/download-sdks.md) voor web-, mobiele of overdekte platforms. De vereiste extensies moeten worden geïmplementeerd om de invoegpaden voor het inpakken van streaming media in te schakelen.

1. **Adobe Analytics-rapporten inschakelen**<br>
Om rapporten in Analytics toe te laten en de inhoud en de gegevens te bekijken die u verzamelt, moet u rapporten in Analytics toelaten. Zie [Media-rapporten inschakelen](/help/reporting/media-reports-enable.md).
