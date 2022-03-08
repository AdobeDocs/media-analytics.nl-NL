---
title: Leer hoe u het afspelen van de kern kunt bijhouden op Roku
description: Leer hoe te om kern het volgen uit te voeren gebruikend Media SDK op Roku.
uuid: a8aa7b3c-2d39-44d7-8ebc-b101d130101f
exl-id: 5272c0ce-4e3d-48c6-bfa6-94066ccbf9ac
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 14329fab02e88cbad69ceea4ccd719b90f6555a6
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 1%

---

# Muziek afspelen bijhouden op Roku{#track-core-playback-on-roku}

Deze documentatie behandelt het volgen in versie 2.x van SDK.

>[!IMPORTANT]
>Als u een 1.x-versie van de SDK implementeert, kunt u hier de 1.x-handleidingen voor ontwikkelaars downloaden: [SDK&#39;s downloaden](/help/sdk-implement/download-sdks.md)

1. **Eerste instelling voor bijhouden**

   Identificeer wanneer de gebruiker de bedoeling van playback teweegbrengt (de gebruiker klikt spel en/of autoplay is) en creeer een `MediaObject` -instantie.

   **`MediaObject`referentie:**

   | Naam variabele | Beschrijving | Vereist |
   | --- | --- | :---: |
   | `name` | Videonaam | Ja |
   | `mediaid` | Unieke videoid | Ja |
   | `length` | Videolengte | Ja |
   | `streamType` | Type stream (zie _StreamType-constanten_ hieronder) | Ja |
   | `mediaType` | Mediatype (zie _MediaType-constanten_ hieronder) | Ja |

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

   **Maak een Media Info-object voor video met VOD-inhoud:**

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

   **Een Media Info-object maken voor video met AOD-inhoud:**

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

1. **Metagegevens koppelen**

   Koppel standaard- en/of aangepaste metagegevensobjecten optioneel aan de volgende sessie via de variabelen van de contextgegevens.

   * **Standaardmetagegevens**

[Standaardmetadata implementeren in Roku](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)

      >[!NOTE]
      >Het is optioneel om het standaardobject voor videometagegevens aan het mediaobject te koppelen.

   * **Aangepaste metagegevens**

      Maak een veranderlijk object voor de douanevariabelen en bevolk met de gegevens voor deze video. Bijvoorbeeld:

      ```
      mediaContextData = {}
      mediaContextData["cmk1"] = "cmv1"
      mediaContextData["cmk2"] = "cmv2"
      ```

1. **Houd de intentie bij om het afspelen te starten**

   Als u een mediasessie wilt bijhouden, roept u `trackSessionStart` op de Media Heartbone-instantie:

   ```
   ADBMobile().mediaTrackSessionStart(mediaInfo,mediaContextData)
   ```

   >[!TIP]
   >De tweede waarde is de aangepaste objectnaam voor videometagegevens die u in stap 2 hebt gemaakt.

   >[!IMPORTANT]
   >`trackSessionStart` Hiermee wordt bijgehouden wat de gebruiker wil afspelen, niet het begin van het afspelen. Deze API wordt gebruikt om de videogegevens/meta-gegevens te laden en tijd-aan-begin metrische QoS (de tijdsduur tussen `trackSessionStart` en `trackPlay`).

   >[!NOTE]
   >Als u geen aangepaste videometagegevens gebruikt, kunt u gewoon een leeg object verzenden voor de `data` argument in `trackSessionStart`, zoals getoond in de commentaarlijn in het iOS voorbeeld hierboven.

1. **Het feitelijke begin van het afspelen bijhouden**

   Identificeer de gebeurtenis van de videospeler voor het begin van de videoplayback, waar het eerste kader van de video op het scherm wordt teruggegeven, en vraag `trackPlay`:

   ```
   ADBMobile().mediaTrackPlay()
   ```

1. **Waarde van afspeelkop bijwerken**

   Wanneer de veranderingen van de media playhead de SDK door te roepen op de hoogte brengen `mediaUpdatePlayhead` API. <br /> Voor video-op-bestelling (VOD), wordt de waarde gespecificeerd in seconden vanaf het begin van het media punt. <br /> Wanneer de speler voor live streaming geen informatie over de duur van de inhoud geeft, kan de waarde worden opgegeven als het aantal seconden dat is verstreken sinds middernacht UTC van die dag. <br /> Opmerking: Wanneer u voortgangsmarkeringen gebruikt, is de duur van de inhoud vereist en moet de afspeelkop worden bijgewerkt als het aantal seconden vanaf het begin van het media-item, te beginnen met 0.


   ```
   ADBMobile().mediaUpdatePlayhead(position)
   ```

1. **De voltooiing van het afspelen bijhouden**

   Identificeer de gebeurtenis van de videospeler voor de voltooiing van de videoplayback, waar de gebruiker de inhoud tot het eind heeft bekeken, en vraag `trackComplete`:

   ```
   ADBMobile().mediaTrackComplete()
   ```

1. **Het einde van de sessie bijhouden**

   Identificeer de gebeurtenis van de videospeler voor het leegmaken/sluiten van de videoplayback, waar de gebruiker de video en/of de video voltooit en is leeggemaakt, en vraag `trackSessionEnd`:

   ```
   ADBMobile().mediaTrackSessionEnd()
   ```

   >[!IMPORTANT]
   >`trackSessionEnd` markeert het einde van een videolesessie. Als de sessie succesvol is gecontroleerd naar voltooiing, waarbij de gebruiker de inhoud tot het einde heeft bekeken, zorgt u ervoor dat `trackComplete` wordt eerder aangeroepen `trackSessionEnd`. andere `track*` API-aanroep wordt genegeerd na `trackSessionEnd`, met uitzondering van `trackSessionStart` voor een nieuwe sessie voor het bijhouden van video.

1. **Houd alle mogelijke pauzescenario&#39;s bij**

   De gebeurtenis van de videospeler identificeren voor pauzeren en oproepen van video `trackPause`:

   ```
   ADBMobile().mediaTrackPause()
   ```

   **Scenario&#39;s pauzeren**

   Identificeer om het even welk scenario waarin VideoPlayer zal pauzeren en zorg ervoor dat `trackPause` wordt correct geroepen. De volgende scenario&#39;s vereisen allemaal dat uw app wordt aangeroepen `trackPause()`:

   * De gebruiker raakt expliciet de pauze in de app.
   * De speler plaatst zichzelf in de pauzestatus.
   * (*Mobiele apps*) - De gebruiker plaatst de toepassing op de achtergrond, maar u wilt dat de toepassing de sessie geopend houdt.
   * (*Mobiele apps*) - Elk type onderbreking van het systeem treedt op waardoor een toepassing achteraan wordt geplaatst. Bijvoorbeeld, ontvangt de gebruiker een vraag, of een pop-up van een andere toepassing komt voor, maar u wilt de toepassing de zitting levend houden om de gebruiker de kans te geven om de video van het punt van onderbreking te hervatten.

1. De gebeurtenis van de speler identificeren voor het afspelen van video en/of het hervatten van video vanaf het pauzeren en aanroepen `trackPlay`:

   ```
   ADBMobile().mediaTrackPlay()
   ```

   >[!TIP]
   >Dit kan de zelfde gebeurtenisbron zijn die in Stap 4 werd gebruikt. Zorg ervoor dat elk `trackPause()` API-aanroep is gekoppeld aan het volgende `trackPlay()` API-aanroep wanneer het afspelen van de video wordt hervat.

* Volgscenario&#39;s: [VOD afspelen zonder advertenties](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Voorbeeldspeler die is opgenomen in de SDK van Roku voor een volledig voorbeeld van bijhouden.
