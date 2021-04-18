---
title: Sessie-id ophalen
description: Sessie-id ophalen
uuid: fc8712fa-848f-4564-af5d-5dd9d6b088d8
exl-id: 4a1c4ade-4a5e-4af0-8117-19d718dd8bda
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '46'
ht-degree: 0%

---

# Een sessie-id ophalen{#obtaining-a-session-id}

Dit codefragment van de Speler van de Verwijzing toont één manier om een [verzoek van Sessies,](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) samen met het halen van identiteitskaart van de Zitting (en de versie van de Inzameling van Media API) van de kopbal van de Plaats in de reactie te coderen:

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
