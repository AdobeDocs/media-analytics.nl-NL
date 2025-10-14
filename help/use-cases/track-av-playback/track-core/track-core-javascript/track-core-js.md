---
title: Leer hoe u het afspelen van de kern kunt bijhouden met JavaScript 2.x
description: Leer hoe u core tracking implementeert met de Media SDK in een browser met JavaScript 2.x-apps.
uuid: 3d6e0ab1-899a-43c3-b632-8276e84345ab
exl-id: d8af37a0-9048-4e6b-8cba-809386cbed5f
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 2%

---

# Core playback volgen met JavaScript 2.x{#track-core-playback-on-javascript}

De volgende instructies bieden richtlijnen voor implementatie in 2.x SDK&#39;s.

>[!IMPORTANT]
>Als u een 1.x versie van SDK uitvoert, kunt u 1.x de Gidsen van Ontwikkelaars hier downloaden: [&#x200B; Download SDKs &#x200B;](/help/getting-started/download-sdks.md)

1. **Aanvankelijke het volgen opstelling**

   Bepaal wanneer de gebruiker de afspeelintentie activeert (de gebruiker klikt op Afspelen en/of Automatisch afspelen is ingeschakeld) en maak een `MediaObject` -instantie.

   [&#x200B; createMediaObject API &#x200B;](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | Naam variabele | Beschrijving | Vereist |
   | --- | --- | :---: |
   | `name` | Mediumnaam | Ja |
   | `mediaid` | Unieke id voor media | Ja |
   | `length` | Medialengte | Ja |
   | `streamType` | Het type van stroom (zie _constanten StreamType_ hieronder) | Ja |
   | `mediaType` | Het type van media (zie _constanten MediaType_ hieronder) | Ja |

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

1. **verbind meta-gegevens**

   Koppel standaard- en/of aangepaste metagegevensobjecten optioneel aan de volgende sessie via variabelen voor contextgegevens.

   * **Standaard meta-gegevens**

     [Standaardmetadata implementeren in JavaScript](/help/use-cases/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)

     >[!NOTE]
     >
     >Het koppelen van het standaardobject voor metagegevens aan het mediaobject is optioneel.

      * De APIVerwijzing van de meta-gegevens van media sleutels - [&#x200B; Standaard meta-gegevenssleutels - JavaScript &#x200B;](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

        Zie de uitvoerige reeks van beschikbare meta-gegevens hier: [&#x200B; Audio en videoparameters &#x200B;](/help/implementation/variables/audio-video-parameters.md)

   * **de meta-gegevens van de Douane**

     Maak een veranderlijk object voor de douanevariabelen en bevolk met de gegevens voor deze media. Bijvoorbeeld:

     ```js
     /* Set custom context data */
     var customVideoMetadata = {
         isUserLoggedIn: "false",
         tvStation: "Sample TV station",
         programmer: "Sample programmer"
     };
     ```

1. **Spoor de intentie om playback** te beginnen

   Als u een mediasessie wilt volgen, roept u `trackSessionStart` aan op de Media Heartbeat-instantie:

   ```js
   mediaHeartbeat.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!TIP]
   >
   >De tweede waarde is de objectnaam voor aangepaste mediametagegevens die u in stap 2 hebt gemaakt.

   >[!IMPORTANT]
   >
   >In `trackSessionStart` wordt bijgehouden wat de gebruiker wil afspelen, niet het begin van het afspelen. Deze API wordt gebruikt om de gegevens/meta-gegevens te laden en tijd-aan-begin metrische QoS (de tijdduur tussen `trackSessionStart` en `trackPlay`) te schatten.

   >[!NOTE]
   >
   >Als u geen aangepaste metagegevens gebruikt, verzendt u gewoon een leeg object voor het argument `data` in `trackSessionStart` , zoals getoond in de regel met opmerkingen in het bovenstaande iOS-voorbeeld.

1. **spoor het daadwerkelijke begin van playback**

   Identificeer de gebeurtenis van de mediaspeler voor het begin van het afspelen, waar het eerste frame van de media op het scherm wordt weergegeven, en roep `trackPlay` aan:

   ```js
   mediaHeartbeat.trackPlay();
   ```

1. **Spoor de voltooiing van playback**

   Identificeer de gebeurtenis van de media speler voor de voltooiing van het playback, waar de gebruiker de inhoud tot het eind heeft bekeken, en roep `trackComplete`:

   ```js
   mediaHeartbeat.trackComplete();
   ```

1. **Spoor het eind van de zitting**

   Identificeer de gebeurtenis van de mediaspeler voor het verwijderen/sluiten van het afspelen, waar de gebruiker de media en/of de media sluit en verwijderd is, en roep `trackSessionEnd` aan:

   ```js
   mediaHeartbeat.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` markeert het einde van een volgende sessie. Als de sessie succesvol is gecontroleerd op voltooiing, waarbij de gebruiker de inhoud tot het einde heeft gecontroleerd, controleert u of `trackComplete` vóór `trackSessionEnd` is aangeroepen. Eventuele andere `track*` API-aanroepen worden na `trackSessionEnd` genegeerd, behalve voor `trackSessionStart` voor een nieuwe traceringssessie.

1. **spoor alle mogelijke pauzescenario&#39;s**

   Identificeer de gebeurtenis van de media speler voor pauze en vraag `trackPause`:

   ```js
   mediaHeartbeat.trackPause();
   ```

   **Scenario&#39;s van de Pauze**

   Identificeer om het even welk scenario waarin de media speler zal pauzeren en zorg ervoor dat `trackPause` behoorlijk wordt geroepen. De volgende scenario&#39;s vereisen allemaal dat uw app `trackPause()` aanroept:

   * De gebruiker raakt expliciet de pauze in de app.
   * De speler plaatst zichzelf in de pauzestatus.
   * (*Mobiele Apps*) - de gebruiker zet de toepassing in de achtergrond, maar u wilt dat app de zitting open houdt.
   * (*Mobiele Apps*) - om het even welk type van systeem onderbreekt komt voor dat een toepassing veroorzaakt om worden gesteund. Bijvoorbeeld, ontvangt de gebruiker een vraag, of een pop-up van een andere toepassing komt voor, maar u wilt de toepassing de zitting levend houden om de gebruiker de kans te geven om de media van het punt van onderbreking te hervatten.

1. Identificeer de gebeurtenis van de speler voor spel en/of hervat van pauze en vraag `trackPlay`:

   ```js
   mediaHeartbeat.trackPlay();
   ```

   >[!TIP]
   >
   >Dit kan de zelfde gebeurtenisbron zijn die in Stap 4 werd gebruikt. Zorg ervoor dat elke API-aanroep van `trackPause()` wordt gekoppeld aan een volgende API-aanroep van `trackPlay()` wanneer het afspelen wordt hervat.

* Het volgen scenario&#39;s: [&#x200B; de playback van VOD zonder advertenties &#x200B;](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* Voorbeeld van een voorbeeldspeler die bij de JavaScript SDK wordt geleverd voor een volledig voorbeeld van &#39;tracking&#39;.
