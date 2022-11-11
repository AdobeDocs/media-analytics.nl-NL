---
title: Meer informatie over het volgen van advertenties op Android
description: Implementeer en volg in Android-toepassingen met behulp van de Media SDK.
uuid: 4a4249fb-dc39-4947-a14d-a51d972f32d4
exl-id: 1f96dde9-c924-4fce-8b14-7dec7137f265
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 4%

---

# Advertenties bijhouden op Android{#track-ads-on-android}

De volgende instructies bieden richtlijnen voor implementatie met behulp van de 2.x SDK&#39;s.

>[!IMPORTANT]
>
>Als u een 1.x-versie van de SDK implementeert, kunt u hier de 1.x-handleidingen voor ontwikkelaars downloaden: [SDK&#39;s downloaden.](/help/getting-started/download-sdks.md)

## Constanten voor bijhouden van advertenties

| Naam van constante | Beschrijving |
| --- | --- |
| `MediaHeartbeat.Event.AdBreakStart` | Constante voor het bijhouden van de gebeurtenis AdBreak Start |
| `MediaHeartbeat.Event.AdBreakComplete` | Constante voor het bijhouden van de gebeurtenis AdBreak Complete |
| `MediaHeartbeat.Event.AdStart` | Constante voor het bijhouden van de gebeurtenis Ad Start |
| `MediaHeartbeat.Event.AdComplete` | Constante voor het bijhouden van de gebeurtenis Advertentie voltooid |
| `MediaHeartbeat.Event.AdSkip` | Constante voor het bijhouden van de gebeurtenis Advertentie overslaan |

## Uitvoeringsstappen

1. Identificeer wanneer de grens van de advertentie begint, met inbegrip van pre-rol, en creeer een `AdBreakObject` met behulp van de informatie over het advertentieeinde.

   `AdBreakObject` referentie:

   | Naam variabele | Beschrijving | Vereist |
   | --- | --- | :---: |
   | `name` | De naam van het invoegpunt, zoals pre-roll, mid-roll en post-roll. | Ja |
   | `position` | De getalpositie van het advertentierak binnen de inhoud, beginnend met 1. | Ja |
   | `startTime` | Waarde van afspeelkop aan het begin van het advertentieeinde. | Ja |

   Object maken van einde toevoegen:

   ```java
   MediaObject adBreakInfo =  
     MediaHeartbeat.createAdBreakObject(<ADBREAK_NAME>,  
                                        <POSITION>,  
                                        <START_TIME>);
   ```

1. Bellen `trackEvent()` with `AdBreakStart` in de `MediaHeartbeat` -instantie om het ad-einde te volgen:

   ```java
   public void onAdBreakStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart,  
                             adBreakInfo,  
                             null);
   }
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

   ```java
   MediaObject adInfo =  
     MediaHeartbeat.createAdObject(<AD_NAME>
                                   <AD_ID>,  
                                   <POSITION>,  
                                   <LENGTH>);
   ```

1. Voeg desgewenst standaard- en/of advertentiemetagegevens toe aan de mediatraceringssessie via de variabelen van de contextgegevens.

   * [Standaardmetadata voor advertenties implementeren in Android](/help/use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)

   help/use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md

   * **Aangepaste en metagegevens -** Voor aangepaste metagegevens maakt u een variabelenobject voor de aangepaste gegevensvariabelen en vult u de gegevens voor de huidige advertentie in:

      ```java
      // Setting Ad Metadata
      HashMap<String, String> adMetadata = new HashMap<String, String>();
      adMetadata.put("affiliate", "Sample affiliate");
      adMetadata.put("campaign", "Sample ad campaign");
      ```


1. Bellen `trackEvent()` met de `AdStart` in de `MediaHeartbeat` -instantie om het afspelen van de advertentie te volgen.

   Neem een verwijzing naar de aangepaste metagegevensvariabele (of een leeg object) op als de derde parameter in de gebeurtenisaanroep:

   ```java
   public void onAdStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdStart,  
                             adInfo,  
                             adMetadata);
   }
   ```

1. Wanneer het afspelen van de advertentie het einde van de advertentie heeft bereikt, roept u `trackEvent()` met de `AdComplete` gebeurtenis:

   ```java
   public void onAdComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdComplete, null, null);
   }
   ```

1. Als het afspelen van de advertentie niet is voltooid omdat de gebruiker de advertentie heeft overgeslagen, voert u de `AdSkip` gebeurtenis:

   ```java
   public void onAdSkip(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdSkip, null, null);
   }
   ```

1. Als er extra advertenties zijn binnen dezelfde `AdBreak`Herhaal stap 3 tot en met 7 opnieuw.
1. Wanneer het advertentieeinde is voltooid, gebruikt u de `AdBreakComplete` te volgen gebeurtenis:

   ```java
   public void onAdBreakComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete, null, null);
   }
   ```

Zie het volgende scenario [VOD afspelen met pre-roll-advertenties](/help/use-cases/tracking-scenarios/vod-preroll-ads.md) voor meer informatie .
