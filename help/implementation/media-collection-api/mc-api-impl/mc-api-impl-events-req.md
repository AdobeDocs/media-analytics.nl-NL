---
title: Een Events-aanvraag implementeren
description: Leer hoe te om het de verzoekeindpunt van Gebeurtenissen voor alle volgende volgende volgende volgende volgende volgende volgende vraag te gebruiken nadat u een identiteitskaart van de Zitting verkrijgt
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
exl-id: af9a3470-85c7-498e-9bf4-6df3c6aafad9
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---

# Een verzoek om gebeurtenissen uitvoeren{#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

Gebruik het [ verzoek van Gebeurtenissen ](../mc-api-ref/mc-api-events-req.md) voor alle verdere volgende volgende het volgen vraag nadat u een identiteitskaart van de Zitting gebruikend het [ verzoek van Zitting verkrijgt.](../mc-api-ref/mc-api-sessions-req.md) Geef de locatie en het tijdstempel van de afspeelkop, het gebeurtenistype en eventuele optionele parameters op die u wilt opnemen in de JSON-hoofdtekst van de aanvraag.

Het JSON- verzoeklichaam voor het [ verzoek van Gebeurtenissen ](../mc-api-ref/mc-api-events-req.md) heeft de zelfde structuur zoals dat van het verzoek van Sessies, echter controleer de [ JSON bevestigingsschema&#39;s ](../mc-api-ref/mc-api-json-validation.md) voor parametervereisten en types.
