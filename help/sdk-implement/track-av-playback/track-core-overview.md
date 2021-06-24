---
title: Afspelen van bijgehouden inhoud beschreven
description: '"Meer informatie over het bijhouden van het afspelen van de kern, zoals het laden van de media, het starten van de media, het pauzeren van de media en het voltooien van de media. "'
uuid: 7b8e2f76-bc4e-4721-8933-3e4453b01788
exl-id: 98ad2783-c9e3-48de-88df-8549f26114a0
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 0%

---

# Overzicht van bijhouden{#tracking-overview}

>[!IMPORTANT]
>
>Deze documentatie behandelt het volgen in versie 2.x van SDK. Als u een 1.x-versie van de SDK implementeert, kunt u hier de 1.x-handleidingen voor ontwikkelaars downloaden: [SDK&#39;s downloaden.](/help/sdk-implement/download-sdks.md)

## Player Events

Tot het bijhouden van het afspelen van de kern behoren het bijhouden van het laden van media, het starten van media, het pauzeren van media en het voltooien van media. Hoewel dit niet verplicht is, vormen het bijhouden van buffering en zoeken ook kerncomponenten die worden gebruikt voor het bijhouden van het afspelen van inhoud. In uw media speler API, identificeer de spelergebeurtenissen die met de het volgen vraag van SDK van Media beantwoorden, en codeer uw gebeurtenismanagers om het volgen APIs te roepen, en vereiste en facultatieve variabelen te bevolken.

### Bij laden van media

* Het mediaobject maken
* Metagegevens vullen
* `trackSessionStart` aanroepen; Bijvoorbeeld: `trackSessionStart(mediaObject, contextData)`

### Bij starten van media

* `trackPlay` aanroepen

### Bij pauzeren/hervatten

* `trackPause` aanroepen
* `trackPlay` aanroepen   _wanneer het afspelen wordt hervat_

### Op media voltooid

* `trackComplete` aanroepen

### Bij afbreken van media

* `trackSessionEnd` aanroepen

### Bij starten van scrubben

* `trackEvent(SeekStart)` aanroepen

### Als scrubben eindigt

* `trackEvent(SeekComplete)` aanroepen

### Wanneer de buffering wordt gestart

* `trackEvent(BufferStart);` aanroepen

### Wanneer het bufferen eindigt

* `trackEvent(BufferComplete);` aanroepen

>[!TIP]
>
>De positie van de afspeelkop wordt ingesteld als onderdeel van de instellings- en configuratiecode. Voor meer informatie over `getCurrentPlayheadTime`, zie [Overzicht: Algemene implementatierichtlijnen.](/help/sdk-implement/setup/setup-overview.md#general-implementation-guidelines)

## Implementeren {#implement}

1. **Initiële instelling voor bijhouden -** Identificeren wanneer de gebruiker de afspeelintentie activeert (de gebruiker klikt op Afspelen en/of Automatisch afspelen is ingeschakeld) en een  `MediaObject` instantie maken met de mediagegevens voor de naam van de inhoud, de inhoud-id, de lengte van de inhoud en het stroomtype.

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

   De algemene notatie voor het maken van de `MediaObject` is `MediaHeartbeat.createMediaObject(<MEDIA_NAME>, <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);`

1. **Metagegevens koppelen -** Optioneel standaard- en/of aangepaste metagegevensobjecten aan de volgende sessie koppelen met gebruik van contextgegevensvariabelen.

   * **Standaardmetagegevens -**

      >[!NOTE]
      >
      >Het koppelen van het standaardobject voor metagegevens aan het mediaobject is optioneel.

      Instantiëren van een standaard metagegevensobject, vullen van de gewenste variabelen en stellen het metagegevensobject in op het Media Heartbone-object.

      Zie de uitgebreide lijst met metagegevens hier: [Parameters voor audio en video.](/help/metrics-and-metadata/audio-video-parameters.md)

   * **Aangepaste metagegevens -** Maak een variabelenobject voor de aangepaste variabelen en vul de gegevens voor deze inhoud in.

1. **Houd de intentie bij om het afspelen te starten -** Als u een sessie wilt volgen, roept u  `trackSessionStart` de Media Heartbeat-instantie aan.

   >[!IMPORTANT]
   >
   >`trackSessionStart` Hiermee wordt bijgehouden wat de gebruiker wil afspelen, niet het begin van het afspelen. Deze API wordt gebruikt om de gegevens/meta-gegevens te laden en tijd-aan-begin metrische QoS (de tijdduur tussen `trackSessionStart` en `trackPlay`) te schatten.

   >[!NOTE]
   >
   >Als u geen douanemetagegevens gebruikt, verzend eenvoudig een leeg voorwerp voor het `data` argument in `trackSessionStart`.

1. **Traceer het daadwerkelijke begin van playback -** identificeer de gebeurtenis van de media speler voor het begin van het playback, waar het eerste kader van de inhoud op het scherm wordt teruggegeven, en vraag  `trackPlay`.

1. **Volg de voltooiing van het afspelen -** Identificeer de gebeurtenis van de mediaspeler voor het afspelen, waar de gebruiker de inhoud tot het einde heeft bekeken, en roep  `trackComplete`.

1. **Volg het einde van de sessie -** Identificeer de gebeurtenis van de mediaspeler voor het verwijderen/sluiten van het afspelen, waarbij de gebruiker de inhoud en/of de inhoud sluit en verwijderd is, en roep  `trackSessionEnd`.

   >[!IMPORTANT]
   >
   >`trackSessionEnd` markeert het einde van een volgende sessie. Als de sessie succesvol is gecontroleerd op voltooiing, waarbij de gebruiker de inhoud tot het einde heeft bekeken, controleert u of `trackComplete` vóór `trackSessionEnd` is aangeroepen. Eventuele andere `track*` API-aanroepen worden genegeerd na `trackSessionEnd`, behalve `trackSessionStart` voor een nieuwe traceringssessie.

1. **Houd alle mogelijke pauzescenario&#39;s bij -** Identificeer de gebeurtenis van de media speler voor pauze en vraag  `trackPause`.

   **Scenario&#39;s pauzeren -** Identificeer om het even welk scenario waarin de Speler zal pauzeren en ervoor zorgen dat dat behoorlijk  `trackPause` wordt geroepen. De volgende scenario&#39;s vereisen allen dat uw app `trackPause()` roept:

   * De gebruiker raakt expliciet de pauze in de app.
   * De speler plaatst zichzelf in de pauzestatus.
   * (*Mobiele toepassingen*) - De gebruiker plaatst de toepassing op de achtergrond, maar u wilt dat de toepassing de sessie geopend houdt.
   * (*Mobiele toepassingen*) - Elk type systeem dat wordt onderbroken, zorgt ervoor dat een toepassing op de achtergrond wordt gezet. Bijvoorbeeld, ontvangt de gebruiker een vraag, of een pop-up van een andere toepassing komt voor, maar u wilt de toepassing de zitting levend houden om de gebruiker de kans te geven om de inhoud van het punt van onderbreking te hervatten.

1. Identificeer de gebeurtenis van de speler voor spel en/of hervat van pauze en vraag `trackPlay`.

   >[!TIP]
   >
   >Dit kan de zelfde gebeurtenisbron zijn die in Stap 4 werd gebruikt. Zorg ervoor dat elke `trackPause()` API vraag met de volgende `trackPlay()` API vraag wordt geparseerd wanneer de playback hervat.

1. Luister naar afspeelzoekgebeurtenissen van de mediaspeler. Bij het zoeken start-gebeurtenisbericht zoekt u naar de gebeurtenis `SeekStart`.
1. Volg bij het zoeken naar volledige meldingen van de mediaspeler het einde van het zoeken met de gebeurtenis `SeekComplete`.
1. Luister naar de afspeelbuffergebeurtenissen van de mediaspeler en volg bij de melding van de gebeurtenis buffering van de buffer de buffering met de gebeurtenis `BufferStart`.
1. Volg bij het verzenden van het volledige bericht over de buffer vanuit de mediaspeler het einde van de buffering met de gebeurtenis `BufferComplete`.

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

Voor informatie bij het bevestigen van uw implementatie, zie [Bevestiging.](/help/sdk-implement/validation/validation-overview.md)
