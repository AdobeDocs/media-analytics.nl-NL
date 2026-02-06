---
title: Een Events-aanvraag implementeren
description: Leer hoe te om het de verzoekeindpunt van Gebeurtenissen voor alle volgende volgende volgende volgende volgende volgende volgende vraag te gebruiken nadat u een identiteitskaart van de Zitting verkrijgt
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
exl-id: af9a3470-85c7-498e-9bf4-6df3c6aafad9
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---

# Een verzoek om gebeurtenissen uitvoeren{#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

Gebruik het [&#x200B; verzoek van Gebeurtenissen &#x200B;](../mc-api-ref/mc-api-events-req.md) voor alle verdere volgende volgende het volgen vraag nadat u een identiteitskaart van de Zitting gebruikend het [&#x200B; verzoek van Zitting verkrijgt.](../mc-api-ref/mc-api-sessions-req.md) Geef de locatie en het tijdstempel van de afspeelkop, het gebeurtenistype en eventuele optionele parameters op die u wilt opnemen in de JSON-hoofdtekst van de aanvraag.

Het JSON- verzoeklichaam voor het [&#x200B; verzoek van Gebeurtenissen &#x200B;](../mc-api-ref/mc-api-events-req.md) heeft de zelfde structuur zoals dat van het verzoek van Sessies, echter controleer de [&#x200B; JSON bevestigingsschema&#39;s &#x200B;](../mc-api-ref/mc-api-json-validation.md) voor parametervereisten en types.
