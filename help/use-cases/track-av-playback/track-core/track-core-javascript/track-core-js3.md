---
title: Leer hoe u het afspelen van kernelementen kunt bijhouden met JavaScript v3.x
description: Leer hoe u core tracking implementeert met de Media SDK in een browser met JavaScript 3.x-apps.
exl-id: f3145450-82ba-4790-91a4-9d2cc97bbaa5
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: c308dba2d7cf07b89bf124bd6e5f972c253c9f18
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 0%

---

# Muziek afspelen bijhouden met JavaScript 3.x{#track-core-playback-on-javascript}

Deze documentatie behandelt het volgen in versie 3.x van SDK.

>[!IMPORTANT]
>
>Als u eerdere versies van de SDK implementeert, kunt u de ontwikkelaarsgidsen hier downloaden: [SDK&#39;s downloaden](/help/getting-started/download-sdks.md)

1. **Eerste instelling voor bijhouden**

   Identificeer wanneer de gebruiker de bedoeling van playback teweegbrengt (de gebruiker klikt spel en/of autoplay is) en creeer een `MediaObject` -instantie.

   [createMediaObject API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

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

1. **Metagegevens koppelen**

   Voeg desgewenst standaard- en/of aangepaste metagegevens toe aan de volgende sessie via de variabelen van de contextgegevens.

   * **Standaardmetagegevens**

     >[!NOTE]
     >
     >U kunt de standaardmetagegevens niet koppelen.

      * API-naslaggids voor metagegevens van media - [Standaardmetagegevenstoetsen - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

        Hier vindt u de uitgebreide set met beschikbare metagegevens: [Parameters voor audio en video](/help/implementation/variables/audio-video-parameters.md)

   * **Aangepaste metagegevens**

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

1. **Houd de intentie bij om het afspelen te starten**

   Als u een mediasessie wilt bijhouden, roept u `trackSessionStart` op de Media Heartbone-instantie:

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
   >`trackSessionStart` Hiermee wordt bijgehouden wat de gebruiker wil afspelen, niet het begin van het afspelen. Deze API wordt gebruikt om de gegevens/meta-gegevens te laden en tijd-aan-begin metrische QoS (de tijdsduur tussen `trackSessionStart` en `trackPlay`).

   >[!NOTE]
   >
   >Als u contextData niet gebruikt, verzendt u gewoon een leeg object voor de `data` argument in `trackSessionStart`.

1. **Het feitelijke begin van het afspelen bijhouden**

   Identificeer de gebeurtenis van de media speler voor het begin van het playback, waar het eerste kader van de media op het scherm wordt teruggegeven, en vraag `trackPlay`:

   ```js
   tracker.trackPlay();
   ```

1. **Waarde van afspeelkop bijwerken**

   Wanneer de afspeelkop van media verandert, geeft u een melding aan de SDK door de `mediaUpdatePlayhead` API. <br /> Voor video-op-bestelling (VOD), wordt de waarde gespecificeerd in seconden vanaf het begin van het media punt. <br /> Wanneer de speler voor live streaming geen informatie over de duur van de inhoud geeft, kan de waarde worden opgegeven als het aantal seconden dat is verstreken sinds middernacht UTC van die dag.

   ```
   tracker.updatePlayhead(position)
   ```

   >[!NOTE]
   >
   >Overweeg het volgende wanneer het roepen van `tracker.updatePlayhead` API:
   >* Wanneer u voortgangsmarkeringen gebruikt, is de duur van de inhoud vereist en moet de afspeelkop worden bijgewerkt als het aantal seconden vanaf het begin van het media-item, te beginnen met 0.
   >* Als u media-SDK&#39;s gebruikt, moet u de `tracker.updatePlayhead` API minstens één keer per seconde.

1. **De voltooiing van het afspelen bijhouden**

   Identificeer de gebeurtenis van de media speler voor de voltooiing van het playback, waar de gebruiker de inhoud tot het eind heeft bekeken, en vraag `trackComplete`:

   ```js
   tracker.trackComplete();
   ```

1. **Het einde van de sessie bijhouden**

   Identificeer de gebeurtenis van de media speler voor het leegmaken/sluiten van het playback, waar de gebruiker de media en/of de media sluit wordt voltooid en is leeggemaakt, en vraag `trackSessionEnd`:

   ```js
   tracker.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` markeert het einde van een volgende sessie. Als de sessie succesvol is gecontroleerd naar voltooiing, waarbij de gebruiker de inhoud tot het einde heeft bekeken, zorgt u ervoor dat `trackComplete` wordt eerder aangeroepen `trackSessionEnd`. andere `track*` API-aanroep wordt genegeerd na `trackSessionEnd`, met uitzondering van `trackSessionStart` voor een nieuwe traceringssessie.

1. **Houd alle mogelijke pauzescenario&#39;s bij**

   Identificeer de gebeurtenis van de media speler voor pauze en vraag `trackPause`:

   ```js
   tracker.trackPause();
   ```

   **Scenario&#39;s pauzeren**

   Identificeer om het even welk scenario waarin de media speler zal pauzeren en zorg ervoor dat `trackPause` wordt correct aangeroepen. De volgende scenario&#39;s vereisen allemaal dat uw app wordt aangeroepen `trackPause()`:

   * De gebruiker raakt expliciet de pauze in de app.
   * De speler plaatst zichzelf in de pauzestatus.
   * (*Mobiele apps*) - De gebruiker plaatst de toepassing op de achtergrond, maar u wilt dat de toepassing de sessie geopend houdt.
   * (*Mobiele apps*) - Elk type onderbreking van het systeem treedt op waardoor een toepassing achteraan wordt geplaatst. Bijvoorbeeld, ontvangt de gebruiker een vraag, of een pop-up van een andere toepassing komt voor, maar u wilt de toepassing de zitting levend houden om de gebruiker de kans te geven om de media van het punt van onderbreking te hervatten.

1. De gebeurtenis van de speler identificeren voor afspelen en/of hervatten vanuit pauzeren en aanroepen `trackPlay`:

   ```js
   tracker.trackPlay();
   ```

   >[!TIP]
   >
   >Dit kan de zelfde gebeurtenisbron zijn die in Stap 4 werd gebruikt. Zorg ervoor dat elk `trackPause()` API-aanroep is gekoppeld aan het volgende `trackPlay()` API-aanroep wanneer het afspelen wordt hervat.

* Volgscenario&#39;s: [VOD afspelen zonder advertenties](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* Voorbeeldspeler die is opgenomen in de JavaScript SDK voor een volledig voorbeeld van bijhouden.
