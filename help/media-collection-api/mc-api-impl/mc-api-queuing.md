---
title: Gebeurtenissen in de wachtrij plaatsen wanneer de reactie van de sessie traag is
description: Gebeurtenissen in de wachtrij plaatsen wanneer de reactie van de sessie traag is
uuid: 39ea59d9-89d3-4087-a806-48a43ecf0c98
exl-id: 2c23c378-c104-4256-b6e7-8eb6871f62da
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 1%

---

# Gebeurtenissen in een wachtrij plaatsen wanneer de reactie van de sessie langzaam is{#queueing-events-when-sessions-response-is-slow}

De Media Collection API is RESTful: U moet dus een HTTP-aanvraag indienen en op de reactie wachten. Dit is een belangrijk punt slechts voor wanneer u [Sessies request](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) maakt om een identiteitskaart van de Zitting aan het begin van videoplayback te verkrijgen. Dit is belangrijk omdat identiteitskaart van de Zitting voor alle verdere volgende het volgen vraag wordt vereist.

Het is mogelijk dat uw speler gebeurtenissen _kan branden alvorens de reactie van Zittingen_ (met de parameter van identiteitskaart van de Zitting) van het achtereind terugkeert. Als dit gebeurt, moet uw app alle volgende gebeurtenissen in de wachtrij plaatsen die aankomen tussen het [verzoek om sessies](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) en het antwoord daarop. Wanneer de reactie van Zittingen aankomt, zou u om het even welke een rij gevormde [gebeurtenissen](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) eerst moeten verwerken, dan kunt u beginnen verwerkend _live_ gebeurtenissen met [Gebeurtenissen](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) vraag.

>[!NOTE]
>
>De [Gebeurtenisaanvraag](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) retourneert geen gegevens naar de client die verder gaan dan een HTTP-antwoordcode.

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

**Verwerk gebeurtenissen in de wachtrij -** De referentiespeler verwerkt gebeurtenissen in de wachtrij als volgt:

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
