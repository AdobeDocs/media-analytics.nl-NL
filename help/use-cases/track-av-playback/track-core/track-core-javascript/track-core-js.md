---
title: Leer hoe u het afspelen van de kern kunt bijhouden met JavaScript 2.x
description: Leer hoe u core tracking implementeert met de Media SDK in een browser met JavaScript 2.x-apps.
uuid: 3d6e0ab1-899a-43c3-b632-8276e84345ab
exl-id: d8af37a0-9048-4e6b-8cba-809386cbed5f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 2%

---

# Muziek afspelen bijhouden met JavaScript 2.x{#track-core-playback-on-javascript}

De volgende instructies bieden richtlijnen voor implementatie in 2.x SDK&#39;s.

>[!IMPORTANT]
>Als u een 1.x-versie van de SDK implementeert, kunt u hier de 1.x-handleidingen voor ontwikkelaars downloaden: [SDK&#39;s downloaden](/help/getting-started/download-sdks.md)

1. **Eerste instelling voor bijhouden**

   Identificeer wanneer de gebruiker de bedoeling van playback teweegbrengt (de gebruiker klikt spel en/of autoplay is) en creeer een `MediaObject` -instantie.

   [createMediaObject API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | Naam variabele | Beschrijving | Vereist |
   | --- | --- | :---: |
   | `name` | Mediumnaam | Ja |
   | `mediaid` | Unieke id voor media | Ja |
   | `length` | Medialengte | Ja |
   | `streamType` | Type stream (zie _StreamType-constanten_ hieronder) | Ja |
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

      [Standaardmetadata implementeren in JavaScript](/help/use-cases/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)

      >[!NOTE]
      >
      >Het koppelen van het standaardobject voor metagegevens aan het mediaobject is optioneel.

      * API-naslaggids voor metagegevens van media - [Standaardmetagegevenstoetsen - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

         Hier vindt u de uitgebreide set met beschikbare metagegevens: [Parameters voor audio en video](/help/implementation/variables/audio-video-parameters.md)
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

   Als u een mediasessie wilt bijhouden, roept u `trackSessionStart` op de Media Heartbone-instantie:

   ```js
   mediaHeartbeat.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!TIP]
   >
   >De tweede waarde is de objectnaam voor aangepaste mediametagegevens die u in stap 2 hebt gemaakt.

   >[!IMPORTANT]
   >
   >`trackSessionStart` Hiermee wordt bijgehouden wat de gebruiker wil afspelen, niet het begin van het afspelen. Deze API wordt gebruikt om de gegevens/meta-gegevens te laden en tijd-aan-begin metrische QoS (de tijdsduur tussen `trackSessionStart` en `trackPlay`).

   >[!NOTE]
   >
   >Als u geen aangepaste metagegevens gebruikt, kunt u gewoon een leeg object verzenden voor de `data` argument in `trackSessionStart`, zoals getoond in de commentaarlijn in het iOS voorbeeld hierboven.

1. **Het feitelijke begin van het afspelen bijhouden**

   Identificeer de gebeurtenis van de media speler voor het begin van het playback, waar het eerste kader van de media op het scherm wordt teruggegeven, en vraag `trackPlay`:

   ```js
   mediaHeartbeat.trackPlay();
   ```

1. **De voltooiing van het afspelen bijhouden**

   Identificeer de gebeurtenis van de media speler voor de voltooiing van het playback, waar de gebruiker de inhoud tot het eind heeft bekeken, en vraag `trackComplete`:

   ```js
   mediaHeartbeat.trackComplete();
   ```

1. **Het einde van de sessie bijhouden**

   Identificeer de gebeurtenis van de media speler voor het leegmaken/sluiten van het playback, waar de gebruiker de media en/of de media sluit wordt voltooid en is leeggemaakt, en vraag `trackSessionEnd`:

   ```js
   mediaHeartbeat.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` markeert het einde van een volgende sessie. Als de sessie succesvol is gecontroleerd naar voltooiing, waarbij de gebruiker de inhoud tot het einde heeft bekeken, zorgt u ervoor dat `trackComplete` wordt eerder aangeroepen `trackSessionEnd`. andere `track*` API-aanroep wordt genegeerd na `trackSessionEnd`, met uitzondering van `trackSessionStart` voor een nieuwe traceringssessie.

1. **Houd alle mogelijke pauzescenario&#39;s bij**

   Identificeer de gebeurtenis van de media speler voor pauze en vraag `trackPause`:

   ```js
   mediaHeartbeat.trackPause();
   ```

   **Scenario&#39;s pauzeren**

   Identificeer om het even welk scenario waarin de media speler zal pauzeren en zorg ervoor dat `trackPause` wordt correct geroepen. De volgende scenario&#39;s vereisen allemaal dat uw app wordt aangeroepen `trackPause()`:

   * De gebruiker raakt expliciet de pauze in de app.
   * De speler plaatst zichzelf in de pauzestatus.
   * (*Mobiele apps*) - De gebruiker plaatst de toepassing op de achtergrond, maar u wilt dat de toepassing de sessie geopend houdt.
   * (*Mobiele apps*) - Elk type onderbreking van het systeem treedt op waardoor een toepassing achteraan wordt geplaatst. Bijvoorbeeld, ontvangt de gebruiker een vraag, of een pop-up van een andere toepassing komt voor, maar u wilt de toepassing de zitting levend houden om de gebruiker de kans te geven om de media van het punt van onderbreking te hervatten.

1. De gebeurtenis van de speler identificeren voor afspelen en/of hervatten vanuit pauzeren en aanroepen `trackPlay`:

   ```js
   mediaHeartbeat.trackPlay();
   ```

   >[!TIP]
   >
   >Dit kan de zelfde gebeurtenisbron zijn die in Stap 4 werd gebruikt. Zorg ervoor dat elk `trackPause()` API-aanroep is gekoppeld aan het volgende `trackPlay()` API-aanroep wanneer het afspelen wordt hervat.

* Volgscenario&#39;s: [VOD afspelen zonder advertenties](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* Voorbeeldspeler die is opgenomen in de JavaScript SDK voor een volledig voorbeeld van bijhouden.
