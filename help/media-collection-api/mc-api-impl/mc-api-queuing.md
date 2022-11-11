---
title: Gebeurtenissen in wachtrij plaatsen wanneer de reactie op sessies traag is
description: Leer wat te doen wanneer Sessie-id wordt geretourneerd nadat de speler gebeurtenissen heeft geactiveerd.
uuid: 39ea59d9-89d3-4087-a806-48a43ecf0c98
exl-id: 2c23c378-c104-4256-b6e7-8eb6871f62da
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: d89b2af2e2ae5a170ce98f62656cdeed6fe31f19
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 4%

---

# Gebeurtenissen in de wachtrij plaatsen wanneer de reactie van de sessie traag is{#queueing-events-when-sessions-response-is-slow}

De Media Collection API is RESTful: U moet dus een HTTP-aanvraag indienen en op de reactie wachten. Dit is alleen belangrijk wanneer u een [Aanvraag voor sessies](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) om een sessie-id te verkrijgen aan het begin van het afspelen van de video. Dit is belangrijk omdat identiteitskaart van de Zitting voor alle verdere volgende het volgen vraag wordt vereist.

Het is mogelijk dat uw speler gebeurtenissen kan starten _voordat de reactie Sessies wordt geretourneerd_ (met de parameter van identiteitskaart van de Zitting) van het achterste eind. Als dit gebeurt, moet uw toepassing alle volgende gebeurtenissen in de wachtrij plaatsen die tussen de [Aanvraag voor sessies](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) en haar antwoord. Wanneer de reactie van Zittingen aankomt, zou u om het even welke rij eerst moeten verwerken [gebeurtenissen](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)en dan kunt u beginnen met de verwerking _leven_ gebeurtenissen met de [Gebeurtenissen](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) oproepen.

>[!NOTE]
>
>De [Verzoek om gebeurtenissen](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) geeft geen gegevens meer dan een HTTP-antwoordcode terug naar de client.

Controleer de Speler van de Verwijzing in uw distributie voor één manier om gebeurtenissen te verwerken alvorens een identiteitskaart van de Zitting te ontvangen. Bijvoorbeeld:

```js
var eventData = {};            // JSON payload 
eventData.playerTime = getPlayerTime(); // Required 
eventData.eventType = "play";           // Required 
eventData.params = {};                  // Optional for events 
 
VideoPlayer.prototype._collectEvent =  
  function(eventData) { 
 
    // If we don't have a Session ID yet,  
    // queue the event and return... 
    if (!sessionStarted) { 
        console.log("[Player] Queueing event "); 
        _pendingEvents.push(eventData); 
        return; 
    } 
 
    // If we DO have a Session ID, process the 
    // tracking event...     
    apiClient.request({ 
        "baseUrl": "{endpoint}", 
        "path": "api/v1/{sid}/events", // events request 
        "method": "POST", 
        "data": eventData 
    }).then((response) => {   
        […] 
    } 
} 
 
VideoPlayer.prototype.collectEvent =  
  function (eventType, eventParams) { 
         
    if (typeof eventParams === 'undefined') {   
        eventParams = {}; 
    } 
 
    this._collectEvent({                   
        eventType: eventType,            // Required 
        playerTime: getPlayerTime(),     // Required 
        params: eventParams              // Optional  
    });                                    
}; 
 
VideoPlayer.prototype.getPlayerTime = function() { 
    return { 
        playhead: this.getPlayhead(),    // playhead value in seconds 
        ts: this.getCurrentTimestamp()   // timestamp value in milliseconds 
    }; 
};
```

**Alle gebeurtenissen in de wachtrij verwerken -** De referentiespeler verwerkt gebeurtenissen in de wachtrij als volgt:

```js
    […] 
    this._processPendingEvents();    // Once you have a Session ID, 
    […]                              // process any queued events 
 
VideoPlayer.prototype._processPendingEvents =  
  function() { 
    this._pendingEvents.forEach((eventData) => { 
        this._collectEvent(eventData); 
    }); 
 
    this._pendingEvents = []; 
}
```

Ga door met het verwerken van &#39;tracking&#39;-gebeurtenissen zoals deze zich voordoen.
