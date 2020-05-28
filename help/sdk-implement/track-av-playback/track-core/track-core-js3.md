---
title: Muziekweergave bijhouden met JavaScript v3.x
description: In dit onderwerp wordt beschreven hoe u het bijhouden van kernelementen implementeert met de SDK van Media in een browser met JavaScript 3.x-apps.
translation-type: tm+mt
source-git-commit: 6c672bdf71a817f18cc2ca7ac76a17f8c4c93d4b
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 0%

---


# Muziek afspelen bijhouden met JavaScript 3.x{#track-core-playback-on-javascript}

>[!IMPORTANT]
>Deze documentatie behandelt het volgen in versie 3.x van SDK. Als u eerdere versies van de SDK implementeert, kunt u de ontwikkelaarsgidsen hier downloaden: [SDK&#39;s downloaden](/help/sdk-implement/download-sdks.md)

1. **Eerste instelling voor bijhouden**

   Identificeer wanneer de gebruiker de bedoeling van playback teweegbrengt (de gebruiker klikt spel en/of autoplay is) en creeer een `MediaObject` geval.

   [createMediaObject API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | Naam variabele | Type | Beschrijving |
   | --- | --- | --- |
   | `name` | string | Niet-lege tekenreeks die de medianaam aangeeft. |
   | `id` | string | Niet-lege tekenreeks die unieke media-id aangeeft. |
   | `length` | getal | Positief getal dat de lengte van het medium in seconden aangeeft. Gebruik 0 als de lengte onbekend is. |
   | `streamType` | string | [Stroomtype](koppeling naar streamType-constanten) of niet-lege tekenreeks om het type mediastream aan te duiden. |
   | `mediaType` | [MediaType](koppeling naar MediaType-constanten) | Type media (audio of video). |

   **`StreamType`constanten:**

   | Naam van constante | Beschrijving   |
   |---|---|
   | `VOD` | Het type van stroom voor Video op bestelling. |
   | `LIVE` | Stroomtype voor LIVE-inhoud. |
   | `LINEAR` | Het type van stroom voor inhoud LINEAR. |
   | `AOD` | Het type van stroom voor Audio op bestelling. |
   | `AUDIOBOOK` | Streaming type voor audioboek. |
   | `PODCAST` | Het type van stroom voor Podcast. |

   **`MediaType`constanten:**

   | Naam van constante | Beschrijving |
   |---|---|
   | `Audio` | Mediatype voor audiostreams. |
   | `Video` | Mediatype voor videostreams. |

   ```
   var mediaObject = ADB.Media.createMediaObject(<MEDIA_NAME>,
                                     <MEDIA_ID,
                                     <MEDIA_LENGTH>,
                                     <STREAM_TYPE>,
                                     <MEDIA_TYPE>);
   ```

1. **Metagegevens koppelen**

   Voeg desgewenst standaard- en/of aangepaste metagegevens toe aan de volgende sessie via de variabelen van de contextgegevens.

   * **Standaardmetagegevens**

      >[!NOTE]
      >
      >Het koppelen van de standaardmetagegevens is optioneel.

      * API-naslaggids voor metagegevens van media - [Standaardmetagegevenstoetsen - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

         Hier vindt u de uitgebreide set met beschikbare metagegevens: [Parameters voor audio en video](/help/metrics-and-metadata/audio-video-parameters.md)
   * **Aangepaste metagegevens**

      Maak een veranderlijk object voor de douanevariabelen en bevolk met de gegevens voor deze media. Bijvoorbeeld:

      ```js
      /* Set context data */
       var contextData = {};
      
       //Standard metadata
       contextData[ADB.Media.VideoMetadataKeys.EPISODE] = "Sample Episode";
       contextData[ADB.Media.VideoMetadataKeys.SHOW] = "Sample Show";
      
       //Custom metadata
       contextData["isUserLoggedIn"] = "false";
       contextData["tvStation"] = "Sample TV Station";
      ```


1. **Houd de intentie bij om het afspelen te starten**

   Als u een mediasessie wilt volgen, roept u `trackSessionStart` de Media Heartmaatinstantie aan:

   ```js
   var mediaObject = ADB.Media.createMediaObject("video-name",
                                                 "video-id",
                                                 60.0,
                                                 ADB.Media.StreamType.VOD,
                                                 ADB.Media.MediaType.Video);
   
   var contextData = {};
   
   //Standard metadata
   contextData[ADB.Media.VideoMetadataKeys.EPISODE] = "Sample Episode";
   contextData[ADB.Media.VideoMetadataKeys.SHOW] = "Sample Show";
   
   //Custom metadata
   contextData["isUserLoggedIn"] = "false";
   contextData["tvStation"] = "Sample TV Station";
   
   tracker.trackSessionStart(mediaObject, contextData);
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` Hiermee wordt bijgehouden wat de gebruiker wil afspelen, niet het begin van het afspelen. Deze API wordt gebruikt om de gegevens/meta-gegevens te laden en tijd-aan-begin metrische QoS (de tijdduur tussen `trackSessionStart` en `trackPlay`) te schatten.

   >[!NOTE]
   >
   >Als u contextData niet gebruikt, verzendt u gewoon een leeg object voor het `data` argument in `trackSessionStart`.

1. **Het feitelijke begin van het afspelen bijhouden**

   Identificeer de gebeurtenis van de mediaspeler voor het begin van het afspelen, waar het eerste frame van de media op het scherm wordt weergegeven, en roep `trackPlay`:

   ```js
   tracker.trackPlay();
   ```

1. **De voltooiing van het afspelen bijhouden**

   Identificeer de gebeurtenis van de media speler voor de voltooiing van het playback, waar de gebruiker de inhoud tot het eind heeft bekeken, en roep `trackComplete`:

   ```js
   tracker.trackComplete();
   ```

1. **Het einde van de sessie bijhouden**

   Identificeer de gebeurtenis van de mediaspeler voor het verwijderen/sluiten van het afspelen, waar de gebruiker de media en/of de media sluit en verwijderd is, en roep `trackSessionEnd`:

   ```js
   tracker.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` markeert het einde van een volgende sessie. Als de sessie is gecontroleerd op voltooiing, waarbij de gebruiker de inhoud tot het einde heeft bekeken, moet u controleren of de sessie eerder `trackComplete` is aangeroepen `trackSessionEnd`. Elke andere `track*` API-aanroep wordt na `trackSessionEnd`de gebeurtenis genegeerd, behalve `trackSessionStart` voor een nieuwe traceringssessie.

1. **Houd alle mogelijke pauzescenario&#39;s bij**

   Identificeer de gebeurtenis van de media speler voor pauze en vraag `trackPause`:

   ```js
   tracker.trackPause();
   ```

   **Scenario&#39;s pauzeren**

   Identificeer om het even welk scenario waarin de media speler zal pauzeren en ervoor zorgen dat dat behoorlijk geroepen `trackPause` is. Voor de volgende scenario&#39;s is het nodig dat uw app wordt aangeroepen `trackPause()`:

   * De gebruiker raakt expliciet de pauze in de app.
   * De speler plaatst zichzelf in de pauzestatus.
   * (*Mobiele apps*) - De gebruiker plaatst de toepassing op de achtergrond, maar u wilt dat de toepassing de sessie geopend houdt.
   * (*Mobiele apps*) - Elk type systeemonderbreking vindt plaats waardoor een toepassing op de achtergrond wordt gezet. Bijvoorbeeld, ontvangt de gebruiker een vraag, of een pop-up van een andere toepassing komt voor, maar u wilt de toepassing de zitting levend houden om de gebruiker de kans te geven om de media van het punt van onderbreking te hervatten.

1. Identificeer de gebeurtenis van de speler voor spel en/of hervat van pauze en vraag `trackPlay`:

   ```js
   tracker.trackPlay();
   ```

   >[!TIP]
   >
   >Dit kan de zelfde gebeurtenisbron zijn die in Stap 4 werd gebruikt. Zorg ervoor dat elke `trackPause()` API-aanroep wordt gekoppeld aan een volgende `trackPlay()` API-aanroep wanneer het afspelen wordt hervat.

* Volgscenario&#39;s: [VOD afspelen zonder advertenties](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Voorbeeldspeler die is opgenomen in de JavaScript SDK voor een volledig voorbeeld van bijhouden.
