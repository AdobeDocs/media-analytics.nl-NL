---
title: Pingsgebeurtenissen verzenden
description: null
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Pingsgebeurtenissen verzenden{#sending-ping-events}

**Voor hoofdinhoud, moet u in brand pingelen gebeurtenissen elke 10 seconden, die na 10 seconden van playback beginnen, ongeacht andere API gebeurtenissen die u hebt verzonden. Voor het volgen van de Advertentie, moet u pingelen gebeurtenissen elke 1 seconde in brand steken.**

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

