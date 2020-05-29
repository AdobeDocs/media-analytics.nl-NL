---
title: Muziek afspelen bijhouden op Roku
description: Dit onderwerp beschrijft hoe te om kern het volgen uit te voeren gebruikend Media SDK op Roku.
uuid: a8aa7b3c-2d39-44d7-8ebc-b101d130101f
translation-type: tm+mt
source-git-commit: 815965d1cd41e73e50666a89f4a7c450af5022da
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 2%

---


# Track core playback on Roku{#track-core-playback-on-roku}

>[!IMPORTANT]
>Deze documentatie behandelt het volgen in versie 2.x van SDK. Als u een 1.x-versie van de SDK implementeert, kunt u hier de 1.x-handleidingen voor ontwikkelaars downloaden: [SDK&#39;s downloaden](/help/sdk-implement/download-sdks.md)

1. **Eerste instelling voor bijhouden**

   Identificeer wanneer de gebruiker de bedoeling van playback teweegbrengt (de gebruiker klikt spel en/of autoplay is) en creeer een `MediaObject` geval.

   **`MediaObject`referentie:**

   | Naam variabele | Beschrijving | Vereist |
   | --- | --- | :---: |
   | `name` | Videonaam | Ja |
   | `mediaid` | Unieke videoid | Ja |
   | `length` | Videolengte | Ja |
   | `streamType` | Stroomtype (zie _StreamType-constanten_ hieronder) | Ja |
   | `mediaType` | Media type (see _MediaType constants_ below) | Ja |

   **`StreamType`constanten:**

   | Naam van constante | Beschrijving   |
   |---|---|
   | `MEDIA_STREAM_TYPE_VOD` | Het type van stroom voor Video op bestelling. |
   | `MEDIA_STREAM_TYPE_LIVE` | Stroomtype voor LIVE-inhoud. |
   | `MEDIA_STREAM_TYPE_LINEAR` | Het type van stroom voor inhoud LINEAR. |
   | `MEDIA_STREAM_TYPE_AOD` | Stroomtype voor audio op aanvraag |
   | `MEDIA_STREAM_TYPE_AUDIOBOOK` | Streaming type voor audioboek |
   | `MEDIA_STREAM_TYPE_PODCAST` | Stroomtype voor Podcast |

   **`MediaType`constanten:**

   | Naam van constante | Beschrijving |
   |---|---|
   | `MEDIA_STREAM_TYPE_AUDIO` | Mediatype voor audiostreams. |
   | `MEDIA_STREAM_TYPE_VIDEO` | Mediatype voor videostreams. |

   **Maak een Media Info-object voor video met VOD-inhoud:**

   ```
    mediaInfo = adb_media_init_mediainfo(
     "<MEDIA_NAME>",
     "<MEDIA_ID>",
     600,
     ADBMobile().MEDIA_STREAM_TYPE_VOD,
     ADBMobile().MEDIA_TYPE_VIDEO
   )
   ```

   of

   ```
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.name = "<MEDIA_NAME>"
   mediaInfo.id = "<MEDIA_ID>"
   mediaInfo.length = 600
   mediaInfo.streamType = ADBMobile().MEDIA_STREAM_TYPE_VOD
   mediaInfo.mediaType = ADBMobile().MEDIA_TYPE_VIDEO
   ```

   **Een Media Info-object maken voor video met AOD-inhoud:**

   ```
   mediaInfo = adb_media_init_mediainfo(
    "<MEDIA_NAME>",
    "<MEDIA_ID>",
    600,
    ADBMobile().MEDIA_STREAM_TYPE_AOD,
    ADBMobile().MEDIA_TYPE_AUDIO
   )
   ```

   of

   ```
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.name = "<MEDIA_NAME>"
   mediaInfo.id = "<MEDIA_ID>"
   mediaInfo.length = 600
   mediaInfo.streamType = ADBMobile().MEDIA_STREAM_TYPE_AOD
   mediaInfo.mediaType = ADBMobile().MEDIA_TYPE_AUDIO
   ```

1. **Metagegevens koppelen**

   Koppel standaard- en/of aangepaste metagegevensobjecten optioneel aan de volgende sessie via de variabelen van de contextgegevens.

   * **Standaardmetagegevens**

      [Standaardmetadata implementeren in JavaScript](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)

      >[!NOTE]
      >
      >Het koppelen van het standaardobject voor metagegevens aan het mediaobject is optioneel.

      * API-naslaggids voor metagegevens van media - [Standaardmetagegevenstoetsen - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

         Hier vindt u de uitgebreide set met beschikbare metagegevens: [Parameters voor audio en video](/help/metrics-and-metadata/audio-video-parameters.md)
   * **Aangepaste metagegevens**

      Maak een veranderlijk object voor de douanevariabelen en bevolk met de gegevens voor deze media. Bijvoorbeeld:

      ```js
      /* Set custom context data */
      var customVideoMetadata = {
          isUserLoggedIn: "false",
          tvStation: "Sample TV station",
          programmer: "Sample programmer"
      };
      ```


1. **Houd de intentie bij om het afspelen te starten**

   Als u een mediasessie wilt volgen, roept u `trackSessionStart` de Media Heartmaatinstantie aan:

   ```js
   mediaHeartbeat.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!TIP]
   >
   >De tweede waarde is de objectnaam voor aangepaste mediametagegevens die u in stap 2 hebt gemaakt.

   >[!IMPORTANT]
   >
   >`trackSessionStart` Hiermee wordt bijgehouden wat de gebruiker wil afspelen, niet het begin van het afspelen. Deze API wordt gebruikt om de gegevens/meta-gegevens te laden en tijd-aan-begin metrische QoS (de tijdduur tussen `trackSessionStart` en `trackPlay`) te schatten.

   >[!NOTE]
   >
   >Als u geen aangepaste metagegevens gebruikt, verzendt u gewoon een leeg object voor het `data` argument in `trackSessionStart`, zoals in de regel met opmerkingen in het bovenstaande iOS-voorbeeld wordt getoond.

1. **Het feitelijke begin van het afspelen bijhouden**

   Identificeer de gebeurtenis van de mediaspeler voor het begin van het afspelen, waar het eerste frame van de media op het scherm wordt weergegeven, en roep `trackPlay`:

   ```js
   mediaHeartbeat.trackPlay();
   ```

1. **De voltooiing van het afspelen bijhouden**

   Identificeer de gebeurtenis van de media speler voor de voltooiing van het playback, waar de gebruiker de inhoud tot het eind heeft bekeken, en roep `trackComplete`:

   ```js
   mediaHeartbeat.trackComplete();
   ```

1. **Het einde van de sessie bijhouden**

   Identificeer de gebeurtenis van de mediaspeler voor het verwijderen/sluiten van het afspelen, waar de gebruiker de media en/of de media sluit en verwijderd is, en roep `trackSessionEnd`:

   ```js
   mediaHeartbeat.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >Een `trackSessionEnd` teken het einde van een volgende sessie. Als de sessie is gecontroleerd op voltooiing, waarbij de gebruiker de inhoud tot het einde heeft bekeken, moet u controleren of de sessie eerder `trackComplete` is aangeroepen `trackSessionEnd`. Elke andere `track*` API-aanroep wordt na `trackSessionEnd`de gebeurtenis genegeerd, behalve `trackSessionStart` voor een nieuwe traceringssessie.  Methode voor het bijhouden van het afspelen van media om het laden van de media te volgen en de huidige sessie in te stellen op actief:

   ```
   ‘ Create a media info object
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.id = <MEDIA_ID>
   mediaInfo.playhead = "0"
   mediaInfo.length = "600"
   ```

1. **Metagegevens van video bijvoegen**

   U kunt standaard- en/of aangepaste metagegevensobjecten voor video&#39;s optioneel aan de volgende sessie koppelen via variabelen voor contextgegevens.

   * **Standaard videometagegevens**

      [Standaardmetadata implementeren in Roku](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)

      >[!NOTE]
      >Het is optioneel om het standaardobject voor videometagegevens aan het mediaobject te koppelen.

   * **Aangepaste metagegevens**

      Maak een veranderlijk object voor de douanevariabelen en bevolk met de gegevens voor deze video. Bijvoorbeeld:

      ```
      mediaContextData = {}
      mediaContextData["cmk1"] = "cmv1"
      mediaContextData["cmk2"] = "cmv2"
      ```

1. **Houd de intentie bij om het afspelen te starten**

   Als u een mediasessie wilt volgen, roept u `trackSessionStart` de Media Heartmaatinstantie aan:

   ```
   ADBMobile().mediaTrackSessionStart(mediaInfo,mediaContextData)
   ```

   >[!TIP]
   >De tweede waarde is de aangepaste objectnaam voor videometagegevens die u in stap 2 hebt gemaakt.

   >[!IMPORTANT]
   >`trackSessionStart` Hiermee wordt bijgehouden wat de gebruiker wil afspelen, niet het begin van het afspelen. Deze API wordt gebruikt om de videogegevens/meta-gegevens te laden en tijd-aan-begin metrische QoS (de tijdduur tussen `trackSessionStart` en `trackPlay`) te schatten.

   >[!NOTE]
   >Als u geen aangepaste videometagegevens gebruikt, verzendt u gewoon een leeg object voor het `data` argument in `trackSessionStart`, zoals in de regel met opmerkingen in het bovenstaande iOS-voorbeeld wordt getoond.

1. **Het feitelijke begin van het afspelen bijhouden**

   Identificeer de gebeurtenis van de videospeler voor het begin van de videoplayback, waar het eerste kader van de video op het scherm wordt teruggegeven, en roep `trackPlay`:

   ```
   ADBMobile().mediaTrackPlay()
   ```

1. **De voltooiing van het afspelen bijhouden**

   Identificeer de gebeurtenis van de videospeler voor de voltooiing van de videoplayback, waar de gebruiker de inhoud tot het eind heeft bekeken, en roep `trackComplete`:

   ```
   ADBMobile().mediaTrackComplete()
   ```

1. **Het einde van de sessie bijhouden**

   Identificeer de gebeurtenis van de videospeler voor het leegmaken/sluiten van de videoplayback, waar de gebruiker de video en/of video voltooit en is verwijderd, en roep `trackSessionEnd`:

   ```
   ADBMobile().mediaTrackSessionEnd()
   ```

   >[!IMPORTANT]
   >`trackSessionEnd` markeert het einde van een videolesessie. Als de sessie is gecontroleerd op voltooiing, waarbij de gebruiker de inhoud tot het einde heeft bekeken, moet u controleren of de sessie eerder `trackComplete` is aangeroepen `trackSessionEnd`. Elke andere `track*` API-aanroep wordt na `trackSessionEnd`de gebeurtenis genegeerd, behalve `trackSessionStart` voor een nieuwe sessie voor het bijhouden van video.

1. **Houd alle mogelijke pauzescenario&#39;s bij**

   Identificeer de gebeurtenis van de videospeler voor videopauze en vraag `trackPause`:

   ```
   ADBMobile().mediaTrackPause()
   ```

   **Scenario&#39;s pauzeren**

   Identificeer om het even welk scenario waarin de Videospeler zal pauzeren en ervoor zorgen dat dat behoorlijk wordt geroepen. `trackPause` Voor de volgende scenario&#39;s is het nodig dat uw app wordt aangeroepen `trackPause()`:

   * De gebruiker raakt expliciet de pauze in de app.
   * De speler plaatst zichzelf in de pauzestatus.
   * (*Mobiele apps*) - De gebruiker plaatst de toepassing op de achtergrond, maar u wilt dat de toepassing de sessie geopend houdt.
   * (*Mobiele apps*) - Elk type systeemonderbreking vindt plaats waardoor een toepassing op de achtergrond wordt gezet. Bijvoorbeeld, ontvangt de gebruiker een vraag, of een pop-up van een andere toepassing komt voor, maar u wilt de toepassing de zitting levend houden om de gebruiker de kans te geven om de video van het punt van onderbreking te hervatten.

1. Identificeer de gebeurtenis van de speler voor videospel en/of video hervat van pauze en vraag `trackPlay`:

   ```
   ADBMobile().mediaTrackPlay()
   ```

   >[!TIP]
   >Dit kan de zelfde gebeurtenisbron zijn die in Stap 4 werd gebruikt. Zorg ervoor dat elke `trackPause()` API-aanroep wordt gekoppeld aan een volgende `trackPlay()` API-aanroep wanneer het afspelen van de video wordt hervat.

* Volgscenario&#39;s: [VOD afspelen zonder advertenties](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Voorbeeldspeler die is opgenomen in de SDK van Roku voor een volledig voorbeeld van bijhouden.
