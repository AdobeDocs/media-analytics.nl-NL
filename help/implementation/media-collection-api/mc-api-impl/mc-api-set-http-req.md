---
title: Het HTTP-aanvraagtype instellen in de Player
description: De aanvraaginstantie voor alle aanvragen voor de API voor mediagroep moet de JSON-indeling hebben. Leer hoe u het type inhoudsaanvraag instelt in uw speler.
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
exl-id: 9ab3eb07-8f0d-4f9a-8feb-db20c4de3db4
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 240fa48bdc738425e04cd29c27625c7dd612ff18
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---

# Het HTTP-aanvraagtype instellen {#setting-the-http-request-type}

De aanvraaginstantie voor alle aanvragen voor de API voor mediagroep moet de JSON-indeling hebben. U moet daarom het type inhoudsaanvraag in de speler instellen. In JavaScript kunt u bijvoorbeeld de opdracht `Content-Type` verzoek koptekst als volgt:

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```
