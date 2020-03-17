---
title: Gebeurtenissen in de wachtrij plaatsen wanneer de reactie van de sessie traag is
description: null
uuid: 39ea59d9-89d3-4087-a806-48a43ecf0c98
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Gebeurtenissen in de wachtrij plaatsen wanneer de reactie van de sessie traag is{#queueing-events-when-sessions-response-is-slow}

De Media Collection API is RESTful: U moet dus een HTTP-aanvraag indienen en op de reactie wachten. Dit is een belangrijk punt slechts voor wanneer u een verzoek [van de](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) Zitting indient om een identiteitskaart van de Zitting aan het begin van videoplayback te verkrijgen. Dit is belangrijk omdat identiteitskaart van de Zitting voor alle verdere volgende het volgen vraag wordt vereist.

Het is mogelijk dat de speler gebeurtenissen kan starten _voordat de reactie Sessies vanaf de achtergrond wordt geretourneerd_ (met de parameter Session ID). Als dit gebeurt, moet uw app alle volgende gebeurtenissen in de wachtrij plaatsen die aankomen tussen de aanvraag [voor](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) sessies en het antwoord daarop. Wanneer de reactie van Sessies aankomt, zou u eerst om het even welke een rij gevormde [gebeurtenissen](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)moeten verwerken, dan kunt u beginnen verwerkend _levende_ gebeurtenissen met de vraag van [Gebeurtenissen](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) .

>[!NOTE]
>
>De [Events-aanvraag](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) retourneert geen gegevens meer naar de client dan een HTTP-antwoordcode.

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

**Verwerk gebeurtenissen in de wachtrij -** De verwijzingsspeler verwerkt gebeurtenissen in de wachtrij als volgt:

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
