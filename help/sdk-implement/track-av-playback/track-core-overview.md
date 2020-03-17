---
title: Overzicht van bijhouden
description: 'In dit onderwerp wordt het bijhouden van het afspelen van de kernelementen beschreven, zoals het laden van media, het starten van media, het pauzeren van media en het voltooien van media. '
uuid: 7b8e2f76-bc4e-4721-8933-3e4453b01788
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Overzicht van bijhouden{#tracking-overview}

>[!IMPORTANT]
>
>Deze documentatie behandelt het volgen in versie 2.x van SDK. Als u een 1.x-versie van de SDK implementeert, kunt u hier de 1.x-handleidingen voor ontwikkelaars downloaden: SDK&#39;s [downloaden.](/help/sdk-implement/download-sdks.md)

## Player Events

Tot het bijhouden van het afspelen van de kern behoren het bijhouden van het laden van media, het starten van media, het pauzeren van media en het voltooien van media. Hoewel dit niet verplicht is, vormen het bijhouden van buffering en zoeken ook kerncomponenten die worden gebruikt voor het bijhouden van het afspelen van inhoud. In uw media speler API, identificeer de spelergebeurtenissen die met de het volgen vraag van SDK van Media beantwoorden, en codeer uw gebeurtenismanagers om het volgen APIs te roepen, en vereiste en facultatieve variabelen te bevolken.

### Bij laden van media

* Het mediaobject maken
* Metagegevens vullen
* oproep `trackSessionStart`; Bijvoorbeeld: `trackSessionStart(mediaObject, contextData)`

### Bij starten van media

* Bellen `trackPlay`

### Bij pauzeren/hervatten

* Bellen `trackPause`
* Bellen `trackPlay` _wanneer het afspelen wordt hervat_

### Op media voltooid

* Bellen `trackComplete`

### Bij afbreken van media

* Bellen `trackSessionEnd`

### Bij starten van scrubben

* Bellen `trackEvent(SeekStart)`

### Als scrubben eindigt

* Bellen `trackEvent(SeekComplete)`

### Wanneer de buffering wordt gestart

* Bellen `trackEvent(BufferStart);`

### Wanneer het bufferen eindigt

* Bellen `trackEvent(BufferComplete);`

>[!TIP]
>
>De positie van de afspeelkop wordt ingesteld als onderdeel van de instellings- en configuratiecode. Voor meer informatie over `getCurrentPlayheadTime`, zie [Overzicht: Algemene uitvoeringsrichtsnoeren.](/help/sdk-implement/setup/setup-overview.md#general-implementation-guidelines)

## Implementeren {#implement}

1. **Initiële instelling voor bijhouden -** Identificeer wanneer de gebruiker de afspeelintentie activeert (de gebruiker klikt op Afspelen en/of Automatisch afspelen is ingeschakeld) en maak een `MediaObject` instantie met de mediagegevens voor de naam van de inhoud, de inhoud-id, de lengte van de inhoud en het type stream.

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

   De algemene indeling voor het maken van het `MediaObject` object is `MediaHeartbeat.createMediaObject(<MEDIA_NAME>, <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);`

1. **Metagegevens koppelen -** Eventueel standaard en/of aangepaste metagegevensobjecten koppelen aan de volgende sessie via de variabelen van contextgegevens.

   * **Standaardmetagegevens -**

      >[!NOTE]
      >
      >Het koppelen van het standaardobject voor metagegevens aan het mediaobject is optioneel.

      Instantiëren van een standaard metagegevensobject, vullen van de gewenste variabelen en stellen het metagegevensobject in op het Media Heartbone-object.

      Zie de uitgebreide lijst met metagegevens hier: Parameters voor [audio en video.](/help/metrics-and-metadata/audio-video-parameters.md)

   * **Aangepaste metagegevens -** Maak een variabelenobject voor de aangepaste variabelen en vul de gegevens voor deze inhoud in.

1. **Houd de intentie bij om het afspelen te starten -** Als u een sessie wilt volgen, roept u `trackSessionStart` de Media Heartmaatinstantie aan.

   >[!IMPORTANT]
   >
   >`trackSessionStart` Hiermee wordt bijgehouden wat de gebruiker wil afspelen, niet het begin van het afspelen. Deze API wordt gebruikt om de gegevens/meta-gegevens te laden en tijd-aan-begin metrische QoS (de tijdduur tussen `trackSessionStart` en `trackPlay`) te schatten.

   >[!NOTE]
   >
   >Als u geen aangepaste metagegevens gebruikt, verzendt u gewoon een leeg object voor het `data` argument in `trackSessionStart`.

1. **Volg het feitelijke begin van het afspelen -** Identificeer de gebeurtenis vanaf de mediaspeler voor het begin van het afspelen, waar het eerste frame van de inhoud op het scherm wordt weergegeven, en roep `trackPlay`.

1. **Volg de voltooiing van het afspelen -** Identificeer de gebeurtenis van de mediaspeler voor de voltooiing van het afspelen, waar de gebruiker de inhoud tot het einde heeft bekeken, en roep `trackComplete`.

1. **Volg het einde van de sessie -** Identificeer de gebeurtenis van de mediaspeler voor het verwijderen/sluiten van het afspelen, waarbij de gebruiker de inhoud en/of de inhoud sluit en verwijderd is, en roep `trackSessionEnd`.

   >[!IMPORTANT]
   >
   >`trackSessionEnd` markeert het einde van een volgende sessie. Als de sessie is gecontroleerd op voltooiing, waarbij de gebruiker de inhoud tot het einde heeft bekeken, moet u controleren of de sessie eerder `trackComplete` is aangeroepen `trackSessionEnd`. Elke andere `track*` API-aanroep wordt na `trackSessionEnd`de gebeurtenis genegeerd, behalve `trackSessionStart` voor een nieuwe traceringssessie.

1. **Houd alle mogelijke pauzescenario&#39;s bij -** Identificeer de gebeurtenis van de media speler voor pauze en vraag `trackPause`.

   **Scenario&#39;s pauzeren -** elk scenario identificeren waarin de speler wordt gepauzeerd en ervoor zorgen dat dit correct `trackPause` wordt aangeroepen. Voor de volgende scenario&#39;s is het nodig dat uw app wordt aangeroepen `trackPause()`:

   * De gebruiker raakt expliciet de pauze in de app.
   * De speler plaatst zichzelf in de pauzestatus.
   * (*Mobiele apps*) - De gebruiker plaatst de toepassing op de achtergrond, maar u wilt dat de toepassing de sessie geopend houdt.
   * (*Mobiele apps*) - Elk type systeemonderbreking vindt plaats waardoor een toepassing op de achtergrond wordt gezet. Bijvoorbeeld, ontvangt de gebruiker een vraag, of een pop-up van een andere toepassing komt voor, maar u wilt de toepassing de zitting levend houden om de gebruiker de kans te geven om de inhoud van het punt van onderbreking te hervatten.

1. Identificeer de gebeurtenis van de speler voor spel en/of hervat van pauze en vraag `trackPlay`.

   >[!TIP]
   >
   >Dit kan de zelfde gebeurtenisbron zijn die in Stap 4 werd gebruikt. Zorg ervoor dat elke `trackPause()` API-aanroep wordt gekoppeld aan een volgende `trackPlay()` API-aanroep wanneer het afspelen wordt hervat.

1. Luister naar afspeelzoekgebeurtenissen van de mediaspeler. Bij het zoeken start-gebeurtenisbericht zoekt u naar de `SeekStart` gebeurtenis.
1. Volg bij het zoeken naar volledige meldingen van de mediaspeler het einde van het zoeken met de `SeekComplete` gebeurtenis.
1. Luister naar de buffergebeurtenissen voor het afspelen vanaf de mediaspeler en volg de buffering van de `BufferStart` gebeurtenis bij het melden van de buffergebeurtenis.
1. Volg bij het verzenden van het volledige bericht over de buffer vanuit de mediaspeler het einde van de buffering met behulp van de `BufferComplete` gebeurtenis.

Zie voorbeelden van elke stap in de volgende platformspecifieke onderwerpen, en bekijk de steekproefspelers inbegrepen met uw SDKs.

Zie dit gebruik van de JavaScript 2.x SDK in een HTML5-speler voor een eenvoudig voorbeeld van het bijhouden van afspelen:

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
if (e.type == “buffering”) { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart); 
}; 
 
/* Call on buffer complete */ 
if (e.type == “buffered”) { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete); 
};
```

## Valideren {#validate}

Zie [Validatie voor meer informatie over het valideren van uw implementatie.](/help/sdk-implement/validation/validation-overview.md)

