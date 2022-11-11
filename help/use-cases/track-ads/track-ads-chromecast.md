---
title: Meer informatie over het volgen van advertenties op Chromecast
description: Implementeer en tracking in Chromecast-toepassingen met de SDK van Media.
uuid: 7b1f584a-3472-416c-944c-5f5ea0ee5529
exl-id: 57465c42-b349-439d-b8d7-083b299a8c83
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---

# Advertenties bijhouden op Chromecast{#track-ads-on-chromecast}

De volgende instructies bieden richtlijnen voor implementatie met behulp van de 2.x SDK&#39;s.

>[!IMPORTANT]
>
>Als u een 1.x-versie van de SDK implementeert, kunt u hier de 1.x-handleidingen voor ontwikkelaars downloaden: [SDK&#39;s downloaden.](/help/getting-started/download-sdks.md)

## Constanten voor bijhouden van advertenties

| Naam van constante | Beschrijving   |
|---|---|
| `AdBreakStart` | Constante voor het bijhouden van de gebeurtenis AdBreak Start |
| `AdBreakComplete` | Constante voor het bijhouden van de gebeurtenis AdBreak Complete |
| `AdStart` | Constante voor het bijhouden van de gebeurtenis Ad Start |
| `AdComplete` | Constante voor het bijhouden van de gebeurtenis Advertentie voltooid |
| `AdSkip` | Constante voor het bijhouden van de gebeurtenis Advertentie overslaan |

## Uitvoeringsstappen

1. Identificeer wanneer de grens van de advertentie begint, met inbegrip van pre-rol, en creeer een `AdBreakObject` met behulp van de informatie over het advertentieeinde.

   Object maken van einde toevoegen: [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createAdBreakObject)

   ```
   adBreakInfo = ADBMobile.media.createAdBreakObject("First Ad-Break", 1, AD_BREAK_START_TIME, playerName);
   ```

1. Bellen `trackEvent()` with `AdBreakStart` in de `MediaHeartbeat` -instantie om het ad-einde te volgen: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakStart, getAdBreakInfo());
   ```

1. Identificeer wanneer de advertentie begint en creeer een `AdObject` -instantie die de advertentiegegevens gebruikt.

   Object maken toevoegen: [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createAdObject)

   ```
   adInfo = ADBMobile.media.createAdObject("Sample ad", "001", 1, AD_LENGTH);
   ```

1. Voeg desgewenst standaard- en/of advertentiemetagegevens toe aan de mediatraceringssessie via de variabelen van de contextgegevens.

   * **Standaard en metagegevens -** Voor standaard- en metagegevens maakt u een woordenboek van standaard- en metagegevenssleutelwaardeparen met behulp van de toetsen voor uw platform:
   * **Aangepaste en metagegevens -** Voor aangepaste metagegevens maakt u een variabelenobject voor de aangepaste gegevensvariabelen en vult u de gegevens voor het huidige ad-element in:

1. Bellen `trackEvent()` met de `AdStart` om het afspelen van de advertentie te volgen.

   Neem een verwijzing naar de aangepaste metagegevensvariabele (of een leeg object) op als de derde parameter in de gebeurtenisaanroep: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, getAdInfo(), adContextData);
   ```

1. Wanneer het afspelen van het advertentiemiddel het einde van de advertentie bereikt, roept u `trackEvent()` met de `AdComplete` gebeurtenis: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdComplete);
   ```

1. Als er extra advertenties zijn binnen dezelfde `AdBreak`Herhaal stap 3 tot en met 6 opnieuw.
1. Wanneer het advertentieeinde is voltooid, gebruikt u de `AdBreakComplete` te volgen gebeurtenis: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakComplete, getAdBreakInfo());
   ```

Zie het volgende scenario [VOD afspelen met pre-roll-advertenties](/help/use-cases/tracking-scenarios/vod-preroll-ads.md) voor meer informatie .
