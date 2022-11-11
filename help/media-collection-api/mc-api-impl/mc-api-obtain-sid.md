---
title: Een sessie-ID verkrijgen
description: Leer hoe u een verzoek van Sessies codeert om de sessie-id te verkrijgen van de koptekst Locatie in een reactie.
uuid: fc8712fa-848f-4564-af5d-5dd9d6b088d8
exl-id: 4a1c4ade-4a5e-4af0-8117-19d718dd8bda
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: d89b2af2e2ae5a170ce98f62656cdeed6fe31f19
workflow-type: tm+mt
source-wordcount: '61'
ht-degree: 6%

---

# Sessie-id ophalen{#obtaining-a-session-id}

Dit codefragment van de Speler van de Verwijzing toont één manier om te coderen [verzoek om sessies,](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) samen met het uitpakken van de sessie-id (en de media Collection API-versie) uit de locatiekoptekst in de reactie:

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
