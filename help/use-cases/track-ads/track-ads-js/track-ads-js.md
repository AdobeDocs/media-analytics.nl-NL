---
title: Leer hoe u advertenties kunt bijhouden met JavaScript 2.x
description: Implementeer en volg in browser (JS) toepassingen gebruikend Media SDK.
uuid: 4d81d29c-c55d-4d48-b505-3260922712ff
exl-id: 4404d3a6-ab98-40f0-9573-ee32f480f650
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 4%

---

# Advertenties bijhouden met JavaScript 2.x{#track-ads-on-javascript}

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

   `AdBreakObject` referentie:

   | Naam variabele | Beschrijving | Vereist |
   | --- | --- | :---: |
   | `name` | De naam van het invoegpunt, zoals pre-roll, mid-roll en post-roll. | Ja |
   | `position` | De getalpositie van het advertentiespoor dat met 1 begint. | Ja |
   | `startTime` | Waarde van afspeelkop aan het begin van het advertentieeinde. | Ja |

   Object maken van einde toevoegen:

   ```js
   var adBreakObject =  
     MediaHeartbeat.createAdBreakObject(<ADBREAK_NAME>,  
                                        <POSITION>,  
                                        <START_TIME>);
   ```

1. Bellen `trackEvent()` with `AdBreakStart` in de `MediaHeartbeat` -instantie om het ad-einde te volgen:

   ```js
   mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);
   ```

1. Identificeer wanneer de advertentie begint en creeer `AdObject` -instantie die de advertentiegegevens gebruikt.

   `AdObject` referentie:

   | Naam variabele | Beschrijving | Vereist |
   | --- | --- | :---: |
   | `name` | Vriendelijke naam van de advertentie. | Ja |
   | `adId` | De unieke id voor de advertentie. | Ja |
   | `position` | De numerieke positie van de advertentie binnen het advertentiespoor, beginnend met 1. | Ja |
   | `length` | Ad-lengte | Ja |

   Object maken toevoegen:

   ```js
   var adObject =  
     MediaHeartbeat.createAdObject(<AD_NAME>,  
                                   <AD_ID>,  
                                   <POSITION>,  
                                   <LENGTH>);
   ```

1. Voeg desgewenst standaard- en/of advertentiemetagegevens toe aan de mediatraceringssessie via de variabelen van de contextgegevens.

   * [Standaardmetadata voor advertenties implementeren in JavaScript](/help/use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js.md)
   * **Aangepaste en metagegevens -** Voor aangepaste metagegevens maakt u een variabelenobject voor de aangepaste gegevensvariabelen en vult u de gegevens voor de huidige advertentie in:

      ```js
      /* Set custom context data */
      var adCustomMetadata = {
          affiliate: "Sample affiliate",
          campaign: "Sample ad campaign",
          creative: "Sample creative"
      };
      ```

1. Bellen `trackEvent()` met de `AdStart` in de `MediaHeartbeat` -instantie om het afspelen van de advertentie te volgen.

   Neem een verwijzing naar de aangepaste metagegevensvariabele (of een leeg object) op als de derde parameter in de gebeurtenisaanroep:

   ```js
   _onAdStart = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart,  
                                       adObject,  
                                       adCustomMetadata);
   };
   ```

1. Wanneer het afspelen van de advertentie het einde van de advertentie heeft bereikt, roept u `trackEvent()` met de `AdComplete` gebeurtenis:

   ```js
   _onAdComplete = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete);
   };
   ```

1. Als het afspelen van de advertentie niet is voltooid omdat de gebruiker de advertentie heeft overgeslagen, voert u de `AdSkip` gebeurtenis:

   ```js
   _onAdSkip = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip);
   };
   ```

1. Als er extra advertenties zijn binnen dezelfde `AdBreak`Herhaal stap 3 tot en met 7 opnieuw.
1. Wanneer het advertentieeinde is voltooid, gebruikt u de `AdBreakComplete` te volgen gebeurtenis:

   ```js
   _onAdBreakComplete = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete);
   };
   ```

Zie het volgende scenario [VOD afspelen met pre-roll-advertenties](/help/use-cases/tracking-scenarios/vod-preroll-ads.md) voor meer informatie .
