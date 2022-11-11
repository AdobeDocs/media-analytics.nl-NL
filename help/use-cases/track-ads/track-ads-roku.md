---
title: Leer hoe je advertenties kunt bijhouden op Roku
description: Implementeer en tracking in Roku-toepassingen met de SDK van Media.
uuid: b1567265-7043-4efa-a313-aaaa91c4bb01
exl-id: aaed828d-1aba-486e-83e3-2ffd092305e2
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 3%

---

# Advertenties bijhouden op Roku{#track-ads-on-roku}

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

   ```
   ‘ Create an adbreak info object
   adBreakInfo = adb_media_init_adbreakinfo()
   adBreakInfo.name = <ADBREAK_NAME>
   adBreakInfo.startTime = <START_TIME>
   adBreakInfo.position = <POSITION>
   ```

1. Bellen `trackEvent()` with `AdBreakStart` in de `MediaHeartbeat` -instantie om het ad-einde te volgen:

   ```
   contextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_AD_BREAK_START, adBreakInfo, contextData)
   ```

1. Identificeer wanneer de advertentie begint en creeer een `AdObject` -instantie die de advertentiegegevens gebruikt.

   ```
   adInfo =  
     adb_media_init_adinfo(ad.title,  
                           ad.id,  
                           ad.position,  
                           ad.duration)
   ```

1. Voeg desgewenst standaard- en/of advertentiemetagegevens toe aan de mediatraceringssessie via de variabelen van de contextgegevens.

   * [Standaardmetadata voor advertenties implementeren in Roku](/help/use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   * **Aangepaste en metagegevens -** Voor aangepaste metagegevens maakt u een variabelenobject voor de aangepaste gegevensvariabelen en vult u de gegevens voor het huidige ad-element in:

      ```
      contextData = {}
      contextData["adinfo1"] = "adinfo2"
      contextData["adinfo2"] = "adinfo2"
      ```

1. Bellen `trackEvent()` met de `AdStart` in de `MediaHeartbeat` -instantie om het afspelen van de advertentie te volgen:

   ```
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_START, adInfo, contextData)
   ```

1. Wanneer het afspelen van het advertentiemiddel het einde van de advertentie bereikt, roept u `trackEvent()` met de `AdComplete` gebeurtenis.

   ```
   standardAdMetadata = {}
   contextData = {}
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_COMPLETE, adInfo, contextData)
   ```

1. Als het afspelen van de advertentie niet is voltooid omdat de gebruiker de advertentie heeft overgeslagen, voert u de `AdSkip` gebeurtenis:

   ```
   contextData = {}
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_SKIP, adInfo, contextData
   ```

1. Als er extra advertenties zijn binnen dezelfde `AdBreak`Herhaal stap 3 tot en met 7 opnieuw.
1. Wanneer het advertentieeinde is voltooid, gebruikt u de `AdBreakComplete` te volgen gebeurtenis:

   ```
   contextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_AD_BREAK_COMPLETE, adBreakInfo, contextData)
   ```

Zie het volgende scenario [VOD afspelen met pre-roll-advertenties](/help/use-cases/tracking-scenarios/vod-preroll-ads.md) voor meer informatie .
