---
title: JSON-validatieschema's voor Streaming Media Collection
description: Wat zijn de bevestigingsschema's van Media JSON bevestiging en hoe zij worden gebruikt om de correcte parameters van het verzoeklichaam voor elk type van gebeurtenis te bepalen.
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
exl-id: 2931715d-2e7d-4c15-8569-da63b43d6006
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 240fa48bdc738425e04cd29c27625c7dd612ff18
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 0%

---

# JSON-validatieschema&#39;s{#json-validation-schemas}

De het stromen Invoegsel-op achterste kant van de Inzameling van Media bevestigt de verzoekparameters voor elk gebeurtenistype gebruikend JSON bevestigingsschema&#39;s. Deze schema&#39;s zijn beschikbaar aan u, en dienen als huidig gezag op parametertypes die in MA API worden gebruikt.

`GET https://{uri}/api/v1/schemas/{event-type}`

Voor meer informatie over het gebruik van de JSON-validatieschema&#39;s raadpleegt u [Gebeurtenisaanvragen valideren.](../mc-api-impl/mc-api-validate-reqs.md)
