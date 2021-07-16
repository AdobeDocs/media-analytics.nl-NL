---
title: Leer hoe u advertenties kunt bijhouden op iOS
description: Implementeer en tracking in iOS-toepassingen met de SDK van Media.
uuid: e979e679-cde5-4c30-8f34-867feceac13a
exl-id: a352bca9-bcfc-4418-b2a2-c9b1ad226359
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 4%

---

# Advertenties bijhouden op iOS{#track-ads-on-ios}

De volgende instructies bieden richtlijnen voor implementatie met behulp van de 2.x SDK&#39;s.

>[!IMPORTANT]
>
>Als u een 1.x-versie van de SDK implementeert, kunt u hier de 1.x-handleidingen voor ontwikkelaars downloaden: [SDK&#39;s downloaden.](/help/sdk-implement/download-sdks.md)

## Constanten voor bijhouden van advertenties

| Naam van constante | Beschrijving   |
|---|---|
| `ADBMediaHeartbeatEventAdBreakStart` | Constante voor het bijhouden van de gebeurtenis AdBreak Start |
| `ADBMediaHeartbeatEventAdBreakComplete` | Constante voor het bijhouden van de gebeurtenis AdBreak Complete |
| `ADBMediaHeartbeatEventAdStart` | Constante voor het bijhouden van de gebeurtenis Ad Start |
| `ADBMediaHeartbeatEventAdComplete` | Constante voor het bijhouden van de gebeurtenis Advertentie voltooid |
| `ADBMediaHeartbeatEventAdSkip` | Constante voor het bijhouden van de gebeurtenis Advertentie overslaan |

## Uitvoeringsstappen

1. Bepaal wanneer de grens van de advertentierak begint, met inbegrip van pre-rol, en creeer `AdBreakObject` door de informatie van de advertentierak te gebruiken.

   `AdBreakObject` referentie:

   | Naam variabele | Beschrijving | Vereist |
   | --- | --- | :---: |
   | `name` | De naam van het invoegpunt, zoals pre-roll, mid-roll en post-roll. | Ja |
   | `position` | De getalpositie van het advertentierak binnen de inhoud, beginnend met 1. | Ja |
   | `startTime` | Waarde van afspeelkop aan het begin van het advertentieeinde. | Ja |

   Object maken van einde toevoegen:

   ```
   id adBreakObject = [ADBMediaHeartbeat createAdBreakObjectWithName:[ADBREAK_NAME]
                               position:[POSITION]  
                               startTime:[START_TIME]];
   ```

1. Roep `trackEvent()` met `AdBreakStart` in de `MediaHeartbeat` instantie aan om het advertentiesonderbreking te volgen:

   ```
   - (void)onAdBreakStart:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakStart  
                        mediaObject:adBreakObject  
                        data:nil];
   }
   ```

1. Identificeer wanneer de advertentie begint en creeer een `AdObject` instantie gebruikend de advertentieinformatie.

   `AdObject` referentie:

   | Naam variabele | Beschrijving | Vereist |
   | --- | --- | :---: |
   | `name` | Vriendelijke naam van de advertentie. | Ja |
   | `adId` | De unieke id voor de advertentie. | Ja |
   | `position` | De numerieke positie van de advertentie binnen het advertentiespoor, beginnend met 1. | Ja |
   | `length` | Ad-lengte | Ja |

   Object maken toevoegen:

   ```
   id adObject = [ADBMediaHeartbeat createAdObjectWithName:[AD_NAME]
                                    adId:[AD_ID]
                                    position:[POSITION]
                                    length:[LENGTH]];
   ```

1. Voeg desgewenst standaard- en/of advertentiemetagegevens toe aan de mediatraceringssessie via de variabelen van de contextgegevens.

   * [Standaardmetadata voor advertenties implementeren in iOS](/help/sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
   * **Aangepast en metagegevens -** Voor aangepaste metagegevens maakt u een variabelenobject voor de aangepaste gegevensvariabelen en vult u de gegevens voor de huidige advertentie in:

      ```
      NSMutableDictionary *adDictionary = [[NSMutableDictionary alloc] init];
      [adDictionary setObject:@"Sample affiliate" forKey:@"affiliate"];
      [adDictionary setObject:@"Sample campaign" forKey:@"campaign"];
      [adDictionary setObject:@"Sample creative" forKey:@"creative"];
      ```

1. Roep `trackEvent()` met de gebeurtenis `AdStart` in de instantie `MediaHeartbeat` aan om het afspelen van de advertentie te volgen.

   Neem een verwijzing naar de aangepaste metagegevensvariabele (of een leeg object) op als de derde parameter in de gebeurtenisaanroep:

   ```
   - (void)onAdStart:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdStart  
                        mediaObject:adObject  
                        data:adDictionary];
   }
   ```

1. Wanneer het afspelen van de advertentie het einde van de advertentie bereikt, roept u `trackEvent()` aan met de gebeurtenis `AdComplete`.

   ```
   - (void)onAdComplete:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdComplete  
                        mediaObject:nil  
                        data:nil];
   }
   ```

1. Als het afspelen van de advertentie niet is voltooid omdat de gebruiker de advertentie heeft overgeslagen, houdt u de gebeurtenis `AdSkip` bij.

   ```
   - (void)onAdSkip:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdSkip  
                        mediaObject:nil  
                        data:nil];
   }
   ```

1. Herhaal stap 3 tot en met 7 als er extra advertenties binnen dezelfde `AdBreak` zijn.
1. Wanneer het ad-einde is voltooid, gebruikt u de gebeurtenis `AdBreakComplete` om te volgen:

   ```
   - (void)onAdBreakComplete:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakComplete  
                        mediaObject:nil  
                        data:nil];
   }
   ```

Zie het volgende scenario [VOD playback met pre-rol advertenties](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md) voor meer informatie.
