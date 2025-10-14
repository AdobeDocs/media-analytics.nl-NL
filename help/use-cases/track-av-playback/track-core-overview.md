---
title: Afspelen van bijgehouden inhoud beschreven
description: 'Leer hoe u het afspelen van de kern kunt bijhouden, zoals het laden van media, het starten van media, het pauzeren van media en het voltooien van media. '
uuid: 7b8e2f76-bc4e-4721-8933-3e4453b01788
exl-id: 98ad2783-c9e3-48de-88df-8549f26114a0
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 0%

---

# Overzicht van bijhouden{#tracking-overview}

Deze documentatie behandelt het volgen in versie 2.x van de SDK.

>[!IMPORTANT]
>
>Als u een 1.x versie van SDK uitvoert, kunt u 1.x de Gidsen van Ontwikkelaars hier downloaden: [&#x200B; Download SDKs.](/help/getting-started/download-sdks.md)

## Player Events

Tot het bijhouden van het afspelen van de kern behoren het bijhouden van het laden van media, het starten van media, het pauzeren van media en het voltooien van media. Hoewel dit niet verplicht is, vormen het bijhouden van buffering en zoeken ook kerncomponenten die worden gebruikt voor het bijhouden van het afspelen van inhoud. In uw media speler API, identificeer de spelergebeurtenissen die met de Media SDK volgen vraag beantwoorden, en codeer uw gebeurtenismanagers om het volgen APIs te roepen, en vereiste en facultatieve variabelen te bevolken.

### Bij laden van media

* Het mediaobject maken
* Metagegevens vullen
* Roep `trackSessionStart` aan, bijvoorbeeld: `trackSessionStart(mediaObject, contextData)`

### Bij starten van media

* Roep `trackPlay`

### Bij pauzeren/hervatten

* Roep `trackPause`
* Roep `trackPlay`   _wanneer de playback_ hervat

### Op media voltooid

* Roep `trackComplete`

### Bij afbreken van media

* Roep `trackSessionEnd`

### Bij starten van scrubben

* Roep `trackEvent(SeekStart)`

### Als scrubben eindigt

* Roep `trackEvent(SeekComplete)`
Wijzigingen annuleren

### Wanneer de buffering wordt gestart

* Roep `trackEvent(BufferStart);`

### Wanneer het bufferen eindigt

* Roep `trackEvent(BufferComplete);`


## Implementeren {#implement}

1. **Aanvankelijke het volgen opstelling -** identificeert zich wanneer de gebruiker de bedoeling van playback teweegbrengt (de gebruiker klikt spel en/of autoplay is) en creeert een `MediaObject` instantie gebruikend de media informatie voor inhoudsnaam, inhoudsidentiteitskaart, inhoudslengte, en stroomtype.

   **`MediaObject`reference:**

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
   | `LIVE` | Streamtype voor Live-inhoud. |
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

1. **maak meta-gegevens -** naar keuze vast standaard en/of douanemeta-gegevensvoorwerpen aan de volgende zitting door de variabelen van contextgegevens.

   * **Standaard meta-gegevens -**

     >[!NOTE]
     >
     >Het koppelen van het standaardobject voor metagegevens aan het mediaobject is optioneel.

     Instantiëren van een standaard metagegevensobject, vullen van de gewenste variabelen en stellen het metagegevensobject in op het Media Heartbone-object.

     Zie de uitvoerige lijst van meta-gegevens hier: [&#x200B; Audio en videoparameters.](../../implementation/variables/audio-video-parameters.md)

   * **meta-gegevens van de Douane -** creeer een veranderlijk voorwerp voor de douanevariabelen en bevolk met de gegevens voor deze inhoud.

1. **spoor het voornemen om playback te beginnen -** beginnen een zitting te volgen, vraag `trackSessionStart` op de instantie van de Hartslag van Media.

   >[!IMPORTANT]
   >
   >In `trackSessionStart` wordt bijgehouden wat de gebruiker wil afspelen, niet het begin van het afspelen. Deze API wordt gebruikt om de gegevens/meta-gegevens te laden en tijd-aan-begin metrische QoS (de tijdduur tussen `trackSessionStart` en `trackPlay`) te schatten.

   >[!NOTE]
   >
   >Als u geen aangepaste metagegevens gebruikt, verzendt u gewoon een leeg object voor het argument `data` in `trackSessionStart` .

1. **spoor het daadwerkelijke begin van playback -** identificeer de gebeurtenis van de media speler voor het begin van de playback, waar het eerste kader van de inhoud op het scherm wordt teruggegeven, en vraag `trackPlay`.

1. **spoor de voltooiing van playback -** identificeer de gebeurtenis van de media speler voor de voltooiing van de playback, waar de gebruiker de inhoud tot het eind heeft gecontroleerd, en vraag `trackComplete`.

1. **Spoor het eind van de zitting -** identificeer de gebeurtenis van de media speler voor het ontladen/sluiten van de playback, waar de gebruiker de inhoud en/of de inhoud sluit wordt voltooid en, en vraag `trackSessionEnd` verwijderd.

   >[!IMPORTANT]
   >
   >`trackSessionEnd` markeert het einde van een volgende sessie. Als de sessie succesvol is gecontroleerd op voltooiing, waarbij de gebruiker de inhoud tot het einde heeft gecontroleerd, controleert u of `trackComplete` vóór `trackSessionEnd` is aangeroepen. Eventuele andere `track*` API-aanroepen worden na `trackSessionEnd` genegeerd, behalve voor `trackSessionStart` voor een nieuwe traceringssessie.

1. **spoor alle mogelijke pauzescenario&#39;s -** identificeer de gebeurtenis van de media speler voor pauze en vraag `trackPause`.

   **Scenario&#39;s van de Pauze -** identificeer om het even welk scenario waarin de Speler zal pauzeren en ervoor zorgen dat `trackPause` behoorlijk wordt geroepen. De volgende scenario&#39;s vereisen allemaal dat uw app `trackPause()` aanroept:

   * De gebruiker raakt expliciet de pauze in de app.
   * De speler plaatst zichzelf in de pauzestatus.
   * (*Mobiele Apps*) - de gebruiker zet de toepassing in de achtergrond, maar u wilt dat app de zitting open houdt.
   * (*Mobiele Apps*) - om het even welk type van systeem onderbreekt komt voor dat een toepassing veroorzaakt om worden gesteund. Bijvoorbeeld, ontvangt de gebruiker een vraag, of een pop-up van een andere toepassing komt voor, maar u wilt de toepassing de zitting levend houden om de gebruiker de kans te geven om de inhoud van het punt van onderbreking te hervatten.

1. Identificeer de gebeurtenis van de speler voor spel en/of hervat van pauze en vraag `trackPlay`.

   >[!TIP]
   >
   >Dit kan de zelfde gebeurtenisbron zijn die in Stap 4 werd gebruikt. Zorg ervoor dat elke API-aanroep van `trackPause()` wordt gekoppeld aan een volgende API-aanroep van `trackPlay()` wanneer het afspelen wordt hervat.

1. Luister naar afspeelzoekgebeurtenissen van de mediaspeler. Bij het zoeken naar meldingen bij het starten van een gebeurtenis, zoekt u naar de gebeurtenis `SeekStart` .
1. Volg bij het zoeken naar volledige meldingen van de mediaspeler het einde van het zoeken met de gebeurtenis `SeekComplete` .
1. Luister naar de buffergebeurtenissen voor het afspelen vanaf de mediaspeler en volg de buffering met de gebeurtenis `BufferStart` bij het melden van de buffergebeurtenis.
1. Volg bij het verzenden van het volledige bericht over de buffer vanuit de mediaspeler het einde van de buffering met de gebeurtenis `BufferComplete` .

Zie voorbeelden van elke stap in de volgende platformspecifieke onderwerpen, en bekijk de steekproefspelers inbegrepen met uw SDKs.

Zie dit gebruik van de JavaScript 2.x SDK in een HTML5-speler voor een eenvoudig voorbeeld van afspelen:

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

Voor informatie bij het bevestigen van uw *erfenis* implementatie, zie [&#x200B; Validering van de Oudheid.](/help/legacy/validation/validation-overview.md)
