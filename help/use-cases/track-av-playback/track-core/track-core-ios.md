---
title: Meer informatie over het bijhouden van de Core Playback op iOS
description: Leer hoe u core tracking implementeert met de Media SDK op iOS.
uuid: bdc0e05c-4fe5-430e-aee2-f331bc59ac6b
exl-id: 5c6b36b3-a421-45a4-a65e-4eb57513ca4a
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 1%

---

# Muziek afspelen bijhouden op iOS{#track-core-playback-on-ios}

Deze documentatie behandelt het volgen in versie 2.x van de SDK.

>[!IMPORTANT]
>
>Als u een 1.x versie van SDK uitvoert, kunt u 1.x de Gidsen van Ontwikkelaars hier downloaden: [ Download SDKs ](/help/getting-started/download-sdks.md)

1. **Aanvankelijke het volgen opstelling**

   Bepaal wanneer de gebruiker de afspeelintentie activeert (de gebruiker klikt op Afspelen en/of Automatisch afspelen is ingeschakeld) en maak een `MediaObject` -instantie.

   [ createMediaObjectWithName API ](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)

   | Naam variabele | Beschrijving | Vereist |
   |---|---|---|
   | `name` | Videonaam | Ja |
   | `mediaid` | Unieke video-id | Ja |
   | `length` | Videolengte | Ja |
   | `streamType` | Het type van stroom (zie _constanten StreamType_ hieronder) | Ja |
   | `mediaType` | Het type van media (zie _constanten MediaType_ hieronder) | Ja |

   **`StreamType`constanten:**

   | Naam van constante | Beschrijving |
   |---|---|
   | `ADBMediaHeartbeatStreamTypeVOD` | Stroomtype voor Video op aanvraag |
   | `ADBMediaHeartbeatStreamTypeLIVE` | Stroomtype voor Live-inhoud |
   | `ADBMediaHeartbeatStreamTypeLINEAR` | Stroomtype voor lineaire inhoud |
   | `ADBMediaHeartbeatStreamTypeAOD` | Stroomtype voor audio op aanvraag |
   | `ADBMediaHeartbeatStreamTypeAUDIOBOOK` | Streaming type voor audioboek |
   | `ADBMediaHeartbeatStreamTypePODCAST` | Stroomtype voor Podcast |

   **`MediaType`constanten:**

   | Naam van constante | Beschrijving |
   |---|---|
   | `ADBMediaTypeAudio` | Mediatype voor audiostreams. |
   | `ADBMediaTypeVideo` | Mediatype voor videostreams. |

   De algemene indeling voor het maken van de `MediaObject` :

   ```
   ADBMediaObject *mediaObject =  
     [ADBMediaHeartbeat createMediaObjectWithName:<MEDIA_NAME>
                                          mediaId:<MEDIA_ID>
                                           length:<MEDIA_LENGTH>                       
                                       streamType:<STREAM_TYPE>
                                        mediaType: <MEDIA_TYPE>];
   ```

