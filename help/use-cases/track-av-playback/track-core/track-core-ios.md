---
title: Meer informatie over het bijhouden van de Core Playback op iOS
description: Leer hoe u core tracking implementeert met de Media SDK op iOS.
uuid: bdc0e05c-4fe5-430e-aee2-f331bc59ac6b
exl-id: 5c6b36b3-a421-45a4-a65e-4eb57513ca4a
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 2%

---

# Core playback bijhouden op iOS{#track-core-playback-on-ios}

Deze documentatie behandelt het volgen in versie 2.x van SDK.

>[!IMPORTANT]
>Als u een 1.x-versie van de SDK implementeert, kunt u hier de 1.x-handleidingen voor ontwikkelaars downloaden: [SDK&#39;s downloaden](/help/getting-started/download-sdks.md)

1. **Eerste instelling voor bijhouden**

   Identificeer wanneer de gebruiker de bedoeling van playback teweegbrengt (de gebruiker klikt spel en/of autoplay is) en creeer een `MediaObject` -instantie.

   [createMediaObjectWithName API](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)

   | Naam variabele | Beschrijving | Vereist |
   |---|---|---|
   | `name` | Videonaam | Ja |
   | `mediaid` | Unieke videoid | Ja |
   | `length` | Videolengte | Ja |
   | `streamType` | Type stream (zie _StreamType-constanten_ hieronder) | Ja |
   | `mediaType` | Mediatype (zie _MediaType-constanten_ hieronder) | Ja |

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

   De algemene indeling voor het maken van de `MediaObject`:

   ```
   ADBMediaObject *mediaObject =  
     [ADBMediaHeartbeat createMediaObjectWithName:<MEDIA_NAME>
                                          mediaId:<MEDIA_ID>
                                           length:<MEDIA_LENGTH>                       
                                       streamType:<STREAM_TYPE>
                                        mediaType: <MEDIA_TYPE>];
   ```

1. **Metagegevens van video bijvoegen**

   U kunt standaard- en/of aangepaste metagegevensobjecten voor video&#39;s optioneel aan de volgende sessie koppelen via variabelen voor contextgegevens.

   * **Standaard videometagegevens**

      * [Standaardmetadata implementeren in iOS](/help/use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
      * **Videometagegevens**

         [iOS-metagegevenssleutels](/help/use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

      * Zie de uitgebreide lijst met videometagegevens hier: [Parameters voor audio en video](/help/implementation/variables/audio-video-parameters.md)
      >[!NOTE]
      >
      >Het is optioneel om het standaardobject voor videometagegevens aan het mediaobject te koppelen.

   * **Aangepaste metagegevens**

      Maak een veranderlijk object voor de douanevariabelen en bevolk met de gegevens voor deze video. Bijvoorbeeld:

      ```
      NSMutableDictionary *videoMetadata = [[NSMutableDictionary alloc] init];
      [videoMetadata setObject:@"false" forKey:@"isUserLoggedIn"];
      [videoMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
      ```


1. **Houd de intentie bij om het afspelen te starten**

   Als u een mediasessie wilt bijhouden, roept u `trackSessionStart` op de Media Heartbone-instantie.

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
   >`trackSessionStart` Hiermee wordt bijgehouden wat de gebruiker wil afspelen, niet het begin van het afspelen. Deze API wordt gebruikt om de videogegevens/meta-gegevens te laden en tijd-aan-begin metrische QoS (de tijdsduur tussen `trackSessionStart` en `trackPlay`).

   >[!NOTE]
   >
   >Als u geen aangepaste videometagegevens gebruikt, kunt u gewoon een leeg object verzenden voor de `data` argument in `trackSessionStart`, zoals getoond in de commentaarlijn in het iOS voorbeeld hierboven.

1. **Het feitelijke begin van het afspelen bijhouden**

   Identificeer de gebeurtenis van de videospeler voor het begin van de videoplayback, waar het eerste kader van de video op het scherm wordt teruggegeven, en vraag `trackPlay`:

   ```
   - (void)onVideoPlay:(NSNotification *)notification {
       [_mediaHeartbeat trackPlay];
   }
   ```

1. **De voltooiing van het afspelen bijhouden**

   Identificeer de gebeurtenis van de videospeler voor de voltooiing van de videoplayback, waar de gebruiker de inhoud tot het eind heeft bekeken, en vraag `trackComplete`:

   ```
   - (void)onVideoComplete:(NSNotification *)notification {
       [_mediaHeartbeat trackComplete];
   }
   ```

1. **Het einde van de sessie bijhouden**

   Identificeer de gebeurtenis van de videospeler voor het leegmaken/sluiten van de videoplayback, waar de gebruiker de video en/of de video voltooit en is leeggemaakt, en vraag `trackSessionEnd`:

   ```
   - void)onMainVideoUnloaded:(NSNotification *)notification {
       [_mediaHeartbeat trackSessionEnd];
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` markeert het einde van een videolesessie. Als de sessie succesvol is gecontroleerd naar voltooiing, waarbij de gebruiker de inhoud tot het einde heeft bekeken, zorgt u ervoor dat `trackComplete` wordt eerder aangeroepen `trackSessionEnd`. andere `track*` API-aanroep wordt genegeerd na `trackSessionEnd`, met uitzondering van `trackSessionStart` voor een nieuwe sessie voor het bijhouden van video.

1. **Houd alle mogelijke pauzescenario&#39;s bij**

   De gebeurtenis van de videospeler identificeren voor pauzeren en oproepen van video `trackPause`:

   ```
   - (void)onVideoPause:(NSNotification *)notification {
       [_mediaHeartbeat trackPause];
   }
   ```

   **Scenario&#39;s pauzeren**

   Identificeer om het even welk scenario waarin VideoPlayer zal pauzeren en zorg ervoor dat `trackPause` wordt correct geroepen. De volgende scenario&#39;s vereisen allemaal dat uw app wordt aangeroepen `trackPause()`:

   * De gebruiker raakt expliciet de pauze in de app.
   * De speler plaatst zichzelf in de pauzestatus.
   * (*Mobiele apps*) - De gebruiker plaatst de toepassing op de achtergrond, maar u wilt dat de toepassing de sessie geopend houdt.
   * (*Mobiele apps*) - Elk type onderbreking van het systeem treedt op waardoor een toepassing achteraan wordt geplaatst. Bijvoorbeeld, ontvangt de gebruiker een vraag, of een pop-up van een andere toepassing komt voor, maar u wilt de toepassing de zitting levend houden om de gebruiker de kans te geven om de video van het punt van onderbreking te hervatten.

1. De gebeurtenis van de speler identificeren voor het afspelen van video en/of het hervatten van video vanaf het pauzeren en aanroepen `trackPlay`:

   ```
   - (void)onVideoPlay:(NSNotification *)notification {
       [_mediaHeartbeat trackPlay];
   }
   ```

   >[!TIP]
   >
   >Dit kan de zelfde gebeurtenisbron zijn die in Stap 4 werd gebruikt. Zorg ervoor dat elk `trackPause()` API-aanroep is gekoppeld aan het volgende `trackPlay()` API-aanroep wanneer het afspelen van de video wordt hervat.

Raadpleeg de volgende secties voor meer informatie over het bijhouden van het afspelen van core:

* Volgscenario&#39;s: [VOD afspelen zonder advertenties](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* Voorbeeldspeler die is opgenomen in de SDK van iOS voor een volledig voorbeeld van &#39;tracking&#39;.
