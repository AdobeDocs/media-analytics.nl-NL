---
title: Zitting-id verkrijgen
description: Leer hoe u een verzoek van Sessies codeert om de sessie-id te verkrijgen van de koptekst Locatie in een reactie.
uuid: fc8712fa-848f-4564-af5d-5dd9d6b088d8
exl-id: 4a1c4ade-4a5e-4af0-8117-19d718dd8bda
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '61'
ht-degree: 0%

---

# Sessie-id ophalen{#obtaining-a-session-id}

Dit codefragment van de Speler van de Verwijzing toont één manier om a [ verzoek van Sessies ](../mc-api-ref/mc-api-sessions-req.md) te coderen, samen met het halen van identiteitskaart van de Zitting (en de Verzameling API van Media versie) van de kopbal van de Plaats in de reactie:

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
