---
title: Advertenties bijhouden op Chromecast
description: Implementeer en tracking in Chromecast-toepassingen met de SDK van Media.
uuid: 7b1f584a-3472-416c-944c-5f5ea0ee5529
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Advertenties bijhouden op Chromecast{#track-ads-on-chromecast}

>[!IMPORTANT]
>
>De volgende instructies bieden richtlijnen voor implementatie met behulp van de 2.x SDK&#39;s. Als u een 1.x-versie van de SDK implementeert, kunt u hier de 1.x-handleidingen voor ontwikkelaars downloaden: SDK&#39;s [downloaden.](/help/sdk-implement/download-sdks.md)

## Constanten voor bijhouden van advertenties

| Naam van constante | Beschrijving |
|---|---|
| `AdBreakStart` | Constante voor het bijhouden van de gebeurtenis AdBreak Start |
| `AdBreakComplete` | Constante voor het bijhouden van de gebeurtenis AdBreak Complete |
| `AdStart` | Constante voor het bijhouden van de gebeurtenis Ad Start |
| `AdComplete` | Constante voor het bijhouden van de gebeurtenis Advertentie voltooid |
| `AdSkip` | Constante voor het bijhouden van de gebeurtenis Advertentie overslaan |

## Uitvoeringsstappen

1. Bepaal wanneer de grens van de advertentierak begint, met inbegrip van pre-rol, en creeer een `AdBreakObject` door de informatie van de advertentierak te gebruiken.

   Object maken van einde toevoegen: [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createAdBreakObject)

   ```
   adBreakInfo = ADBMobile.media.createAdBreakObject("First Ad-Break", 1, AD_BREAK_START_TIME, playerName); 
   ```

1. Roep `trackEvent()` met `AdBreakStart` in de `MediaHeartbeat` instantie aan begin het volgen van de advertentie onderbreking: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakStart, getAdBreakInfo());
   ```

1. Identificeer wanneer het advertentiemiddel begint en creeer een `AdObject` geval gebruikend de advertentieinformatie.

   Object maken toevoegen: [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createAdObject)

   ```
   adInfo = ADBMobile.media.createAdObject("Sample ad", "001", 1, AD_LENGTH); 
   ```

1. Voeg desgewenst standaard- en/of advertentiemetagegevens toe aan de mediatraceringssessie via de variabelen van de contextgegevens.

   * **Standaard en metagegevens -** Voor standaard- en metagegevens maakt u een woordenboek van standaard- en metagegevenssleutelwaardeparen met behulp van de toetsen voor uw platform:
   * **Aangepast en metagegevens -** Voor aangepaste metagegevens maakt u een variabel object voor de aangepaste gegevensvariabelen en vult u de gegevens voor het huidige ad-element in:

1. Bel `trackEvent()` met de `AdStart` gebeurtenis om het afspelen van de advertentie te volgen.

   Neem een verwijzing naar de aangepaste metagegevensvariabele (of een leeg object) op als de derde parameter in de gebeurtenisaanroep: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, getAdInfo(), adContextData);
   ```

1. Wanneer het afspelen van het advertentiemiddel het einde van de advertentie bereikt, roept u `trackEvent()` de `AdComplete` gebeurtenis aan: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdComplete); 
   ```

1. Herhaal stap 3 tot en met 6 opnieuw als er extra advertenties binnen dezelfde `AdBreak`advertentie zijn.
1. Wanneer het advertentieeinde is voltooid, gebruikt u de `AdBreakComplete` gebeurtenis om te volgen: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakComplete, getAdBreakInfo());
   ```

Zie het volgende scenario [VOD playback met pre-rol advertenties](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md) voor meer informatie.
