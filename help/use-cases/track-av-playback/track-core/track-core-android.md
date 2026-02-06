---
title: Meer informatie over het bijhouden van de Core Playback op Android
description: Leer hoe u core tracking implementeert met de Media SDK op Android.
uuid: ab5fab95-76ed-4ae6-aedb-2e66eece7607
exl-id: d5f5a3f0-f1e0-4d68-af7f-88a30faed0db
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 2%

---

# Muziek afspelen bijhouden op Android{#track-core-playback-on-android}

Deze documentatie behandelt het volgen in versie 2.x van de SDK.
>[!IMPORTANT]
>
>Als u een 1.x versie van SDK uitvoert, kunt u de 1.x Gids van Ontwikkelaars voor Android hier downloaden: [&#x200B; Download SDKs &#x200B;](/help/getting-started/download-sdks.md)

1. **Aanvankelijke het volgen opstelling**

   Bepaal wanneer de gebruiker de afspeelintentie activeert (de gebruiker klikt op Afspelen en/of Automatisch afspelen is ingeschakeld) en maak een `MediaObject` -instantie.

   [&#x200B; createMediaObject API &#x200B;](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)

   | Naam variabele | Beschrijving | Vereist |
   | --- | --- | :---: |
   | `name` | Mediumnaam | Ja |
   | `mediaId` | Unieke id voor media | Ja |
   | `length` | Medialengte | Ja |
   | `streamType` | Het type van stroom (zie _constanten StreamType_ hieronder) | Ja |
   | `mediaType` | Het type van media (zie _constanten MediaType_ hieronder) | Ja |

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

1. **verbind meta-gegevens**

   Koppel standaard- en/of aangepaste metagegevensobjecten optioneel aan de volgende sessie via variabelen voor contextgegevens.

   * **Standaard meta-gegevens**

     [Standaardmetadata implementeren in Android](/help/use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)

     >[!NOTE]
     >
     >Het koppelen van het standaardobject voor metagegevens aan het mediaobject is optioneel.

      * De APIVerwijzing van de meta-gegevens van media sleutels - [&#x200B; Standaard meta-gegevenssleutels - Android &#x200B;](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
      * Zie de uitvoerige reeks van beschikbare videometagegevens hier: [&#x200B; Audio en videoparameters &#x200B;](/help/implementation/variables/audio-video-parameters.md)

   * **de meta-gegevens van de Douane**

     Maak een woordenboek voor de aangepaste variabelen en vul de gegevens voor deze media in. Bijvoorbeeld:

     ```java
     HashMap<String, String> mediaMetadata =  
       new HashMap<String, String>();
     mediaMetadata.put("isUserLoggedIn", "false");
     mediaMetadata.put("tvStation", "Sample TV Station");
     mediaMetadata.put("programmer", "Sample programmer");
     ```

1. **Spoor de intentie om playback** te beginnen

   Als u een mediasessie wilt bijhouden, roept u `trackSessionStart` aan op de Media Heartbeat-instantie. Bijvoorbeeld:

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
   >In `trackSessionStart` wordt bijgehouden wat de gebruiker wil afspelen, niet het begin van het afspelen. Deze API wordt gebruikt om de media gegevens/meta-gegevens te laden en tijd-aan-begin metrische QoS (de tijdduur tussen `trackSessionStart` en `trackPlay`) te schatten.

   >[!NOTE]
   >
   >Als u geen metagegevens van aangepaste media gebruikt, verzendt u gewoon een leeg object voor het tweede argument in `trackSessionStart` .

1. **spoor het daadwerkelijke begin van playback**

   Identificeer de gebeurtenis van de media speler voor het begin van media playback, waar het eerste kader van media op het scherm wordt teruggegeven, en roep `trackPlay`:

   ```java
   // Video is rendered on the screen) and call trackPlay.  
   public void onVideoPlay(Observable observable, Object data) {
       _heartbeat.trackPlay();
   }
   ```

1. **Spoor de voltooiing van playback**

   Identificeer de gebeurtenis van de media speler voor de voltooiing van media playback, waar de gebruiker de inhoud tot het eind heeft bekeken, en roep `trackComplete`:

   ```java
   public void onVideoComplete(Observable observable, Object data) {
       _heartbeat.trackComplete();
   }
   ```

1. **Spoor het eind van de zitting**

   Identificeer de gebeurtenis van de mediaspeler voor het verwijderen/sluiten van het afspelen van de media, waarbij de gebruiker de media en/of de media sluit en verwijderd is, en roep `trackSessionEnd` aan:

   ```java
   // Closes the media and/or the media completed and unloaded,  
   // and call trackSessionEnd().  
   public void onMainVideoUnload(Observable observable, Object data) {  
       _heartbeat.trackSessionEnd();
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` markeert het einde van een mediatrackingsessie. Als de sessie succesvol is gecontroleerd op voltooiing, waarbij de gebruiker de inhoud tot het einde heeft gecontroleerd, controleert u of `trackComplete` vóór `trackSessionEnd` is aangeroepen. Elke andere API-aanroep van `track*` wordt na `trackSessionEnd` genegeerd, behalve voor `trackSessionStart` voor een nieuwe sessie voor mediatracering.

1. **spoor alle mogelijke pauzescenario&#39;s**

   Identificeer de gebeurtenis van de media speler voor media pauzeren en roepen `trackPause`:

   ```java
   public void onVideoPause(Observable observable, Object data) {  
       _heartbeat.trackPause();
   }
   ```

   **Scenario&#39;s van de Pauze**

   Identificeer om het even welk scenario waarin VideoPlayer zal pauzeren en zorg ervoor dat `trackPause` behoorlijk wordt geroepen. De volgende scenario&#39;s vereisen allemaal dat uw app `trackPause()` aanroept:

   * De gebruiker raakt expliciet de pauze in de app.
   * De speler plaatst zichzelf in de pauzestatus.
   * (*Mobiele Apps*) - de gebruiker zet de toepassing in de achtergrond, maar u wilt dat app de zitting open houdt.
   * (*Mobiele Apps*) - om het even welk type van systeem onderbreekt komt voor dat een toepassing veroorzaakt om worden gesteund. Bijvoorbeeld, ontvangt de gebruiker een vraag, of een pop-up van een andere toepassing komt voor, maar u wilt de toepassing de zitting levend houden om de gebruiker de kans te geven om de media van het punt van onderbreking te hervatten.

1. Identificeer de gebeurtenis van de speler voor media spel en/of media hervat van pauze en vraag `trackPlay`.

   ```java
   // trackPlay()
   public void onVideoPlay(Observable observable, Object data) {  
       _heartbeat.trackPlay();
   }
   ```

   >[!TIP]
   >
   >Dit kan de zelfde gebeurtenisbron zijn die in Stap 4 werd gebruikt. Zorg ervoor dat elke API-aanroep van `trackPause()` wordt gekoppeld aan een volgende API-aanroep van `trackPlay()` wanneer het afspelen van het mediabestand wordt hervat.

Raadpleeg de volgende secties voor meer informatie over het bijhouden van het afspelen van core:

* Het volgen scenario&#39;s: [&#x200B; de playback van VOD zonder advertenties &#x200B;](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* Voorbeeld van een voorbeeldspeler die bij de Android SDK wordt geleverd voor een volledig voorbeeld van &#39;tracking&#39;.
