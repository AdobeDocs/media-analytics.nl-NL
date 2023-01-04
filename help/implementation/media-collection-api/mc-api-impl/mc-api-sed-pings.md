---
title: Ping-gebeurtenissen verzenden
description: Pinggebeurtenissen vormen de hartslag van de Streaming Media Analytics. Leer hoe te om een getimed te verzenden pingelt voor belangrijkste inhoud of en het volgen van advertenties.
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 2%

---

# Pingsgebeurtenissen verzenden{#sending-ping-events}

**Voor hoofdinhoud, moet u in brand pingelen gebeurtenissen elke 10 seconden, die na 10 seconden van playback beginnen, ongeacht andere API gebeurtenissen die u hebt verzonden. Voor het volgen van de Advertentie, moet u pingelen gebeurtenissen elke 1 seconde in brand steken.**

Pingel gebeurtenissen zijn letterlijk de &quot;hartslag&quot;van de Analytics van Media. De enige vereiste parameters voor pingelen vraag zijn `eventType: ping` samen met de `playerTime` object (positie afspeelkop en tijdstempel).

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