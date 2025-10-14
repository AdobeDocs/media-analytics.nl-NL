---
title: Meer informatie over het volgen van advertenties met JavaScript 3.x
description: Implementeer en volg in browser (JS) toepassingen gebruikend Media SDK.
exl-id: 6b34b2c0-5e50-471a-b52c-b9c760fa3169
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 1%

---

# Advertenties bijhouden met JavaScript 3.x{#track-ads-on-javascript}

De volgende instructies bieden richtlijnen voor implementatie met behulp van de 3.x SDK&#39;s.

>[!IMPORTANT]
>
>Als u om het even welke vorige versies van SDK uitvoert, kunt u de Gidsen van Ontwikkelaars hier downloaden: [&#x200B; Download SDKs.](/help/getting-started/download-sdks.md)

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

   `AdBreakObject` reference:

   | Naam variabele | Type | Beschrijving |
   | --- | --- | --- |
   | `name` | string | Niet-lege tekenreeks die de naam van het invoegpunt aangeeft (vóór, na en na de rol). |
   | `position` | getal | De getalpositie van het advertentiespoor dat met 1 begint. |
   | `startTime` | getal | Waarde van afspeelkop aan het begin van het advertentieeinde. |

   Object maken van advertentie-einde:

   ```js
   var adBreakObject =
     ADB.Media.createAdBreakObject(<ADBREAK_NAME>,
                                      <POSITION>,
                                      <START_TIME>);
   ```

1. Roep `trackEvent()` aan met `AdBreakStart` in de `MediaHeartbeat` -instantie om het ad-einde te volgen:

   ```js
   tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakObject);
   ```

1. Bepaal wanneer de advertentie begint en creeer een `AdObject` instantie gebruikend de advertentieinformatie.

   `AdObject` reference:

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

1. (Optioneel) Voeg standaard- en/of advertentiemetagegevens toe aan de mediatraceringssessie via de variabelen van de contextgegevens.

   * [Standaard en metagegevens implementeren op JavaScript](/help/use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
   * **Douane en meta-gegevens -** voor douanemetagegevens, creeer een veranderlijk voorwerp voor de variabelen van douanegegevens en bevolk met de gegevens voor de huidige advertentie:

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

1. Roep `trackEvent()` aan met de gebeurtenis `AdStart` in de instantie `MediaHeartbeat` om het afspelen van de advertentie te volgen.

   Neem een verwijzing naar de aangepaste metagegevensvariabele (of een leeg object) op als de derde parameter in de gebeurtenisaanroep:

   ```js
   _onAdStart = function() {
       tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);
   };
   ```

1. Wanneer het afspelen van de advertentie het einde van de advertentie heeft bereikt, roept u `trackEvent()` aan met de gebeurtenis `AdComplete` :

   ```js
   _onAdComplete = function() {
       tracker.trackEvent(ADB.Media.Event.AdComplete);
   };
   ```

1. Als het afspelen van de advertentie niet is voltooid omdat de gebruiker de advertentie heeft overgeslagen, houdt u de gebeurtenis `AdSkip` bij:

   ```js
   _onAdSkip = function() {
       tracker.trackEvent(ADB.Media.Event.AdSkip);
   };
   ```

1. Herhaal stap 3 tot en met 7 opnieuw als er extra advertenties binnen dezelfde `AdBreak` zijn.
1. Wanneer het ad-einde is voltooid, gebruikt u de gebeurtenis `AdBreakComplete` om bij te houden:

   ```js
   _onAdBreakComplete = function() {
       tracker.trackEvent(ADB.Media.Event.AdBreakComplete);
   };
   ```

Zie het volgende scenario [&#x200B; de playback van VOD met pre-roladvertenties &#x200B;](/help/use-cases/tracking-scenarios/vod-preroll-ads.md) voor meer informatie.

## Korrelige advertentie bijhouden

Het standaardinterval voor toevoegen en pingelen is `10 seconds` .

U kunt granulaire advertentie-tracking instellen om `1 second` ad tracking in te schakelen.

>[!IMPORTANT]
>
>Deze informatie moet worden verstrekt wanneer het beginnen van een volgende zitting.



**Syntaxis**

```javascript
ADB.Media.MediaObjectKey = {
   GranularAdTracking: "media.granularadtracking"
   }
```

**Voorbeeld**

```javascript
var mediaObject = ADB.Media.createMediaObject("media-name", "media-id", 60, ADB.Media.StreamType.VOD, ADB.Media.MediaType.Video);

// Enable granular ad tracking
mediaObject[ADB.Media.MediaObjectKey.GranularAdTracking] = true;

tracker.trackSessionStart(mediaObject);
```
