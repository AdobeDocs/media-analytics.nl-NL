---
title: Core playback van het spoor op Chromecast
description: Dit onderwerp beschrijft hoe te om kern het volgen uit te voeren gebruikend Media SDK op Chromecast.
uuid: a9fc59d8-a2f4-4889-bdec-55c42a835d06
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Core playback van het spoor op Chromecast{#track-core-playback-on-chromecast}

>[!IMPORTANT]
>
>Deze documentatie behandelt het volgen in versie 2.x van SDK. Als u een 1.x-versie van de SDK implementeert, kunt u hier de 1.x-handleidingen voor ontwikkelaars downloaden: SDK&#39;s [downloaden](/help/sdk-implement/download-sdks.md)

1. **Eerste instelling voor bijhouden**

   Identificeer wanneer de gebruiker de bedoeling van playback teweegbrengt (de gebruiker klikt spel en/of autoplay is) en creeer een `MediaObject` geval.

   **`MediaObject`API-referentie:**

   [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

   ```
   mediaObject = ADBMobile.media.createMediaObject(<name>, <id>, <duration>, <streamType>, <mediaType>); 
   ```

   **`StreamType`constanten:**

   [ADBMobile Media](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.StreamType)

   **`MediaType`constanten:**

   [ADBMobile Media](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.MediaType)

1. **Metagegevens van video bijvoegen**

   U kunt standaard- en/of aangepaste metagegevensobjecten voor video&#39;s optioneel aan de volgende sessie koppelen via variabelen voor contextgegevens.

   * **Standaard videometagegevens**

      [Standaardmetagegevens toepassen op Chromecast](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)

      >[!NOTE]
      >
      >Het is optioneel om het standaardobject voor videometagegevens aan het mediaobject te koppelen.

   * **Aangepaste metagegevens**

      Maak een veranderlijk object voor de douanevariabelen en bevolk met de gegevens voor deze video. Bijvoorbeeld:

      ```js
      /* Set custom context data */ 
      var customVideoMetadata = { 
          isUserLoggedIn: "false", 
          tvStation: "Sample TV station", 
          programmer: "Sample programmer" 
      };
      ```

1. **Houd de intentie bij om het afspelen te starten**

   Als u een mediasessie wilt bijhouden, roept u [trackSessionStart](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionStart) op het `media` object aan.

   ```
   ADBMobile.media.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` Hiermee wordt bijgehouden wat de gebruiker wil afspelen, niet het begin van het afspelen. Deze API wordt gebruikt om de videogegevens/meta-gegevens te laden en tijd-aan-begin metrische QoS (de tijdduur tussen `trackSessionStart` en `trackPlay`) te schatten.

   >[!NOTE]
   >
   >De tweede waarde is de aangepaste objectnaam voor videometagegevens die u in stap 2 hebt gemaakt. Als u geen aangepaste videometagegevens gebruikt, verzendt u gewoon een leeg object voor het `data` argument in `trackSessionStart`, zoals in de regel met opmerkingen in het bovenstaande iOS-voorbeeld wordt getoond.

1. **Het feitelijke begin van het afspelen bijhouden**

   Identificeer de gebeurtenis van de videospeler voor het begin van de videoplayback, waar het eerste kader van de video op het scherm wordt teruggegeven, en roep [trackPlay:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPlay)

   ```
   ADBMobile.media.trackPlay();
   ```

1. **De voltooiing van het afspelen bijhouden**

   Identificeer de gebeurtenis van de videospeler voor de voltooiing van de videoplayback, waar de gebruiker de inhoud tot het eind heeft bekeken, en roep [trackComplete:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete)

   ```
   ADBMobile.media.trackComplete();
   ```

1. **Het einde van de sessie bijhouden**

   Identificeer de gebeurtenis van de videospeler voor het leegmaken/sluiten van de videoplayback, waar de gebruiker de video en/of de video voltooit en is verwijderd, en roep [trackSessionEnd:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionEnd)

   ```
   ADBMobile.media.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` markeert het einde van een videolesessie. Als de sessie is gecontroleerd op voltooiing, waarbij de gebruiker de inhoud tot het einde heeft bekeken, moet u controleren of de sessie eerder `trackComplete` is aangeroepen `trackSessionEnd`. Elke andere `track*` API-aanroep wordt na `trackSessionEnd`de gebeurtenis genegeerd, behalve `trackSessionStart` voor een nieuwe sessie voor het bijhouden van video.

1. **Houd alle mogelijke pauzescenario&#39;s bij**

   Identificeer de gebeurtenis van de videospeler voor videopauze en roep [trackPause:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPause)

   ```
   ADBMobile.media.trackPause();
   ```

   **Scenario&#39;s pauzeren**

   Identificeer om het even welk scenario waarin de Videospeler zal pauzeren en ervoor zorgen dat dat behoorlijk wordt geroepen. `trackPause` Voor de volgende scenario&#39;s is het nodig dat uw app wordt aangeroepen `trackPause()`:

   * De gebruiker raakt expliciet de pauze in de app.
   * De speler plaatst zichzelf in de pauzestatus.
   * (*Mobiele apps*) - De gebruiker plaatst de toepassing op de achtergrond, maar u wilt dat de toepassing de sessie geopend houdt.
   * (*Mobiele apps*) - Elk type systeemonderbreking vindt plaats waardoor een toepassing op de achtergrond wordt gezet. Bijvoorbeeld, ontvangt de gebruiker een vraag, of een pop-up van een andere toepassing komt voor, maar u wilt de toepassing de zitting levend houden om de gebruiker de kans te geven om de video van het punt van onderbreking te hervatten.

1. Identificeer de gebeurtenis van de speler voor videospel en/of video hervat van pauze en roep [trackPlay:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete)

   ```
   ADBMobile.media.trackPlay();
   ```

   >[!TIP]
   >
   >Dit kan de zelfde gebeurtenisbron zijn die in Stap 4 werd gebruikt. Zorg ervoor dat elke `trackPause()` API-aanroep wordt gekoppeld aan een volgende `trackPlay()` API-aanroep wanneer het afspelen van de video wordt hervat.

* Volgscenario&#39;s: [VOD afspelen zonder advertenties](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Voorbeeldspeler die is opgenomen in de Chromecast SDK voor een volledig voorbeeld van bijhouden.

