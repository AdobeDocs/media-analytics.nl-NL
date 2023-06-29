---
title: Afspelen van bijgehouden inhoud beschreven
description: "Meer informatie over het bijhouden van het afspelen van de kern, zoals het laden van de media, het starten van de media, het pauzeren van de media en het voltooien van de media. "
uuid: 7b8e2f76-bc4e-4721-8933-3e4453b01788
exl-id: 98ad2783-c9e3-48de-88df-8549f26114a0
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a26e4e283646e5ceb352f357789748f376f5c747
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 0%

---

# Overzicht van bijhouden{#tracking-overview}

Deze documentatie behandelt het volgen in versie 2.x van SDK.

>[!IMPORTANT]
>
>Als u een 1.x-versie van de SDK implementeert, kunt u hier de 1.x-handleidingen voor ontwikkelaars downloaden: [SDK&#39;s downloaden.](/help/getting-started/download-sdks.md)

## Player Events

Tot het bijhouden van het afspelen van de kern behoren het bijhouden van het laden van media, het starten van media, het pauzeren van media en het voltooien van media. Hoewel dit niet verplicht is, vormen het bijhouden van buffering en zoeken ook kerncomponenten die worden gebruikt voor het bijhouden van het afspelen van inhoud. In uw media speler API, identificeer de spelergebeurtenissen die met de het volgen vraag van SDK van Media beantwoorden, en codeer uw gebeurtenismanagers om het volgen APIs te roepen, en vereiste en facultatieve variabelen te bevolken.

### Bij laden van media

* Het mediaobject maken
* Metagegevens vullen
* Bellen `trackSessionStart`; Bijvoorbeeld: `trackSessionStart(mediaObject, contextData)`

### Bij starten van media

* Bellen `trackPlay`

### Bij pauzeren/hervatten

* Bellen `trackPause`
* Bellen `trackPlay`   _wanneer het afspelen wordt hervat_

### Op media voltooid

* Bellen `trackComplete`

### Bij afbreken van media

* Bellen `trackSessionEnd`

### Bij starten van scrubben

* Bellen `trackEvent(SeekStart)`

### Als scrubben eindigt

* Bellen `trackEvent(SeekComplete)`
Wijzigingen annuleren

### Wanneer de buffering wordt gestart

* Bellen `trackEvent(BufferStart);`

### Wanneer het bufferen eindigt

* Bellen `trackEvent(BufferComplete);`

>[!TIP]
>
>De positie van de afspeelkop wordt ingesteld als onderdeel van de instellings- en configuratiecode. Meer informatie over `getCurrentPlayheadTime`, zie [Overzicht: Algemene uitvoeringsrichtsnoeren.](/help/implementation/media-sdk-overview.md)


## Implementeren {#implement}

1. **Eerste instelling voor bijhouden -** Identificeer wanneer de gebruiker de bedoeling van playback teweegbrengt (de gebruiker klikt spel en/of autoplay is) en creeer een `MediaObject` -instantie die de mediagegevens gebruikt voor de naam van de inhoud, de inhoud-id, de lengte van de inhoud en het stroomtype.

   **`MediaObject`referentie:**

   | Naam variabele | Beschrijving | Vereist |
   |---|---|---|
   | `name` | Naam van inhoud | Ja |
   | `mediaid` | Unieke id voor inhoud | Ja |
   | `length` | Lengte van inhoud | Ja |
   | `streamType` | Het type Stream | Ja |
   | `mediaType` | Mediatype (audio- of video-inhoud) | Ja |

   **`StreamType`constanten:**

   | Naam van constante | Beschrijving |
   |---|---|
   | `VOD` | Het type van stroom voor Video op bestelling. |
   | `LIVE` | Het type van stroom voor Levende inhoud. |
   | `LINEAR` | Het type van stroom voor Lineaire inhoud. |
   | `AOD` | Stroomtype voor audio op aanvraag |
   | `AUDIOBOOK` | Het type van stroom voor audioboek |
   | `PODCAST` | Stroomtype voor Podcast |

   **`MediaType`constanten:**

   | Naam van constante | Beschrijving |
   |---|---|
   | `Audio` | Mediatype voor audiostreams. |
   | `Video` | Mediatype voor videostreams. |

   De algemene indeling voor het maken van de `MediaObject` is `MediaHeartbeat.createMediaObject(<MEDIA_NAME>, <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);`

1. **Metagegevens koppelen -** Koppel standaard- en/of aangepaste metagegevensobjecten optioneel aan de volgende sessie via de variabelen van de contextgegevens.

   * **Standaardmetagegevens -**

     >[!NOTE]
     >
     >Het koppelen van het standaardobject voor metagegevens aan het mediaobject is optioneel.

     Instantiëren van een standaard metagegevensobject, vullen van de gewenste variabelen en stellen het metagegevensobject in op het Media Heartbone-object.

     Zie de uitgebreide lijst met metagegevens hier: [Parameters voor audio en video.](../../implementation/variables/audio-video-parameters.md)

   * **Aangepaste metagegevens -** Maak een veranderlijk object voor de douanevariabelen en bevolk met de gegevens voor deze inhoud.

1. **Houd de intentie bij om het afspelen te starten -** Als u een sessie wilt volgen, roept u `trackSessionStart` op de Media Heartbone-instantie.

   >[!IMPORTANT]
   >
   >`trackSessionStart` Hiermee wordt bijgehouden wat de gebruiker wil afspelen, niet het begin van het afspelen. Deze API wordt gebruikt om de gegevens/meta-gegevens te laden en tijd-aan-begin metrische QoS (de tijdsduur tussen `trackSessionStart` en `trackPlay`).

   >[!NOTE]
   >
   >Als u geen aangepaste metagegevens gebruikt, kunt u gewoon een leeg object verzenden voor de `data` argument in `trackSessionStart`.

1. **Het feitelijke begin van het afspelen bijhouden -** Identificeer de gebeurtenis van de media speler voor het begin van de playback, waar het eerste kader van de inhoud op het scherm wordt teruggegeven, en vraag `trackPlay`.

1. **De voltooiing van het afspelen volgen -** Identificeer de gebeurtenis van de media speler voor de voltooiing van het playback, waar de gebruiker de inhoud tot het eind heeft bekeken, en vraag `trackComplete`.

1. **Het einde van de sessie volgen -** Identificeer de gebeurtenis van de media speler voor het leegmaken/sluiten van het playback, waar de gebruiker de inhoud sluit en/of de inhoud wordt voltooid en is leeggemaakt, en vraag `trackSessionEnd`.

   >[!IMPORTANT]
   >
   >`trackSessionEnd` markeert het einde van een volgende sessie. Als de sessie succesvol is gecontroleerd naar voltooiing, waarbij de gebruiker de inhoud tot het einde heeft bekeken, zorgt u ervoor dat `trackComplete` wordt eerder aangeroepen `trackSessionEnd`. andere `track*` API-aanroep wordt genegeerd na `trackSessionEnd`, met uitzondering van `trackSessionStart` voor een nieuwe traceringssessie.

1. **Houd alle mogelijke pauzescenario&#39;s bij -** Identificeer de gebeurtenis van de media speler voor pauze en vraag `trackPause`.

   **Scenario&#39;s pauzeren -** Identificeer om het even welk scenario waarin de Speler zal pauzeren en zorg ervoor dat `trackPause` wordt correct geroepen. De volgende scenario&#39;s vereisen allemaal dat uw app wordt aangeroepen `trackPause()`:

   * De gebruiker raakt expliciet de pauze in de app.
   * De speler plaatst zichzelf in de pauzestatus.
   * (*Mobiele apps*) - De gebruiker plaatst de toepassing op de achtergrond, maar u wilt dat de toepassing de sessie geopend houdt.
   * (*Mobiele apps*) - Elk type onderbreking van het systeem treedt op waardoor een toepassing achteraan wordt geplaatst. Bijvoorbeeld, ontvangt de gebruiker een vraag, of een pop-up van een andere toepassing komt voor, maar u wilt de toepassing de zitting levend houden om de gebruiker de kans te geven om de inhoud van het punt van onderbreking te hervatten.

1. De gebeurtenis van de speler identificeren voor afspelen en/of hervatten vanuit pauzeren en aanroepen `trackPlay`.

   >[!TIP]
   >
   >Dit kan de zelfde gebeurtenisbron zijn die in Stap 4 werd gebruikt. Zorg ervoor dat elk `trackPause()` API-aanroep is gekoppeld aan het volgende `trackPlay()` API-aanroep wanneer het afspelen wordt hervat.

1. Luister naar afspeelzoekgebeurtenissen van de mediaspeler. Bij het zoeken van een begingebeurtenismelding zoekt u naar het gebruik van de `SeekStart` gebeurtenis.
1. Volg bij het zoeken naar volledige meldingen van de mediaspeler het einde van het zoeken met de `SeekComplete` gebeurtenis.
1. Luister naar de buffergebeurtenissen voor het afspelen vanaf de mediaspeler en volg bij een melding van een bufferstart de buffering met de knop `BufferStart` gebeurtenis.
1. Volg bij het verzenden van het volledige bericht over de buffer vanuit de mediaspeler het einde van de buffering met de `BufferComplete` gebeurtenis.

Zie voorbeelden van elke stap in de volgende platformspecifieke onderwerpen, en bekijk de steekproefspelers inbegrepen met uw SDKs.

Zie dit gebruik van de JavaScript 2.x-SDK in een HTML5-speler voor een eenvoudig voorbeeld van het bijhouden van het afspelen:

```js
/* Call on media start */
if (e.type == "play") {

    // Check for start of media
    if (!sessionStarted) {
        /* Set media info */     
        /* MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                            <MEDIA_ID>,  
                                            <MEDIA_LENGTH>,
                                            <MEDIA_STREAMTYPE>,
                                            <MEDIA_MEDIATYPE>);*/
        var mediaInfo = MediaHeartbeat.createMediaObject(
          document.getElementsByTagName('video')[0].getAttribute("name"),  
          document.getElementsByTagName('video')[0].getAttribute("id"),  
          video.duration,
          MediaHeartbeat.StreamType.VOD);

        /* Set custom context data */
        var customVideoMetadata = {
            isUserLoggedIn: "false",
            tvStation: "Sample TV station",
            programmer: "Sample programmer"
        };

        /* Set standard video metadata */     
        var standardVideoMetadata = {};
        standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.EPISODE] = "Sample Episode";
        standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.SHOW] = "Sample Show";
        mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata,  
                           standardVideoMetadata);     

        // Start Session
        this.mediaHeartbeat.trackSessionStart(mediaInfo, customVideoMetadata);    

        // Track play
        this.mediaHeartbeat.trackPlay();  
        sessionStarted = true;     

    } else {
        // Track play for resuming playack    
        this.mediaHeartbeat.trackPlay();  
    }
};

/* Call on video complete */
if (e.type == "ended") {
    console.log("video ended");
    this.mediaHeartbeat.trackComplete();
    this.mediaHeartbeat.trackSessionEnd();
    sessionStarted = false;     
};

/* Call on pause */
if (e.type == "pause") {
    this.mediaHeartbeat.trackPause();
};

/* Call on scrub start */
if (e.type == "seeking") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart);
};

/* Call on scrub stop */
if (e.type == "seeked") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete);
};

/* Call on buffer start */
if (e.type == "buffering") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart);
};

/* Call on buffer complete */
if (e.type == "buffered") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete);
};
```

## Valideren {#validate}

Voor informatie over het valideren van uw *verouderd* implementatie, zie [Oudere validatie.](/help/legacy/validation/validation-overview.md)
