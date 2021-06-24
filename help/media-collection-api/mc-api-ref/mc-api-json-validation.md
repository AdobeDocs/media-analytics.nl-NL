---
title: JSON-validatieschema's voor Streaming Media Analytics
description: Wat zijn de bevestigingsschema's van Media JSON bevestiging en hoe zij worden gebruikt om de correcte parameters van het verzoeklichaam voor elk type van gebeurtenis te bepalen.
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
exl-id: 2931715d-2e7d-4c15-8569-da63b43d6006
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 0%

---

# JSON-validatieschema&#39;s{#json-validation-schemas}

De back-end voor Media Analytics valideert de aanvraagparameters voor elk gebeurtenistype met JSON-validatieschema&#39;s. Deze schema&#39;s zijn beschikbaar aan u, en dienen als huidig gezag op parametertypes die in MA API worden gebruikt.

```
GET
https://{uri}/api/v1/schemas/{event-type}
```

Zie [Gebeurtenisverzoeken valideren](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md) voor meer informatie over het gebruik van de JSON-validatieschema&#39;s.
