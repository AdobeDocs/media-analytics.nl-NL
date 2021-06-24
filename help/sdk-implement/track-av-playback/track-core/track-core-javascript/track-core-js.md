---
title: Leer hoe u het afspelen van de kern kunt bijhouden met JavaScript 2.x
description: Leer hoe u core tracking implementeert met de Media SDK in een browser met JavaScript 2.x-apps.
uuid: 3d6e0ab1-899a-43c3-b632-8276e84345ab
exl-id: d8af37a0-9048-4e6b-8cba-809386cbed5f
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 2%

---

# Muziek afspelen bijhouden met JavaScript 2.x{#track-core-playback-on-javascript}

>[!IMPORTANT]
>Deze documentatie behandelt het volgen in versie 2.x van SDK. Als u een 1.x-versie van de SDK implementeert, kunt u hier de 1.x-handleidingen voor ontwikkelaars downloaden: [SDK&#39;s downloaden](/help/sdk-implement/download-sdks.md)

1. **Eerste instelling voor bijhouden**

   Identificeer wanneer de gebruiker de bedoeling van playback teweegbrengt (de gebruiker klikt spel en/of autoplay is) en creeer een `MediaObject` instantie.

   [createMediaObject API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | Naam variabele | Beschrijving | Vereist |
   | --- | --- | :---: |
   | `name` | Mediumnaam | Ja |
   | `mediaid` | Unieke id voor media | Ja |
   | `length` | Medialengte | Ja |
   | `streamType` | Stroomtype (zie _StreamType-constanten_ hieronder) | Ja |
   | `mediaType` | Mediatype (zie _MediaType-constanten_ hieronder) | Ja |

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
   var mediaObject =  
     MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                     <MEDIA_ID,  
                                     <MEDIA_LENGTH>,
                                     MediaHeartbeat.StreamType.VOD,
                                     <MEDIA_TYPE>);
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

   Als u een mediasessie wilt volgen, roept u `trackSessionStart` op in de Media Heartmaatinstantie:

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
   >Als u geen aangepaste metagegevens gebruikt, verzendt u gewoon een leeg object voor het argument `data` in `trackSessionStart`, zoals getoond in de regel met opmerkingen in het bovenstaande iOS-voorbeeld.

1. **Het feitelijke begin van het afspelen bijhouden**

   Identificeer de gebeurtenis van de media speler voor het begin van het playback, waar het eerste kader van de media op het scherm wordt teruggegeven, en roep `trackPlay`:

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
   >`trackSessionEnd` markeert het einde van een volgende sessie. Als de sessie succesvol is gecontroleerd op voltooiing, waarbij de gebruiker de inhoud tot het einde heeft bekeken, controleert u of `trackComplete` vóór `trackSessionEnd` is aangeroepen. Eventuele andere `track*` API-aanroepen worden genegeerd na `trackSessionEnd`, behalve `trackSessionStart` voor een nieuwe traceringssessie.

1. **Houd alle mogelijke pauzescenario&#39;s bij**

   Identificeer de gebeurtenis van de media speler voor pauze en vraag `trackPause`:

   ```js
   mediaHeartbeat.trackPause();
   ```

   **Scenario&#39;s pauzeren**

   Identificeer om het even welk scenario waarin de media speler zal pauzeren en zorg ervoor dat `trackPause` behoorlijk wordt geroepen. De volgende scenario&#39;s vereisen allen dat uw app `trackPause()` roept:

   * De gebruiker raakt expliciet de pauze in de app.
   * De speler plaatst zichzelf in de pauzestatus.
   * (*Mobiele toepassingen*) - De gebruiker plaatst de toepassing op de achtergrond, maar u wilt dat de toepassing de sessie geopend houdt.
   * (*Mobiele toepassingen*) - Elk type systeem dat wordt onderbroken, zorgt ervoor dat een toepassing op de achtergrond wordt gezet. Bijvoorbeeld, ontvangt de gebruiker een vraag, of een pop-up van een andere toepassing komt voor, maar u wilt de toepassing de zitting levend houden om de gebruiker de kans te geven om de media van het punt van onderbreking te hervatten.

1. Identificeer de gebeurtenis van de speler voor spel en/of hervat van pauze en vraag `trackPlay`:

   ```js
   mediaHeartbeat.trackPlay();
   ```

   >[!TIP]
   >
   >Dit kan de zelfde gebeurtenisbron zijn die in Stap 4 werd gebruikt. Zorg ervoor dat elke `trackPause()` API vraag met de volgende `trackPlay()` API vraag wordt geparseerd wanneer de playback hervat.

* Volgscenario&#39;s: [VOD afspelen zonder advertenties](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Voorbeeldspeler die is opgenomen in de JavaScript SDK voor een volledig voorbeeld van bijhouden.