1. **Band videometagegevens**

   U kunt standaard- en/of aangepaste metagegevensobjecten voor video&#39;s optioneel aan de volgende sessie koppelen via variabelen voor contextgegevens.

   * **Standaard videometa-gegevens**

      * [Standaardmetagegevens implementeren op iOS](/help/use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
      * **Video meta-gegevenssleutels**
        [ de meta-gegevenssleutels van iOS ](/help/use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

      * Zie de uitvoerige lijst van videometagegevens hier: [ Audio en videoparameters ](/help/implementation/variables/audio-video-parameters.md)

     >[!NOTE]
     >
     >Het is optioneel om het standaardobject voor videometagegevens aan het mediaobject te koppelen.

   * **de meta-gegevens van de Douane**

     Maak een veranderlijk object voor de douanevariabelen en bevolk met de gegevens voor deze video. Bijvoorbeeld:

     ```
     NSMutableDictionary *videoMetadata = [[NSMutableDictionary alloc] init];
     [videoMetadata setObject:@"false" forKey:@"isUserLoggedIn"];
     [videoMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
     ```

1. **Spoor de intentie om playback** te beginnen

   Als u een mediasessie wilt bijhouden, roept u `trackSessionStart` aan op de Media Heartbeat-instantie.

   >[!TIP]
   >
   >De tweede waarde is de aangepaste objectnaam voor videometagegevens die u in stap 2 hebt gemaakt.

   ```
   - (void)onMainVideoLoaded:(NSNotification *)notification {
   //    [_mediaHeartbeat trackSessionStart:mediaObject data:nil];
       [_mediaHeartbeat trackSessionStart:mediaObject data:videoMetadata];
   }
   ```

   >[!IMPORTANT]
   >
   >In `trackSessionStart` wordt bijgehouden wat de gebruiker wil afspelen, niet het begin van het afspelen. Deze API wordt gebruikt om de videogegevens/meta-gegevens te laden en tijd-aan-begin metrische QoS (de tijdduur tussen `trackSessionStart` en `trackPlay`) te schatten.

   >[!NOTE]
   >
   >Als u geen aangepaste videometagegevens gebruikt, verzendt u gewoon een leeg object voor het argument `data` in `trackSessionStart` , zoals getoond in de regel met opmerkingen in het bovenstaande iOS-voorbeeld.

1. **spoor het daadwerkelijke begin van playback**

   Identificeer de gebeurtenis van de videospeler voor het begin van de videoplayback, waar het eerste kader van de video op het scherm wordt teruggegeven, en roep `trackPlay`:

   ```
   - (void)onVideoPlay:(NSNotification *)notification {
       [_mediaHeartbeat trackPlay];
   }
   ```

1. **Spoor de voltooiing van playback**

   Identificeer de gebeurtenis van de videospeler voor de voltooiing van de videoplayback, waar de gebruiker de inhoud tot het eind heeft bekeken, en roep `trackComplete`:

   ```
   - (void)onVideoComplete:(NSNotification *)notification {
       [_mediaHeartbeat trackComplete];
   }
   ```

1. **Spoor het eind van de zitting**

   Identificeer de gebeurtenis van de videospeler voor het leegmaken/sluiten van de videoplayback, waar de gebruiker de video en/of de video voltooit en is verwijderd, en roep `trackSessionEnd`:

   ```
   - void)onMainVideoUnloaded:(NSNotification *)notification {
       [_mediaHeartbeat trackSessionEnd];
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` markeert het einde van een videovervolgsessie. Als de sessie succesvol is gecontroleerd op voltooiing, waarbij de gebruiker de inhoud tot het einde heeft gecontroleerd, controleert u of `trackComplete` vóór `trackSessionEnd` is aangeroepen. Eventuele andere `track*` API-aanroepen worden na `trackSessionEnd` genegeerd, behalve voor `trackSessionStart` voor een nieuwe sessie voor het bijhouden van video.

1. **spoor alle mogelijke pauzescenario&#39;s**

   Identificeer de gebeurtenis van de videospeler voor videopauze en vraag `trackPause`:

   ```
   - (void)onVideoPause:(NSNotification *)notification {
       [_mediaHeartbeat trackPause];
   }
   ```

   **Scenario&#39;s van de Pauze**

   Identificeer om het even welk scenario waarin VideoPlayer zal pauzeren en zorg ervoor dat `trackPause` behoorlijk wordt geroepen. De volgende scenario&#39;s vereisen allemaal dat uw app `trackPause()` aanroept:

   * De gebruiker raakt expliciet de pauze in de app.
   * De speler plaatst zichzelf in de pauzestatus.
   * (*Mobiele Apps*) - de gebruiker zet de toepassing in de achtergrond, maar u wilt dat app de zitting open houdt.
   * (*Mobiele Apps*) - om het even welk type van systeem onderbreekt komt voor dat een toepassing veroorzaakt om worden gesteund. Bijvoorbeeld, ontvangt de gebruiker een vraag, of een pop-up van een andere toepassing komt voor, maar u wilt de toepassing de zitting levend houden om de gebruiker de kans te geven om de video van het punt van onderbreking te hervatten.

1. Identificeer de gebeurtenis van de speler voor videospel en/of video hervat van pauze en vraag `trackPlay`:

   ```
   - (void)onVideoPlay:(NSNotification *)notification {
       [_mediaHeartbeat trackPlay];
   }
   ```

   >[!TIP]
   >
   >Dit kan de zelfde gebeurtenisbron zijn die in Stap 4 werd gebruikt. Zorg ervoor dat elke API-aanroep van `trackPause()` wordt gekoppeld aan een volgende API-aanroep van `trackPlay()` wanneer het afspelen van de video wordt hervat.

Raadpleeg de volgende secties voor meer informatie over het bijhouden van het afspelen van core:

* Het volgen scenario&#39;s: [ de playback van VOD zonder advertenties ](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* Voorbeeld van een voorbeeldspeler die bij de iOS SDK wordt geleverd voor een volledig voorbeeld van &#39;tracking&#39;.
