---
title: Advertenties bijhouden op Android
description: Implementeer en volg in Android-toepassingen met behulp van de Media SDK.
uuid: 4a4249fb-dc39-4947-a14d-a51d972f32d4
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Advertenties bijhouden op Android{#track-ads-on-android}

>[!IMPORTANT]
>
>De volgende instructies bieden richtlijnen voor implementatie met behulp van de 2.x SDK&#39;s. Als u een 1.x-versie van de SDK implementeert, kunt u hier de 1.x-handleidingen voor ontwikkelaars downloaden: SDK&#39;s [downloaden.](/help/sdk-implement/download-sdks.md)

## Constanten voor bijhouden van advertenties

| Naam van constante | Beschrijving |
| --- | --- |
| `MediaHeartbeat.Event.AdBreakStart` | Constante voor het bijhouden van de gebeurtenis AdBreak Start |
| `MediaHeartbeat.Event.AdBreakComplete` | Constante voor het bijhouden van de gebeurtenis AdBreak Complete |
| `MediaHeartbeat.Event.AdStart` | Constante voor het bijhouden van de gebeurtenis Ad Start |
| `MediaHeartbeat.Event.AdComplete` | Constante voor het bijhouden van de gebeurtenis Advertentie voltooid |
| `MediaHeartbeat.Event.AdSkip` | Constante voor het bijhouden van de gebeurtenis Advertentie overslaan |

## Uitvoeringsstappen

1. Bepaal wanneer de grens van de advertentierak begint, met inbegrip van pre-rol, en creeer een `AdBreakObject` door de informatie van de advertentierak te gebruiken.

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

1. Roep `trackEvent()` met `AdBreakStart` in de `MediaHeartbeat` instantie aan begin het volgen van de advertentie onderbreking:

   ```java
   public void onAdBreakStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart,  
                             adBreakInfo,  
                             null); 
   }
   ```

1. Bepaal wanneer de advertentie begint en creeer een `AdObject` instantie gebruikend de advertentieinformatie.

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

   * [Standaard- en metagegevens implementeren op Android](/help/sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
   * **Aangepast en metagegevens -** Voor aangepaste metagegevens maakt u een variabel object voor de aangepaste gegevensvariabelen en vult u de gegevens voor de huidige advertentie in:

      ```java
      // Setting Ad Metadata 
      HashMap<String, String> adMetadata = new HashMap<String, String>(); 
      adMetadata.put("affiliate", "Sample affiliate"); 
      adMetadata.put("campaign", "Sample ad campaign");
      ```

1. Roep `trackEvent()` met de `AdStart` gebeurtenis in de `MediaHeartbeat` instantie aan om het afspelen van de advertentie te volgen.

   Neem een verwijzing naar de aangepaste metagegevensvariabele (of een leeg object) op als de derde parameter in de gebeurtenisaanroep:

   ```java
   public void onAdStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdStart,  
                             adInfo,  
                             adMetadata); 
   }
   ```

1. Wanneer het afspelen van de advertentie het einde van de advertentie heeft bereikt, roept u `trackEvent()` de `AdComplete` gebeurtenis aan:

   ```java
   public void onAdComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdComplete, null, null); 
   }
   ```

1. Als het afspelen van de advertentie niet is voltooid omdat de gebruiker de advertentie heeft overgeslagen, houdt u de `AdSkip` gebeurtenis bij:

   ```java
   public void onAdSkip(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdSkip, null, null); 
   }
   ```

1. Herhaal stap 3 tot en met 7 opnieuw als er extra advertenties binnen dezelfde `AdBreak`advertentie zijn.
1. Wanneer het advertentieeinde is voltooid, gebruikt u de `AdBreakComplete` gebeurtenis om te volgen:

   ```java
   public void onAdBreakComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete, null, null); 
   }
   ```

Zie het volgende scenario [VOD playback met pre-rol advertenties](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md) voor meer informatie.
