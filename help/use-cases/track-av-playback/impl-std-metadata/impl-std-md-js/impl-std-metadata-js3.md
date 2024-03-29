---
title: Leer standaardmetagegevens implementeren met JavaScript 3.x
description: Leer hoe u standaardvideo- en advertentiemetagegevens instelt die moeten worden verzonden met trackingaanroepen in browser-apps (JS 3.x).
exl-id: 228ba000-10e2-4906-8417-265a03367a9b
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '48'
ht-degree: 6%

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
