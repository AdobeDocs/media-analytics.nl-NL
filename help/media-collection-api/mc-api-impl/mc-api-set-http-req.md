---
title: Het HTTP-aanvraagtype instellen in de Player
description: De aanvraaginstantie voor alle aanvragen voor de API voor streaming media Collection moet de JSON-indeling hebben. Leer hoe u het type inhoudsaanvraag instelt in uw speler.
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
exl-id: 9ab3eb07-8f0d-4f9a-8feb-db20c4de3db4
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: d89b2af2e2ae5a170ce98f62656cdeed6fe31f19
workflow-type: tm+mt
source-wordcount: '76'
ht-degree: 10%

---

# Het HTTP-aanvraagtype instellen {#setting-the-http-request-type}

De aanvraaginstantie voor alle aanvragen voor de API voor mediagroep moet de JSON-indeling hebben. U moet daarom het type inhoudsaanvraag in de speler instellen. In JavaScript stelt u bijvoorbeeld de instelling `Content-Type` verzoek koptekst als volgt:

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```
