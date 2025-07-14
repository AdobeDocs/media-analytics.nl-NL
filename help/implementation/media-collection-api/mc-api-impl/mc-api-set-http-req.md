---
title: Het HTTP-aanvraagtype instellen in de Player
description: De aanvraaginstantie voor alle aanvragen voor de API voor mediagroep moet de JSON-indeling hebben. Leer hoe u het type inhoudsaanvraag instelt in uw speler.
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
exl-id: 9ab3eb07-8f0d-4f9a-8feb-db20c4de3db4
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---

# Het HTTP-aanvraagtype instellen {#setting-the-http-request-type}

De aanvraaginstantie voor alle aanvragen voor de API voor mediagroep moet de JSON-indeling hebben. U moet daarom het type inhoudsaanvraag in de speler instellen. In JavaScript zou u bijvoorbeeld de aanvraagheader `Content-Type` als volgt instellen:

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```
