---
title: Leer hoe u het afspelen van de kern kunt bijhouden op Chromecast
description: Leer hoe u core tracking implementeert met Media SDK op Chromecast.
uuid: a9fc59d8-a2f4-4889-bdec-55c42a835d06
exl-id: 9812d06d-9efd-460c-a626-6a15f61a4c35
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 0%

---

# Core playback van het spoor op Chromecast{#track-core-playback-on-chromecast}

Deze documentatie behandelt het volgen in versie 2.x van de SDK.

>[!IMPORTANT]
>
>Als u een 1.x versie van SDK uitvoert, kunt u 1.x de Gidsen van Ontwikkelaars hier downloaden: [&#x200B; Download SDKs &#x200B;](/help/getting-started/download-sdks.md)

1. **Aanvankelijke het volgen opstelling**

   Bepaal wanneer de gebruiker de afspeelintentie activeert (de gebruiker klikt op Afspelen en/of Automatisch afspelen is ingeschakeld) en maak een `MediaObject` -instantie.

   **`MediaObject`API-referentie:**

   [&#x200B; createMediaObject &#x200B;](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

   ```
   mediaObject = ADBMobile.media.createMediaObject(<name>, <id>, <duration>, <streamType>, <mediaType>);
   ```

   **`StreamType`constanten:**

   [&#x200B; ADBMobile Media &#x200B;](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.StreamType)

   **`MediaType`constanten:**

   [&#x200B; ADBMobile Media &#x200B;](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.MediaType)

1. **Band videometagegevens**

   U kunt standaard- en/of aangepaste metagegevensobjecten voor video&#39;s optioneel aan de volgende sessie koppelen via variabelen voor contextgegevens.

   * **Standaard videometa-gegevens**

     [Standaardmetadata implementeren in Chromecast](/help/use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)

     >[!NOTE]
     >
     >Het is optioneel om het standaardobject voor videometagegevens aan het mediaobject te koppelen.

   * **de meta-gegevens van de Douane**

     Maak een veranderlijk object voor de douanevariabelen en bevolk met de gegevens voor deze video. Bijvoorbeeld:

     ```js
     /* Set custom context data */
     var customVideoMetadata = {
         isUserLoggedIn: "false",
         tvStation: "Sample TV station",
         programmer: "Sample programmer"
     };
     ```

1. **Spoor de intentie om playback** te beginnen

   Beginnen het volgen van een media zitting, vraag [&#x200B; trackSessionStart &#x200B;](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionStart) op het `media` voorwerp.

   ```
   ADBMobile.media.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!IMPORTANT]
   >
   >In `trackSessionStart` wordt bijgehouden wat de gebruiker wil afspelen, niet het begin van het afspelen. Deze API wordt gebruikt om de videogegevens/meta-gegevens te laden en tijd-aan-begin metrische QoS (de tijdduur tussen `trackSessionStart` en `trackPlay`) te schatten.

   >[!NOTE]
   >
   >De tweede waarde is de aangepaste objectnaam voor videometagegevens die u in stap 2 hebt gemaakt. Als u geen aangepaste videometagegevens gebruikt, verzendt u gewoon een leeg object voor het argument `data` in `trackSessionStart` , zoals getoond in de regel met opmerkingen in het bovenstaande iOS-voorbeeld.

1. **spoor het daadwerkelijke begin van playback**

   Identificeer de gebeurtenis van de videospeler voor het begin van de videoplayback, waar het eerste kader van de video op het scherm wordt teruggegeven, en vraag [&#x200B; trackPlay:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPlay)

   ```
   ADBMobile.media.trackPlay();
   ```

1. **de waarde van de Update playhead**

   Wijzig de positiewaarde van `mediaUpdatePlayhead` meerdere keren wanneer de afspeelkop verandert. <br /> Voor video-op-verzoek (VOD) wordt de waarde opgegeven in seconden vanaf het begin van het media-item. <br /> Als de speler voor live streaming geen informatie geeft over de duur van de inhoud, kan de waarde worden opgegeven als het aantal seconden sinds middernacht UTC van die dag.

   ```
   ADBMobile().media.updatePlayhead(position)
   ```

   >[!NOTE]
   >
   >Houd rekening met het volgende wanneer u de API `media.updatePlayhead` aanroept:
   >* Wanneer u voortgangsmarkeringen gebruikt, is de duur van de inhoud vereist en moet de afspeelkop worden bijgewerkt als het aantal seconden vanaf het begin van het media-item, te beginnen met 0.
   >* Wanneer u media-SDK&#39;s gebruikt, moet u de `media.updatePlayhead` API minstens één keer per seconde aanroepen.

1. **Spoor de voltooiing van playback**

   Identificeer de gebeurtenis van de videospeler voor de voltooiing van de videoplayback, waar de gebruiker de inhoud tot het eind heeft bekeken, en vraag [&#x200B; trackComplete:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete)

   ```
   ADBMobile.media.trackComplete();
   ```

1. **Spoor het eind van de zitting**

   Identificeer de gebeurtenis van de videospeler voor het ontladen/sluiten van de videoplayback, waar de gebruiker de video sluit en/of de video wordt voltooid en is gedownload, en vraag [&#x200B; trackSessionEnd:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionEnd)

   ```
   ADBMobile.media.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` markeert het einde van een videovervolgsessie. Als de sessie succesvol is gecontroleerd op voltooiing, waarbij de gebruiker de inhoud tot het einde heeft gecontroleerd, controleert u of `trackComplete` vóór `trackSessionEnd` is aangeroepen. Eventuele andere `track*` API-aanroepen worden na `trackSessionEnd` genegeerd, behalve voor `trackSessionStart` voor een nieuwe sessie voor het bijhouden van video.

1. **spoor alle mogelijke pauzescenario&#39;s**

   Identificeer de gebeurtenis van de videospeler voor videopauze en vraag [&#x200B; trackPause:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPause)

   ```
   ADBMobile.media.trackPause();
   ```

   **Scenario&#39;s van de Pauze**

   Identificeer om het even welk scenario waarin VideoPlayer zal pauzeren en zorg ervoor dat `trackPause` behoorlijk wordt geroepen. De volgende scenario&#39;s vereisen allemaal dat uw app `trackPause()` aanroept:

   * De gebruiker raakt expliciet de pauze in de app.
   * De speler plaatst zichzelf in de pauzestatus.
   * (*Mobiele Apps*) - de gebruiker zet de toepassing in de achtergrond, maar u wilt dat app de zitting open houdt.
   * (*Mobiele Apps*) - om het even welk type van systeem onderbreekt komt voor dat een toepassing veroorzaakt om worden gesteund. Bijvoorbeeld, ontvangt de gebruiker een vraag, of een pop-up van een andere toepassing komt voor, maar u wilt de toepassing de zitting levend houden om de gebruiker de kans te geven om de video van het punt van onderbreking te hervatten.

1. Identificeer de gebeurtenis van de speler voor videospel en/of videohervat van pauze en vraag [&#x200B; trackPlay:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete)

   ```
   ADBMobile.media.trackPlay();
   ```

   >[!TIP]
   >
   >Dit kan de zelfde gebeurtenisbron zijn die in Stap 4 werd gebruikt. Zorg ervoor dat elke API-aanroep van `trackPause()` wordt gekoppeld aan een volgende API-aanroep van `trackPlay()` wanneer het afspelen van de video wordt hervat.

* Het volgen scenario&#39;s: [&#x200B; de playback van VOD zonder advertenties &#x200B;](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* Voorbeeldspeler die bij de Chromecast SDK wordt geleverd voor een volledig voorbeeld van &#39;tracking&#39;.
