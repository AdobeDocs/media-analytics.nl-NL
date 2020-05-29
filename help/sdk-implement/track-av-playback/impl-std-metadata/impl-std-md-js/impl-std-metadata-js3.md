---
title: Standaardmetagegevens implementeren met JavaScript 3.x
description: Beschrijft het plaatsen van standaardvideo en admeta-gegevens die met het volgen vraag in browser apps (JS) moeten worden verzonden.
translation-type: tm+mt
source-git-commit: 318bb60d9835d9a07fb7aa0a0a02162248410d09
workflow-type: tm+mt
source-wordcount: '43'
ht-degree: 4%

---


# Standaardmetagegevens implementeren met JavaScript 3.x{#implement-standard-metadata-on-javascript}

## Implementatie

Instantiëren van een contextgegevensobject en vullen de gewenste standaardmetagegevensvariabelen in. Bijvoorbeeld:

```js
_onVideoLoad = function () {
    //Create the Media Object
    var mediaObject =
      ADB.Media.createMediaObject(<MEDIA_NAME>,
                                       <MEDIA_ID,
                                       <MEDIA_LENGTH>,
                                       <STREAM_TYPE>,
                                       <MEDIA_TYPE>);

    //Set standard Video Metadata
    var contextData = {};
    contextData = "Sample Show";
    contextData = "Sample Season";
    contextData = "Sample Episode";

    //Set standard Audio Metadata
    var contextData = {};
    contextData = "Sample Artist";
    contextData = "Sample Album";
    contextData = "Sample Label";

    this.tracker.trackSessionStart(mediaObject, contextData);
};
```
