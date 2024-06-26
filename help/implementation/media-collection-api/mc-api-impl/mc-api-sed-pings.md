---
title: Pingsgebeurtenissen verzenden
description: Pinggebeurtenissen vormen de hartslag van de invoegtoepassing voor het streamen van media. Leer hoe te om een getimed te verzenden pingelt voor belangrijkste inhoud of en het volgen van advertenties.
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 240fa48bdc738425e04cd29c27625c7dd612ff18
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# Pingsgebeurtenissen verzenden{#sending-ping-events}

**U moet pingelen gebeurtenissen elke 10 seconden in brand steken, die na 10 seconden van playback beginnen, ongeacht andere API gebeurtenissen die u hebt verzonden. Dit geldt zowel voor de hoofdinhoud als voor het bijhouden van advertenties.**

Pingel gebeurtenissen zijn de &quot;hartslag&quot;van de Invoegsel van de Inzameling van Media het Streamen. De enige vereiste parameters voor pingelen vraag zijn `eventType: ping` samen met de `playerTime` object (positie afspeelkop en tijdstempel).

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
