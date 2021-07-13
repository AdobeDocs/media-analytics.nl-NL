---
title: Leer hoe je advertenties kunt bijhouden op Roku
description: Implementeer en tracking in Roku-toepassingen met de SDK van Media.
uuid: b1567265-7043-4efa-a313-aaaa91c4bb01
exl-id: aaed828d-1aba-486e-83e3-2ffd092305e2
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 3%

---

# Advertenties bijhouden op Roku{#track-ads-on-roku}

>[!IMPORTANT]
>
>De volgende instructies bieden richtlijnen voor implementatie met behulp van de 2.x SDK&#39;s. Als u een 1.x-versie van de SDK implementeert, kunt u hier de 1.x-handleidingen voor ontwikkelaars downloaden: [SDK&#39;s downloaden.](/help/sdk-implement/download-sdks.md)

## Constanten voor bijhouden van advertenties

| Naam van constante | Beschrijving   |
|---|---|
| `AdBreakStart` | Constante voor het bijhouden van de gebeurtenis AdBreak Start |
| `AdBreakComplete` | Constante voor het bijhouden van de gebeurtenis AdBreak Complete |
| `AdStart` | Constante voor het bijhouden van de gebeurtenis Ad Start |
| `AdComplete` | Constante voor het bijhouden van de gebeurtenis Advertentie voltooid |
| `AdSkip` | Constante voor het bijhouden van de gebeurtenis Advertentie overslaan |

## Uitvoeringsstappen

1. Bepaal wanneer de grens van de advertentierak begint, met inbegrip van pre-rol, en creeer `AdBreakObject` door de informatie van de advertentierak te gebruiken.

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

1. Roep `trackEvent()` met `AdBreakStart` in de `MediaHeartbeat` instantie aan om het advertentiesonderbreking te volgen:

   ```
   contextData = {} 
   ADBMobile().mediaTrackEvent(MEDIA_AD_BREAK_START, adBreakInfo, contextData)
   ```

1. Identificeer wanneer het advertentiemiddel begint en creeer een `AdObject` instantie gebruikend de advertentieinformatie.

   ```
   adInfo =  
     adb_media_init_adinfo(ad.title,  
                           ad.id,  
                           ad.position,  
                           ad.duration) 
   ```

1. Voeg desgewenst standaard- en/of advertentiemetagegevens toe aan de mediatraceringssessie via de variabelen van de contextgegevens.

   * [Standaardmetadata voor advertenties implementeren in Roku](/help/sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   * **Aangepast en metagegevens -** Voor aangepaste metagegevens maakt u een variabelenobject voor de aangepaste gegevensvariabelen en vult u de gegevens voor het huidige ad-element in:

      ```
      contextData = {} 
      contextData["adinfo1"] = "adinfo2" 
      contextData["adinfo2"] = "adinfo2"
      ```

1. Roep `trackEvent()` met de gebeurtenis `AdStart` in de instantie `MediaHeartbeat` aan om het afspelen van de advertentie te volgen:

   ```
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_START, adInfo, contextData)
   ```

1. Wanneer het afspelen van het advertentiemiddel het einde van de advertentie bereikt, roept u `trackEvent()` aan met de gebeurtenis `AdComplete`.

   ```
   standardAdMetadata = {} 
   contextData = {} 
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_COMPLETE, adInfo, contextData)
   ```

1. Als het afspelen van de advertentie niet is voltooid omdat de gebruiker de advertentie heeft overgeslagen, houdt u de gebeurtenis `AdSkip` bij:

   ```
   contextData = {} 
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_SKIP, adInfo, contextData
   ```

1. Herhaal stap 3 tot en met 7 als er extra advertenties binnen dezelfde `AdBreak` zijn.
1. Wanneer het ad-einde is voltooid, gebruikt u de gebeurtenis `AdBreakComplete` om te volgen:

   ```
   contextData = {} 
   ADBMobile().mediaTrackEvent(MEDIA_AD_BREAK_COMPLETE, adBreakInfo, contextData)
   ```

Zie het volgende scenario [VOD playback met pre-rol advertenties](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md) voor meer informatie.
