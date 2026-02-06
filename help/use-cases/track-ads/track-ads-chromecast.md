---
title: Meer informatie over het volgen van advertenties op Chromecast
description: Implementeer en tracking in Chromecast-toepassingen met de Media SDK.
uuid: 7b1f584a-3472-416c-944c-5f5ea0ee5529
exl-id: 57465c42-b349-439d-b8d7-083b299a8c83
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---

# Advertenties bijhouden op Chromecast{#track-ads-on-chromecast}

De volgende instructies bieden richtlijnen voor implementatie met behulp van de 2.x SDK&#39;s.

>[!IMPORTANT]
>
>Als u een 1.x versie van SDK uitvoert, kunt u 1.x de Gidsen van Ontwikkelaars hier downloaden: [ Download SDKs.](/help/getting-started/download-sdks.md)

## Constanten voor bijhouden van advertenties

| Naam van constante | Beschrijving   |
|---|---|
| `AdBreakStart` | Constante voor het bijhouden van de gebeurtenis AdBreak Start |
| `AdBreakComplete` | Constante voor het bijhouden van de gebeurtenis AdBreak Complete |
| `AdStart` | Constante voor het bijhouden van de gebeurtenis Ad Start |
| `AdComplete` | Constante voor het bijhouden van de gebeurtenis Advertentie voltooid |
| `AdSkip` | Constante voor het bijhouden van de gebeurtenis Advertentie overslaan |

## Implementatiestappen

1. Bepaal wanneer de grens van de advertentieruimte begint, met inbegrip van pre-rol, en creeer `AdBreakObject` door de informatie van de advertentierak te gebruiken.

   De verwezenlijking van het onderbrekingsvoorwerp van de hulp: [ createAdBreakObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createAdBreakObject)

   ```
   adBreakInfo = ADBMobile.media.createAdBreakObject("First Ad-Break", 1, AD_BREAK_START_TIME, playerName);
   ```

1. Vraag `trackEvent()` met `AdBreakStart` in de `MediaHeartbeat` instantie beginnen het volgen van de advertentie: [ trackEvent ](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakStart, getAdBreakInfo());
   ```

1. Bepaal wanneer het advertentie-element begint en maak een `AdObject` -instantie met behulp van de advertentie-informatie.

   De objecten van de Advertentie verwezenlijking: [ createAdObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createAdObject)

   ```
   adInfo = ADBMobile.media.createAdObject("Sample ad", "001", 1, AD_LENGTH);
   ```

1. Voeg desgewenst standaard- en/of advertentiemetagegevens toe aan de mediatraceringssessie via de variabelen van de contextgegevens.

   * **Standaard en meta-gegevens -** voor norm en meta-gegevens, creeer een woordenboek van standaard en de waardeparen van de meta-gegevens zeer belangrijk gebruikend de sleutels voor uw platform:
   * **Douane en meta-gegevens -** voor douanemetagegevens, creeer een veranderlijk voorwerp voor de variabelen van douanegegevens en bevolk met de gegevens voor het huidige ad activa:

1. Roep `trackEvent()` aan met de `AdStart` -gebeurtenis om het afspelen van de advertentie te volgen.

   Omvat een verwijzing naar uw veranderlijke douanemetagegevens (of een leeg voorwerp) als derde parameter in de gebeurtenisvraag: [ trackEvent ](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, getAdInfo(), adContextData);
   ```

1. Wanneer de advertentie activa playback het eind van de advertentie bereikt, vraag `trackEvent()` met de `AdComplete` gebeurtenis: [ trackEvent ](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdComplete);
   ```

1. Herhaal stap 3 tot en met 6 opnieuw als er extra advertenties binnen dezelfde `AdBreak` zijn.
1. Wanneer de advertentieonderbreking volledig is, gebruik de `AdBreakComplete` gebeurtenis om te volgen: [ trackEvent ](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakComplete, getAdBreakInfo());
   ```

Zie het volgende scenario [ de playback van VOD met pre-roladvertenties ](/help/use-cases/tracking-scenarios/vod-preroll-ads.md) voor meer informatie.
