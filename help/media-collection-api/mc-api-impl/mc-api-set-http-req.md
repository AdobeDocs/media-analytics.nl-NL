---
title: Het HTTP-aanvraagtype in de speler instellen
description: Het HTTP-aanvraagtype in de speler instellen
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
exl-id: 9ab3eb07-8f0d-4f9a-8feb-db20c4de3db4
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '58'
ht-degree: 0%

---

# Het HTTP-aanvraagtype {#setting-the-http-request-type} instellen

De aanvraaginstantie voor alle aanvragen voor de API voor mediagroep moet de JSON-indeling hebben. U moet daarom het type inhoudsaanvraag in de speler instellen. In JavaScript zou u bijvoorbeeld de aanvraagheader `Content-Type` als volgt instellen:

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```
