---
title: Pingsgebeurtenissen verzenden
description: Pinggebeurtenissen vormen de hartslag van de Streaming Media Collection. Leer hoe te om een getimed te verzenden pingelt voor belangrijkste inhoud of en het volgen van advertenties.
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# Pingsgebeurtenissen verzenden{#sending-ping-events}

**u moet in brand steken pingelt gebeurtenissen om de 10 seconden, die na 10 seconden van playback beginnen, ongeacht andere API gebeurtenissen die u hebt verzonden. Dit is zowel voor hoofdinhoud als voor het bijhouden van advertenties van toepassing.**

Pingel gebeurtenissen zijn &quot;hartslag&quot;van de het stromen Inzameling van Media. De enige vereiste parameters voor een ping-aanroep zijn `eventType: ping` samen met het `playerTime` -object (positie afspeelkop en tijdstempel).

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
