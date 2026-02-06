---
title: Zitting-id verkrijgen
description: Leer hoe u een verzoek van Sessies codeert om de sessie-id te verkrijgen van de koptekst Locatie in een reactie.
uuid: fc8712fa-848f-4564-af5d-5dd9d6b088d8
exl-id: 4a1c4ade-4a5e-4af0-8117-19d718dd8bda
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '61'
ht-degree: 0%

---

# Sessie-id ophalen{#obtaining-a-session-id}

Dit codefragment van de Speler van de Verwijzing toont één manier om a [&#x200B; verzoek van Sessies &#x200B;](../mc-api-ref/mc-api-sessions-req.md) te coderen, samen met het halen van identiteitskaart van de Zitting (en de Verzameling API van Media versie) van de kopbal van de Plaats in de reactie:

```js
var  
sessionData = { 
        ... 
        "media.contentType": "VOD", 
        "media.channel": "sample-channel", 
        ... 
    } 
}; 
...

const SESSION_ID_EXTRACTOR = /^\/api\/(.*)\/sessions\/(.*)/; 
    ...
    apiClient.request({ 
        "baseUrl": config.apiBaseUrl,   // The endpoint 
        "path": config.apiSessionsPath, // api/v1/sessions/ 
        "method": "POST",               // (Always POST) 
        "data": sessionData             // Mandatory params 
     }).then((response) => { 
        // Extract Session ID (and API version) 
        const [, apiVersion, sessionId] =  response.headers.Location.match(SESSION_ID_EXTRACTOR);  
        this.sessionId = sessionId;     // Session ID obtained 
        this._sessionStarted = true;    // Session started. 
    ...
```
