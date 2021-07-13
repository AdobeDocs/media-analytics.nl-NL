---
title: Leer hoe u het afspelen van de core kunt bijhouden op Android
description: Leer hoe u core tracking implementeert met de Media SDK op Android.
uuid: ab5fab95-76ed-4ae6-aedb-2e66eece7607
exl-id: d5f5a3f0-f1e0-4d68-af7f-88a30faed0db
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 2%

---

# Core playback bijhouden op Android{#track-core-playback-on-android}

>[!IMPORTANT]
>Deze documentatie behandelt het volgen in versie 2.x van SDK. Als u een 1.x-versie van de SDK implementeert, kunt u de 1.x-handleiding voor ontwikkelaars voor Android hier downloaden: [SDK&#39;s downloaden](/help/sdk-implement/download-sdks.md)

1. **Eerste instelling voor bijhouden**

   Identificeer wanneer de gebruiker de bedoeling van playback teweegbrengt (de gebruiker klikt spel en/of autoplay is) en creeer een `MediaObject` instantie.

   [createMediaObject API](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)

   | Naam variabele | Beschrijving | Vereist |
   | --- | --- | :---: |
   | `name` | Mediumnaam | Ja |
   | `mediaId` | Unieke id voor media | Ja |
   | `length` | Medialengte | Ja |
   | `streamType` | Stroomtype (zie _StreamType-constanten_ hieronder) | Ja |
   | `mediaType` | Mediatype (zie _MediaType-constanten_ hieronder) | Ja |

   **`StreamType`constanten:**

   | Naam van constante | Beschrijving |
   |---|---|
   | `VOD` | Het type van stroom voor Video op bestelling. |
   | `LIVE` | Streamtype voor Live-inhoud. |
   | `LINEAR` | Het type van stroom voor Lineaire inhoud. |
   | `AOD` | Stroomtype voor audio op aanvraag |
   | `AUDIOBOOK` | Streaming type voor audioboek |
   | `PODCAST` | Stroomtype voor Podcast |

   **`MediaType`constanten:**

   | Naam van constante | Beschrijving |
   |---|---|
   | `Audio` | Mediatype voor audiostreams. |
   | `Video` | Mediatype voor videostreams. |

   ```
   MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
     <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);
   ```

1. **Metagegevens koppelen**

   Koppel standaard- en/of aangepaste metagegevensobjecten optioneel aan de volgende sessie via de variabelen van de contextgegevens.

   * **Standaardmetagegevens**

      [Standaardmetadata implementeren in Android](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)

      >[!NOTE]
      >
      >Het koppelen van het standaardobject voor metagegevens aan het mediaobject is optioneel.

      * API-naslaggids voor metagegevens van media - [Standaardmetagegevenstoetsen - Android](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
      * Bekijk hier de uitgebreide set met beschikbare videometagegevens: [Parameters voor audio en video](/help/metrics-and-metadata/audio-video-parameters.md)
   * **Aangepaste metagegevens**

      Maak een woordenboek voor de aangepaste variabelen en vul de gegevens voor deze media in. Bijvoorbeeld:

      ```java
      HashMap<String, String> mediaMetadata =  
        new HashMap<String, String>(); 
      mediaMetadata.put("isUserLoggedIn", "false"); 
      mediaMetadata.put("tvStation", "Sample TV Station"); 
      mediaMetadata.put("programmer", "Sample programmer");
      ```


1. **Houd de intentie bij om het afspelen te starten**

   Als u een mediasessie wilt volgen, roept u `trackSessionStart` op in de Media Heartbeat-instantie. Bijvoorbeeld:

   ```java
   public void onVideoLoad(Observable observable, Object data) {  
       _heartbeat.trackSessionStart(mediaInfo, mediaMetadata); 
   }
   ```

   >[!TIP]
   >
   >De tweede waarde is de objectnaam voor aangepaste mediametagegevens die u in stap 2 hebt gemaakt.

   >[!IMPORTANT]
   >
   >`trackSessionStart` Hiermee wordt bijgehouden wat de gebruiker wil afspelen, niet het begin van het afspelen. Deze API wordt gebruikt om de media gegevens/meta-gegevens te laden en tijd-aan-begin metrische QoS (de tijdduur tussen `trackSessionStart` en `trackPlay`) te schatten.

   >[!NOTE]
   >
   >Als u geen meta-gegevens van douanemedia gebruikt, verzend eenvoudig een leeg voorwerp voor het tweede argument in `trackSessionStart`.

1. **Het feitelijke begin van het afspelen bijhouden**

   Identificeer de gebeurtenis van de media speler voor het begin van media playback, waar het eerste kader van media op het scherm wordt teruggegeven, en roep `trackPlay`:

   ```java
   // Video is rendered on the screen) and call trackPlay.  
   public void onVideoPlay(Observable observable, Object data) { 
       _heartbeat.trackPlay(); 
   }
   ```

1. **De voltooiing van het afspelen bijhouden**

   Identificeer de gebeurtenis van de media speler voor de voltooiing van media playback, waar de gebruiker de inhoud tot het eind heeft bekeken, en roep `trackComplete`:

   ```java
   public void onVideoComplete(Observable observable, Object data) { 
       _heartbeat.trackComplete(); 
   }
   ```

1. **Het einde van de sessie bijhouden**

   Identificeer de gebeurtenis van de mediaspeler voor het verwijderen/sluiten van het afspelen van de media, waar de gebruiker de media en/of de media sluit en verwijderd is, en roep `trackSessionEnd`:

   ```java
   // Closes the media and/or the media completed and unloaded,  
   // and call trackSessionEnd().  
   public void onMainVideoUnload(Observable observable, Object data) {  
       _heartbeat.trackSessionEnd(); 
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` markeert het einde van een mediatrackingsessie. Als de sessie succesvol is gecontroleerd op voltooiing, waarbij de gebruiker de inhoud tot het einde heeft bekeken, controleert u of `trackComplete` vóór `trackSessionEnd` is aangeroepen. Eventuele andere `track*` API-aanroepen worden genegeerd na `trackSessionEnd`, behalve `trackSessionStart` voor een nieuwe mediatrackingsessie.

1. **Houd alle mogelijke pauzescenario&#39;s bij**

   Identificeer de gebeurtenis van de media speler voor media pauzeren en roepen `trackPause`:

   ```java
   public void onVideoPause(Observable observable, Object data) {  
       _heartbeat.trackPause(); 
   }
   ```

   **Scenario&#39;s pauzeren**

   Identificeer om het even welk scenario waarin de Videospeler zal pauzeren en zorg ervoor dat `trackPause` behoorlijk wordt geroepen. De volgende scenario&#39;s vereisen allen dat uw app `trackPause()` roept:

   * De gebruiker raakt expliciet de pauze in de app.
   * De speler plaatst zichzelf in de pauzestatus.
   * (*Mobiele toepassingen*) - De gebruiker plaatst de toepassing op de achtergrond, maar u wilt dat de toepassing de sessie geopend houdt.
   * (*Mobiele toepassingen*) - Elk type systeem dat wordt onderbroken, zorgt ervoor dat een toepassing op de achtergrond wordt gezet. Bijvoorbeeld, ontvangt de gebruiker een vraag, of een pop-up van een andere toepassing komt voor, maar u wilt de toepassing de zitting levend houden om de gebruiker de kans te geven om de media van het punt van onderbreking te hervatten.

1. Identificeer de gebeurtenis van de speler voor media spel en/of media hervat van pauze en vraag `trackPlay`.

   ```java
   // trackPlay() 
   public void onVideoPlay(Observable observable, Object data) {  
       _heartbeat.trackPlay(); 
   }
   ```

   >[!TIP]
   >
   >Dit kan de zelfde gebeurtenisbron zijn die in Stap 4 werd gebruikt. Zorg ervoor dat elke `trackPause()` API vraag met volgende `trackPlay()` API vraag wordt geparseerd wanneer de media playback hervat.

Raadpleeg de volgende secties voor meer informatie over het bijhouden van het afspelen van core:

* Volgscenario&#39;s: [VOD afspelen zonder advertenties](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Voorbeeldspeler die is opgenomen in de Android-SDK voor een volledig voorbeeld van bijhouden.
