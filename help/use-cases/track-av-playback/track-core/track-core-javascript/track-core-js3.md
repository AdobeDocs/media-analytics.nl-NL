---
title: Leer hoe u het afspelen van de kern kunt bijhouden met JavaScript v3.x
description: Leer hoe u core tracking implementeert met de Media SDK in een browser met JavaScript 3.x-apps.
exl-id: f3145450-82ba-4790-91a4-9d2cc97bbaa5
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 0%

---

# Core playback volgen met JavaScript 3.x{#track-core-playback-on-javascript}

Deze documentatie behandelt het bijhouden van wijzigingen in versie 3.x van de SDK.

>[!IMPORTANT]
>
>Als u om het even welke vorige versies van SDK uitvoert, kunt u de Gidsen van Ontwikkelaars hier downloaden: [ Download SDKs ](/help/getting-started/download-sdks.md)

1. **Aanvankelijke het volgen opstelling**

   Bepaal wanneer de gebruiker de afspeelintentie activeert (de gebruiker klikt op Afspelen en/of Automatisch afspelen is ingeschakeld) en maak een `MediaObject` -instantie.

   [ createMediaObject API ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | Naam variabele | Type | Beschrijving |
   | --- | --- | --- |
   | `name` | string | Niet-lege tekenreeks die de medianaam aangeeft. |
   | `id` | string | Niet-lege tekenreeks die unieke media-id aangeeft. |
   | `length` | getal | Positief getal dat de lengte van het medium in seconden aangeeft. Gebruik 0 als de lengte onbekend is. |
   | `streamType` | string |   |
   | `mediaType` | | Type media (audio of video). |

   **`StreamType`constanten:**

   | Naam van constante | Beschrijving   |
   |---|---|
   | `VOD` | Het type van stroom voor Video op bestelling. |
   | `AOD` | Het type van stroom voor Audio op bestelling. |

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

1. **verbind meta-gegevens**

   Voeg desgewenst standaard- en/of aangepaste metagegevens toe aan de volgende sessie via de variabelen van de contextgegevens.

   * **Standaard meta-gegevens**

     >[!NOTE]
     >
     >U kunt de standaardmetagegevens niet koppelen.

      * De APIVerwijzing van de meta-gegevens van media sleutels - [ Standaard meta-gegevenssleutels - JavaScript ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

        Zie de uitvoerige reeks van beschikbare meta-gegevens hier: [ Audio en videoparameters ](/help/implementation/variables/audio-video-parameters.md)

   * **de meta-gegevens van de Douane**

     Maak een veranderlijk object voor de douanevariabelen en bevolk met de gegevens voor deze media. Bijvoorbeeld:

     ```js
     /* Set context data */
      var contextData = {};
     
      //Standard metadata
      contextData[ADB.Media.VideoMetadataKeys] = "Sample Episode";
      contextData[ADB.Media.VideoMetadataKeys] = "Sample Show";
     
      //Custom metadata
      contextData["isUserLoggedIn"] = "false";
      contextData["tvStation"] = "Sample TV Station";
     ```

1. **Spoor de intentie om playback** te beginnen

   Als u een mediasessie wilt volgen, roept u `trackSessionStart` aan op de Media Heartbeat-instantie:

   ```js
   var mediaObject = ADB.Media.createMediaObject("video-name",
                                                 "video-id",
                                                 60.0,
                                                 ADB.Media.StreamType.VOD,
                                                 ADB.Media.MediaType.Video);
   
   var contextData = {};
   
   //Standard metadata
   contextData[ADB.Media.VideoMetadataKeys] = "Sample Episode";
   contextData[ADB.Media.VideoMetadataKeys] = "Sample Show";
   
   //Custom metadata
   contextData["isUserLoggedIn"] = "false";
   contextData["tvStation"] = "Sample TV Station";
   
   tracker.trackSessionStart(mediaObject, contextData);
   ```

   >[!IMPORTANT]
   >
   >In `trackSessionStart` wordt bijgehouden wat de gebruiker wil afspelen, niet het begin van het afspelen. Deze API wordt gebruikt om de gegevens/meta-gegevens te laden en tijd-aan-begin metrische QoS (de tijdduur tussen `trackSessionStart` en `trackPlay`) te schatten.

   >[!NOTE]
   >
   >Als u contextData niet gebruikt, verzendt u gewoon een leeg object voor het argument `data` in `trackSessionStart` .

1. **spoor het daadwerkelijke begin van playback**

   Identificeer de gebeurtenis van de mediaspeler voor het begin van het afspelen, waar het eerste frame van de media op het scherm wordt weergegeven, en roep `trackPlay` aan:

   ```js
   tracker.trackPlay();
   ```

1. **de waarde van de Update playhead**

   Wanneer de afspeelkop van media verandert, geeft u een melding aan de SDK door de API `mediaUpdatePlayhead` aan te roepen. <br /> Voor video-op-verzoek (VOD) wordt de waarde opgegeven in seconden vanaf het begin van het media-item. <br /> Als de speler voor live streaming geen informatie geeft over de duur van de inhoud, kan de waarde worden opgegeven als het aantal seconden sinds middernacht UTC van die dag.

   ```
   tracker.updatePlayhead(position)
   ```

   >[!NOTE]
   >
   >Houd rekening met het volgende wanneer u de API `tracker.updatePlayhead` aanroept:
   >* Wanneer u voortgangsmarkeringen gebruikt, is de duur van de inhoud vereist en moet de afspeelkop worden bijgewerkt als het aantal seconden vanaf het begin van het media-item, te beginnen met 0.
   >* Wanneer u media-SDK&#39;s gebruikt, moet u de `tracker.updatePlayhead` API minstens één keer per seconde aanroepen.

1. **Spoor de voltooiing van playback**

   Identificeer de gebeurtenis van de media speler voor de voltooiing van het playback, waar de gebruiker de inhoud tot het eind heeft bekeken, en roep `trackComplete`:

   ```js
   tracker.trackComplete();
   ```

1. **Spoor het eind van de zitting**

   Identificeer de gebeurtenis van de mediaspeler voor het verwijderen/sluiten van het afspelen, waar de gebruiker de media en/of de media sluit en verwijderd is, en roep `trackSessionEnd` aan:

   ```js
   tracker.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` markeert het einde van een volgende sessie. Als de sessie succesvol is gecontroleerd op voltooiing, waarbij de gebruiker de inhoud tot het einde heeft gecontroleerd, controleert u of `trackComplete` vóór `trackSessionEnd` is aangeroepen. Eventuele andere `track*` API-aanroepen worden na `trackSessionEnd` genegeerd, behalve voor `trackSessionStart` voor een nieuwe traceringssessie.

1. **spoor alle mogelijke pauzescenario&#39;s**

   Identificeer de gebeurtenis van de media speler voor pauze en vraag `trackPause`:

   ```js
   tracker.trackPause();
   ```

   **Scenario&#39;s van de Pauze**

   Identificeer om het even welk scenario waarin de media speler zal pauzeren en zorg ervoor dat `trackPause` behoorlijk wordt geroepen. De volgende scenario&#39;s vereisen allemaal dat uw app `trackPause()` aanroept:

   * De gebruiker raakt expliciet de pauze in de app.
   * De speler plaatst zichzelf in de pauzestatus.
   * (*Mobiele Apps*) - de gebruiker zet de toepassing in de achtergrond, maar u wilt dat app de zitting open houdt.
   * (*Mobiele Apps*) - om het even welk type van systeem onderbreekt komt voor dat een toepassing veroorzaakt om worden gesteund. Bijvoorbeeld, ontvangt de gebruiker een vraag, of een pop-up van een andere toepassing komt voor, maar u wilt de toepassing de zitting levend houden om de gebruiker de kans te geven om de media van het punt van onderbreking te hervatten.

1. Identificeer de gebeurtenis van de speler voor spel en/of hervat van pauze en vraag `trackPlay`:

   ```js
   tracker.trackPlay();
   ```

   >[!TIP]
   >
   >Dit kan de zelfde gebeurtenisbron zijn die in Stap 4 werd gebruikt. Zorg ervoor dat elke API-aanroep van `trackPause()` wordt gekoppeld aan een volgende API-aanroep van `trackPlay()` wanneer het afspelen wordt hervat.

* Het volgen scenario&#39;s: [ de playback van VOD zonder advertenties ](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* Voorbeeld van een voorbeeldspeler die bij de JavaScript SDK wordt geleverd voor een volledig voorbeeld van &#39;tracking&#39;.
