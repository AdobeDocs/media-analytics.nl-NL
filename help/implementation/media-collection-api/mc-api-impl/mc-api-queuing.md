---
title: Gebeurtenissen in wachtrij wanneer de reactie op sessies traag is
description: Leer wat te doen wanneer Sessie-id wordt geretourneerd nadat de speler gebeurtenissen heeft geactiveerd.
uuid: 39ea59d9-89d3-4087-a806-48a43ecf0c98
exl-id: 2c23c378-c104-4256-b6e7-8eb6871f62da
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---

# Gebeurtenissen in de wachtrij plaatsen wanneer de reactie van de sessie traag is{#queueing-events-when-sessions-response-is-slow}

De Media Collection API is RESTful: d.w.z., maakt u een HTTP- verzoek en wacht op de reactie. Dit is een belangrijk punt slechts voor wanneer u a [&#x200B; verzoek van zittingen &#x200B;](../mc-api-ref/mc-api-sessions-req.md) maakt om een identiteitskaart van de Zitting aan het begin van videoplayback te verkrijgen. Dit is belangrijk omdat identiteitskaart van de Zitting voor alle verdere volgende het volgen vraag wordt vereist.

Het is mogelijk dat uw speler gebeurtenissen _kan in brand steken alvorens de reactie van Zittingen_ (met de parameter van identiteitskaart van de Zitting) van het achtereind terugkeert. Als dit voorkomt, moet uw app om het even welke volgende gebeurtenissen in de rij plaatsen die tussen het [&#x200B; verzoek van Zittingen &#x200B;](../mc-api-ref/mc-api-sessions-req.md) en zijn reactie aankomen. Wanneer de reactie van Sessies aankomt, zou u om het even welke een rij gevormde [&#x200B; gebeurtenissen &#x200B;](../mc-api-ref/mc-api-events-req.md) eerst moeten verwerken, dan kunt u beginnen _levende_ gebeurtenissen met de [&#x200B; Gebeurtenissen &#x200B;](../mc-api-ref/mc-api-events-req.md) vraag.

>[!NOTE]
>
>Het [&#x200B; verzoek van Gebeurtenissen &#x200B;](../mc-api-ref/mc-api-events-req.md) keert geen gegevens terug naar de cliënt voorbij een de reactiecode van HTTP.

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

**Proces om het even welke een rij gevormde gebeurtenissen -** de verwijzingsspeler verwerkt een rij gevormde gebeurtenissen als volgt:

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
