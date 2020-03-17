---
title: Het HTTP-aanvraagtype in de speler instellen
description: null
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Het HTTP-aanvraagtype instellen {#setting-the-http-request-type}

De aanvraaginstantie voor alle aanvragen voor de API voor mediagroep moet de JSON-indeling hebben. U moet daarom het type inhoudsaanvraag in de speler instellen. In JavaScript stelt u bijvoorbeeld de `Content-Type` aanvraagkoptekst als volgt in:

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```

