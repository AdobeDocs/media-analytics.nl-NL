---
title: Leer hoe u het afspelen van de kern kunt bijhouden op Roku
description: Leer hoe u core tracking implementeert met de Media SDK op Roku.
uuid: a8aa7b3c-2d39-44d7-8ebc-b101d130101f
exl-id: 5272c0ce-4e3d-48c6-bfa6-94066ccbf9ac
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 1%

---

# Muziek afspelen bijhouden op Roku{#track-core-playback-on-roku}

Deze documentatie behandelt het volgen in versie 2.x van de SDK.

>[!IMPORTANT]
>
>Als u een 1.x versie van SDK uitvoert, kunt u 1.x de Gidsen van Ontwikkelaars hier downloaden: [&#x200B; Download SDKs &#x200B;](/help/getting-started/download-sdks.md)

1. **Aanvankelijke het volgen opstelling**

   Bepaal wanneer de gebruiker de afspeelintentie activeert (de gebruiker klikt op Afspelen en/of Automatisch afspelen is ingeschakeld) en maak een `MediaObject` -instantie.

   **`MediaObject`reference:**

   | Naam variabele | Beschrijving | Vereist |
   | --- | --- | :---: |
   | `name` | Videonaam | Ja |
   | `mediaid` | Unieke video-id | Ja |
   | `length` | Videolengte | Ja |
   | `streamType` | Het type van stroom (zie _constanten StreamType_ hieronder) | Ja |
   | `mediaType` | Het type van media (zie _constanten MediaType_ hieronder) | Ja |

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

   **creeer een media info voorwerp voor video met de inhoud van VOD:**

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

   **creeer een media informatievoorwerp voor video met inhoud AOD:**

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

1. **verbind meta-gegevens**

   Koppel standaard- en/of aangepaste metagegevensobjecten optioneel aan de volgende sessie via variabelen voor contextgegevens.

   * **Standaard meta-gegevens**

[Standaardmetagegevens implementeren op Roku](/help/use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)

     >[!NOTE]
     >
     >Het is optioneel om het standaardobject voor videometagegevens aan het mediaobject te koppelen.

   * **de meta-gegevens van de Douane**

     Maak een veranderlijk object voor de douanevariabelen en bevolk met de gegevens voor deze video. Bijvoorbeeld:

     ```
     mediaContextData = {}
     mediaContextData["cmk1"] = "cmv1"
     mediaContextData["cmk2"] = "cmv2"
     ```

1. **Spoor de intentie om playback** te beginnen

   Als u een mediasessie wilt volgen, roept u `trackSessionStart` aan op de Media Heartbeat-instantie:

   ```
   ADBMobile().mediaTrackSessionStart(mediaInfo,mediaContextData)
   ```

   >[!TIP]
   >
   >De tweede waarde is de aangepaste objectnaam voor videometagegevens die u in stap 2 hebt gemaakt.

   >[!IMPORTANT]
   >
   >In `trackSessionStart` wordt bijgehouden wat de gebruiker wil afspelen, niet het begin van het afspelen. Deze API wordt gebruikt om de videogegevens/meta-gegevens te laden en tijd-aan-begin metrische QoS (de tijdduur tussen `trackSessionStart` en `trackPlay`) te schatten.

   >[!NOTE]
   >
   >Als u geen aangepaste videometagegevens gebruikt, verzendt u gewoon een leeg object voor het argument `data` in `trackSessionStart` , zoals getoond in de regel met opmerkingen in het bovenstaande iOS-voorbeeld.

1. **spoor het daadwerkelijke begin van playback**

   Identificeer de gebeurtenis van de videospeler voor het begin van de videoplayback, waar het eerste kader van de video op het scherm wordt teruggegeven, en roep `trackPlay`:

   ```
   ADBMobile().mediaTrackPlay()
   ```

1. **de waarde van de Update playhead**

   Wanneer de afspeelkop van media verandert, geeft u een melding aan de SDK door de API `mediaUpdatePlayhead` aan te roepen. <br /> Voor video-op-verzoek (VOD) wordt de waarde opgegeven in seconden vanaf het begin van het media-item. <br /> Als de speler voor live streaming geen informatie geeft over de duur van de inhoud, kan de waarde worden opgegeven als het aantal seconden sinds middernacht UTC van die dag.

   ```
   ADBMobile().mediaUpdatePlayhead(position)
   ```

   >[!NOTE]
   >
   >Houd rekening met het volgende wanneer u de API `mediaUpdatePlayhead` aanroept:
   >* Wanneer u voortgangsmarkeringen gebruikt, is de duur van de inhoud vereist en moet de afspeelkop worden bijgewerkt als het aantal seconden vanaf het begin van het media-item, te beginnen met 0.
   >* Wanneer u media-SDK&#39;s gebruikt, moet u de `mediaUpdatePlayhead` API minstens één keer per seconde aanroepen.


1. **Spoor de voltooiing van playback**

   Identificeer de gebeurtenis van de videospeler voor de voltooiing van de videoplayback, waar de gebruiker de inhoud tot het eind heeft bekeken, en roep `trackComplete`:

   ```
   ADBMobile().mediaTrackComplete()
   ```

1. **Spoor het eind van de zitting**

   Identificeer de gebeurtenis van de videospeler voor het leegmaken/sluiten van de videoplayback, waar de gebruiker de video en/of de video voltooit en is verwijderd, en roep `trackSessionEnd`:

   ```
   ADBMobile().mediaTrackSessionEnd()
   ```

   >[!IMPORTANT]
   >`trackSessionEnd` markeert het einde van een videovervolgsessie. Als de sessie succesvol is gecontroleerd op voltooiing, waarbij de gebruiker de inhoud tot het einde heeft gecontroleerd, controleert u of `trackComplete` vóór `trackSessionEnd` is aangeroepen. Eventuele andere `track*` API-aanroepen worden na `trackSessionEnd` genegeerd, behalve voor `trackSessionStart` voor een nieuwe sessie voor het bijhouden van video.

1. **spoor alle mogelijke pauzescenario&#39;s**

   Identificeer de gebeurtenis van de videospeler voor videopauze en vraag `trackPause`:

   ```
   ADBMobile().mediaTrackPause()
   ```

   **Scenario&#39;s van de Pauze**

   Identificeer om het even welk scenario waarin VideoPlayer zal pauzeren en zorg ervoor dat `trackPause` behoorlijk wordt geroepen. De volgende scenario&#39;s vereisen allemaal dat uw app `trackPause()` aanroept:

   * De gebruiker raakt expliciet de pauze in de app.
   * De speler plaatst zichzelf in de pauzestatus.
   * (*Mobiele Apps*) - de gebruiker zet de toepassing in de achtergrond, maar u wilt dat app de zitting open houdt.
   * (*Mobiele Apps*) - om het even welk type van systeem onderbreekt komt voor dat een toepassing veroorzaakt om worden gesteund. Bijvoorbeeld, ontvangt de gebruiker een vraag, of een pop-up van een andere toepassing komt voor, maar u wilt de toepassing de zitting levend houden om de gebruiker de kans te geven om de video van het punt van onderbreking te hervatten.

1. Identificeer de gebeurtenis van de speler voor videospel en/of video hervat van pauze en vraag `trackPlay`:

   ```
   ADBMobile().mediaTrackPlay()
   ```

   >[!TIP]
   >Dit kan de zelfde gebeurtenisbron zijn die in Stap 4 werd gebruikt. Zorg ervoor dat elke API-aanroep van `trackPause()` wordt gekoppeld aan een volgende API-aanroep van `trackPlay()` wanneer het afspelen van de video wordt hervat.

* Het volgen scenario&#39;s: [&#x200B; de playback van VOD zonder advertenties &#x200B;](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* Voorbeeldspeler die bij de Roku SDK wordt geleverd voor een volledig voorbeeld van bijhouden.
