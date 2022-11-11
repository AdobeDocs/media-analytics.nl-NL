---
title: Leer hoe u advertenties kunt bijhouden met JavaScript 3.x
description: Implementeer en volg in browser (JS) toepassingen gebruikend Media SDK.
exl-id: 6b34b2c0-5e50-471a-b52c-b9c760fa3169
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 3%

---

# Advertenties bijhouden met JavaScript 3.x{#track-ads-on-javascript}

De volgende instructies bieden richtlijnen voor implementatie met behulp van de 3.x SDK&#39;s.

>[!IMPORTANT]
>
>Als u eerdere versies van de SDK implementeert, kunt u de ontwikkelaarsgidsen hier downloaden: [SDK&#39;s downloaden.](/help/getting-started/download-sdks.md)

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

   | Naam variabele | Type | Beschrijving |
   | --- | --- | --- |
   | `name` | string | Niet-lege tekenreeks die de naam van het invoegpunt aangeeft (vóór, na en na de rol). |
   | `position` | getal | De getalpositie van het advertentiespoor dat met 1 begint. |
   | `startTime` | getal | Waarde van afspeelkop aan het begin van het advertentieeinde. |

   Object maken van einde toevoegen:

   ```js
   var adBreakObject =
     ADB.Media.createAdBreakObject(<ADBREAK_NAME>,
                                      <POSITION>,
                                      <START_TIME>);
   ```

1. Bellen `trackEvent()` with `AdBreakStart` in de `MediaHeartbeat` -instantie om het ad-einde te volgen:

   ```js
   tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakObject);
   ```

1. Identificeer wanneer de advertentie begint en creeer `AdObject` -instantie die de advertentiegegevens gebruikt.

   `AdObject` referentie:

   | Naam variabele | Type | Beschrijving |
   | --- | --- | --- |
   | `name` | string | Niet-lege tekenreeks die de naam van de advertentie aangeeft. |
   | `adId` | string | Niet-lege tekenreeksaanduiding en id. |
   | `position` | getal | De getalpositie van de advertentie binnen het invoegpunt, te beginnen met 1. |
   | `length` | getal | Positief getal dat de lengte van de advertentie aangeeft. |

   Object maken toevoegen:

   ```js
   var adObject =
     ADB.Media.createAdObject.createAdObject(<AD_NAME>,
                                   <AD_ID>,
                                   <POSITION>,
                                   <LENGTH>);
   ```

1. Voeg desgewenst standaard- en/of advertentiemetagegevens toe aan de mediatraceringssessie via de variabelen van de contextgegevens.

   * [Standaardmetadata voor advertenties implementeren in JavaScript](/help/use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
   * **Aangepaste en metagegevens -** Voor aangepaste metagegevens maakt u een variabelenobject voor de aangepaste gegevensvariabelen en vult u de gegevens voor de huidige advertentie in:

      ```js
      /* Set context data */
      // Standard metadata keys provided by adobe.
      adMetadata[ADB.Media.AdMetadataKeys]  ="Sample Advertiser";
      adMetadata[ADB.Media.AdMetadataKeys] = "Sample Campaign";
      
      // Custom metadata keys
      adMetadata["affiliate"] = "Sample affiliate";
      adMetadata["campaign"] = "Sample ad campaign";
      adMetadata["creative"] = "Sample creative";
      ```

1. Bellen `trackEvent()` met de `AdStart` in de `MediaHeartbeat` -instantie om het afspelen van de advertentie te volgen.

   Neem een verwijzing naar de aangepaste metagegevensvariabele (of een leeg object) op als de derde parameter in de gebeurtenisaanroep:

   ```js
   _onAdStart = function() {
       tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);
   };
   ```

1. Wanneer het afspelen van de advertentie het einde van de advertentie heeft bereikt, roept u `trackEvent()` met de `AdComplete` gebeurtenis:

   ```js
   _onAdComplete = function() {
       tracker.trackEvent(ADB.Media.Event.AdComplete);
   };
   ```

1. Als het afspelen van de advertentie niet is voltooid omdat de gebruiker de advertentie heeft overgeslagen, voert u de `AdSkip` gebeurtenis:

   ```js
   _onAdSkip = function() {
       tracker.trackEvent(ADB.Media.Event.AdSkip);
   };
   ```

1. Als er extra advertenties zijn binnen dezelfde `AdBreak`Herhaal stap 3 tot en met 7 opnieuw.
1. Wanneer het advertentieeinde is voltooid, gebruikt u de `AdBreakComplete` te volgen gebeurtenis:

   ```js
   _onAdBreakComplete = function() {
       tracker.trackEvent(ADB.Media.Event.AdBreakComplete);
   };
   ```

Zie het volgende scenario [VOD afspelen met pre-roll-advertenties](/help/use-cases/tracking-scenarios/vod-preroll-ads.md) voor meer informatie .
