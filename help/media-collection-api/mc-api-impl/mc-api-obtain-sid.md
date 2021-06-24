---
title: Een sessie-ID verkrijgen
description: Leer hoe u een verzoek van Sessies codeert om de sessie-id te verkrijgen van de koptekst Locatie in een reactie.
uuid: fc8712fa-848f-4564-af5d-5dd9d6b088d8
exl-id: 4a1c4ade-4a5e-4af0-8117-19d718dd8bda
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 6%

---

# Sessie-id ophalen{#obtaining-a-session-id}

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
