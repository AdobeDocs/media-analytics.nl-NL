---
title: Ping-gebeurtenissen verzenden
description: Pinggebeurtenissen vormen de hartslag van de Streaming Media Analytics. Leer hoe te om een getimed te verzenden pingelt voor belangrijkste inhoud of en het volgen van advertenties.
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 2%

---

# Pingsgebeurtenissen verzenden{#sending-ping-events}

**Voor hoofdinhoud, moet u in brand pingelen gebeurtenissen elke 10 seconden, die na 10 seconden van playback beginnen, ongeacht andere API gebeurtenissen die u hebt verzonden. Voor het volgen van Advertentie, moet u pingelen gebeurtenissen elke 1 seconde in brand steken.**

Pingel gebeurtenissen zijn letterlijk de &quot;hartslag&quot;van de Analytics van Media. De enige vereiste parameters voor pingelen vraag zijn `eventType: ping` samen met het `playerTime` voorwerp (playhead positie en timestamp).

Het volgende codefragment toont één manier om een getimede pingend mechanisme voor belangrijkste inhoud (10 tweede interval) uit te voeren:

```js
... 
Pinger.init(10000); 
... 
Pinger.kill();

var Pinger = { 
    init: function(interval) { 
        this._timer = window.setInterval(function() { 
                $.event.trigger({type: "onPing", _data: ""}); 
            }, interval); 
    }, 
     
    kill: function() { 
        window.clearInterval(this._timer); 
    } 
}
```
