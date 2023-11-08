---
title: Leer hoe u het afspelen van de core kunt bijhouden op Android
description: Leer hoe u core tracking implementeert met de Media SDK op Android.
uuid: ab5fab95-76ed-4ae6-aedb-2e66eece7607
exl-id: d5f5a3f0-f1e0-4d68-af7f-88a30faed0db
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: c308dba2d7cf07b89bf124bd6e5f972c253c9f18
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 2%

---

# Muziekweergave bijhouden op Android{#track-core-playback-on-android}

Deze documentatie behandelt het volgen in versie 2.x van SDK.
>[!IMPORTANT]
>
>Als u een 1.x-versie van de SDK implementeert, kunt u de 1.x-handleiding voor ontwikkelaars voor Android hier downloaden: [SDK&#39;s downloaden](/help/getting-started/download-sdks.md)

1. **Eerste instelling voor bijhouden**

   Identificeer wanneer de gebruiker de bedoeling van playback teweegbrengt (de gebruiker klikt spel en/of autoplay is) en creeer een `MediaObject` -instantie.

   [createMediaObject API](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)

   | Naam variabele | Beschrijving | Vereist |
   | --- | --- | :---: |
   | `name` | Mediumnaam | Ja |
   | `mediaId` | Unieke id voor media | Ja |
   | `length` | Medialengte | Ja |
   | `streamType` | Type stream (zie _StreamType-constanten_ hieronder) | Ja |
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

   Koppel standaard- en/of aangepaste metagegevensobjecten optioneel aan de volgende sessie via variabelen voor contextgegevens.

   * **Standaardmetagegevens**

     [Standaardmetadata implementeren in Android](/help/use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)

     >[!NOTE]
     >
     >Het koppelen van het standaardobject voor metagegevens aan het mediaobject is optioneel.

      * API-naslaggids voor metagegevens van media - [Standaardmetagegevenstoetsen - Android](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
      * Bekijk hier de uitgebreide set met beschikbare videometagegevens: [Parameters voor audio en video](/help/implementation/variables/audio-video-parameters.md)

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

   Als u een mediasessie wilt bijhouden, roept u `trackSessionStart` op de Media Heartbone-instantie. Bijvoorbeeld:

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
   >`trackSessionStart` Hiermee wordt bijgehouden wat de gebruiker wil afspelen, niet het begin van het afspelen. Deze API wordt gebruikt om de media gegevens/meta-gegevens te laden en tijd-aan-begin metrische QoS (de tijdsduur tussen `trackSessionStart` en `trackPlay`).

   >[!NOTE]
   >
   >Als u geen metagegevens van aangepaste media gebruikt, hoeft u eenvoudig een leeg object voor het tweede argument te verzenden in `trackSessionStart`.

1. **Het feitelijke begin van het afspelen bijhouden**

   Identificeer de gebeurtenis van de media speler voor het begin van media playback, waar het eerste kader van media op het scherm wordt teruggegeven, en vraag `trackPlay`:

   ```java
   // Video is rendered on the screen) and call trackPlay.  
   public void onVideoPlay(Observable observable, Object data) {
       _heartbeat.trackPlay();
   }
   ```

1. **De voltooiing van het afspelen bijhouden**

   Identificeer de gebeurtenis van de media speler voor de voltooiing van media playback, waar de gebruiker de inhoud tot het eind heeft bekeken, en vraag `trackComplete`:

   ```java
   public void onVideoComplete(Observable observable, Object data) {
       _heartbeat.trackComplete();
   }
   ```

1. **Het einde van de sessie bijhouden**

   Identificeer de gebeurtenis van de media speler voor het leegmaken/sluiten van de media playback, waar de gebruiker de media en/of de media voltooit en is leeggemaakt, en vraag `trackSessionEnd`:

   ```java
   // Closes the media and/or the media completed and unloaded,  
   // and call trackSessionEnd().  
   public void onMainVideoUnload(Observable observable, Object data) {  
       _heartbeat.trackSessionEnd();
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` markeert het einde van een mediatrackingsessie. Als de sessie succesvol is gecontroleerd naar voltooiing, waarbij de gebruiker de inhoud tot het einde heeft bekeken, zorgt u ervoor dat `trackComplete` wordt eerder aangeroepen `trackSessionEnd`. andere `track*` API-aanroep wordt genegeerd na `trackSessionEnd`, met uitzondering van `trackSessionStart` voor een nieuwe sessie voor mediatracering.

1. **Houd alle mogelijke pauzescenario&#39;s bij**

   De gebeurtenis van de mediaspeler identificeren voor pauzeren en aanroepen van media `trackPause`:

   ```java
   public void onVideoPause(Observable observable, Object data) {  
       _heartbeat.trackPause();
   }
   ```

   **Scenario&#39;s pauzeren**

   Identificeer om het even welk scenario waarin VideoPlayer zal pauzeren en zorg ervoor dat `trackPause` wordt correct aangeroepen. De volgende scenario&#39;s vereisen allemaal dat uw app wordt aangeroepen `trackPause()`:

   * De gebruiker raakt expliciet de pauze in de app.
   * De speler plaatst zichzelf in de pauzestatus.
   * (*Mobiele apps*) - De gebruiker plaatst de toepassing op de achtergrond, maar u wilt dat de toepassing de sessie geopend houdt.
   * (*Mobiele apps*) - Elk type onderbreking van het systeem treedt op waardoor een toepassing achteraan wordt geplaatst. Bijvoorbeeld, ontvangt de gebruiker een vraag, of een pop-up van een andere toepassing komt voor, maar u wilt de toepassing de zitting levend houden om de gebruiker de kans te geven om de media van het punt van onderbreking te hervatten.

1. De gebeurtenis van de speler identificeren voor het afspelen van media en/of het hervatten van media vanuit pauze en oproep `trackPlay`.

   ```java
   // trackPlay()
   public void onVideoPlay(Observable observable, Object data) {  
       _heartbeat.trackPlay();
   }
   ```

   >[!TIP]
   >
   >Dit kan de zelfde gebeurtenisbron zijn die in Stap 4 werd gebruikt. Zorg ervoor dat elk `trackPause()` API-aanroep is gekoppeld aan het volgende `trackPlay()` API-aanroep wanneer het afspelen van media wordt hervat.

Raadpleeg de volgende secties voor meer informatie over het bijhouden van het afspelen van core:

* Volgscenario&#39;s: [VOD afspelen zonder advertenties](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* Voorbeeldspeler die is opgenomen in de Android-SDK voor een volledig voorbeeld van bijhouden.
