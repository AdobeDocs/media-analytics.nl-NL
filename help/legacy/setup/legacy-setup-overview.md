---
title: Legacy Media SDK's implementeren
description: Leer hoe u de **legacy** 2.x Media SDK instelt voor het bijhouden van media in uw mobiele, OTT- en browsertoepassingen (JS).
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: d94ede3e-95f8-4591-9833-ef39aff12ba9
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 1%

---

# Legacy 2.x Streaming Media SDK Setup - Overzicht{#setup-overview}

De instructies in deze sectie zijn op **erfenis** 2.x Media SDKs van toepassing.

* Voor informatie over het uitvoeren van een versie 1.x van Media SDK, zie de [ 1.x Documentatie van Media SDK.](/help/getting-started/download-sdks.md)

* Voor integrators Primetime, zie de _Documentatie van SDK van Media Primetime_.

>[!IMPORTANT]
>
>Met het einde van de ondersteuning voor versie 4 Mobile SDK&#39;s op 31 augustus 2021 beëindigt Adobe ook de ondersteuning voor de Media Analytics SDK&#39;s voor iOS en Android.  Voor extra informatie, zie [ Analytics SDK End-of-Support FAQs ](/help/additional-resources/end-of-support-faqs.md).


## Ondersteuning voor minimale platformversie {#minimum-platform-version}

In de volgende tabel worden de minimale platformversies beschreven die worden ondersteund voor elke SDK, vanaf 19 februari 2019.

| OS/Browser | Minimumversie vereist |
| --- | --- |
| iOS | iOS 6+ |
| Android | Android 5.0+ - Lollipop |
| Chrome | v22+ |
| Mozilla | v27+ |
| Safari | v7+ |
| IE | v11+ |

## Algemene uitvoeringsrichtsnoeren {#general-implementation-guidelines}

Er zijn drie belangrijke SDK-componenten die betrokken zijn bij mediatracering:
* Configuratie van de Hartslag van media - config bevat de basismontages voor het melden.
* De Afgevaardigde van het Hoogtepunt van media - de afgevaardigde controleert playbacktijd en het voorwerp QoS.
* Mediahartslag - De primaire bibliotheek met leden en methoden.

Voer de volgende stappen uit voor de implementatie:

1. Maak een `MediaHeartbeatConfig` -instantie en stel de configuratieparameterwaarden in.

   |  Naam variabele  | Beschrijving  | Vereist |  Standaardwaarde  |
   |---|---|:---:|---|
   | `trackingServer` | Volgserver voor mediaanalyses. Dit is anders dan de analysetrackserver. | Ja | Lege tekenreeks |
   | `channel` | Kanaalnaam | Nee | Lege tekenreeks |
   | `ovp` | Naam van het online-mediaplatform waarmee inhoud wordt gedistribueerd | Nee | Lege tekenreeks |
   | `appVersion` | Versie van de mediaspeler-app/SDK | Nee | Lege tekenreeks |
   | `playerName` | Naam van de mediaspeler in gebruik, dus &quot;AVPlayer&quot;, &quot;HTML5 Player&quot;, &quot;My Custom Player&quot; | Nee | Lege tekenreeks |
   | `ssl` | Geeft aan of aanroepen moeten worden uitgevoerd via HTTPS | Nee | false |
   | `debugLogging` | Geeft aan of foutopsporingslogbestand is ingeschakeld | Nee | false |

1. Voer `MediaHeartbeatDelegate` uit.

   |  Naam van methode  |  Beschrijving  | Vereist |
   | --- | --- | :---: |
   | `getQoSObject()` | Retourneert de `MediaObject` -instantie die de huidige QoS-informatie bevat. Deze methode wordt meerdere keren aangeroepen tijdens een afspeelsessie. De implementatie van de speler moet altijd de recentst beschikbare gegevens terugkeren QoS. | Ja |
   | `getCurrentPlaybackTime()` | Retourneert de huidige positie van de afspeelkop. <br /> Voor het bijhouden van VOD wordt de waarde opgegeven in seconden vanaf het begin van het media-item. <br /> Als de speler voor live streaming geen informatie geeft over de duur van de inhoud, kan de waarde worden opgegeven als het aantal seconden sinds middernacht UTC van die dag. <br /> Opmerking: wanneer u voortgangsmarkeringen gebruikt, is de duur van de inhoud vereist en moet de afspeelkop worden bijgewerkt tot het aantal seconden vanaf het begin van het media-item, te beginnen met 0. | Ja |

   >[!TIP]
   >
   >Het object Quality of Service (QoS) is optioneel. Als QoS-gegevens beschikbaar zijn voor uw speler en u wilt die gegevens bijhouden, zijn de volgende variabelen vereist:

   | Naam variabele | Beschrijving   | Vereist |
   | --- | --- | :---: |
   | `bitrate` | De bitsnelheid van media in bits per seconde. | Ja |
   | `startupTime` | De opstarttijd van media in milliseconden. | Ja |
   | `fps` | De frames die per seconde worden weergegeven. | Ja |
   | `droppedFrames` | Het aantal gedropte frames tot nu toe. | Ja |

1. Maak de `MediaHeartbeat` -instantie.

   Gebruik `MediaHertbeatConfig` en `MediaHertbeatDelegate` om de instantie `MediaHeartbeat` te maken.

   >[!IMPORTANT]
   >
   >Zorg ervoor dat uw `MediaHeartbeat` -instantie toegankelijk is en pas aan het einde van de sessie wordt gedealiteerd. Deze instantie wordt gebruikt voor alle volgende gebeurtenissen voor het bijhouden van media.

   >[!TIP]
   >
   >`MediaHeartbeat` vereist een instantie van `AppMeasurement` om aanroepen naar Adobe Analytics te verzenden.

1. Combineer alle stukken.

   De volgende voorbeeldcode gebruikt onze JavaScript 2.x SDK voor een HTML5-videospeler:

   ```javascript
   // Create local references to the heartbeat classes
   var MediaHeartbeat = ADB.va.MediaHeartbeat;
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig;
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate;
   
   //Media Heartbeat Config
   var mediaConfig = new MediaHeartbeatConfig();
   mediaConfig.trackingServer = "[your_namespace].hb.omtrdc.net";
   mediaConfig.playerName = "HTML5 Basic";
   mediaConfig.channel = "Video Channel";
   mediaConfig.debugLogging = true;
   mediaConfig.appVersion = "2.0";
   mediaConfig.ssl = false;
   mediaConfig.ovp = "";
   
   // Media Heartbeat Delegate
   var mediaDelegate = new MediaHeartbeatDelegate();
   
   // Set mediaDelegate CurrentPlaybackTime
   mediaDelegate.getCurrentPlaybackTime = function() {
       return video.currentTime;
   };
   
   // Set mediaDelegate QoSObject - OPTIONAL
   mediaDelegate.getQoSObject = function() {
       return MediaHeartbeat.createQoSObject(video.bitrate,  
                                             video.startuptime,  
                                             video.fps,  
                                             video.droppedframes);
   }
   // Create mediaHeartbeat instance      
   this.mediaHeartbeat =  
     new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurementInstance);  
   ```

## Valideren {#validate}

De volgende implementaties van de Analytics van media produceren twee soorten het volgen vraag:

* De vraag van het media en van het Begin van de advertentie wordt verzonden rechtstreeks naar de server van Adobe Analytics (AppMeasurement).
* De vraag van de hartslag wordt verzonden naar de Media Analytics (hartslagen) volgende server, daar verwerkt, en tot de server van Adobe Analytics overgegaan.

* **Adobe Analytics (AppMeasurement) server**
Voor meer informatie over het volgen van serveropties, zie [ correct de variabelen trackingServer en trackingServerSecure bevolken.](https://helpx.adobe.com/nl/analytics/kb/determining-data-center.html)

  >[!IMPORTANT]
  >
  >Voor de Experience Cloud Visitor ID-service is een RDC-trackingserver of CNAME vereist die een RDC-server oplost.

  De analytics tracking-server moet eindigen in &quot;`.sc.omtrdc.net`&quot; of een CNAME zijn.

* **&#x200B; Media Analytics (Heartbeats)-server**
Dit heeft altijd het formaat &quot;`[your_namespace].hb.omtrdc.net`&quot;. De waarde van &quot;`[your_namespace]`&quot;specificeert uw bedrijf, en door Adobe verstrekt.

Mediatracering werkt op alle platformen hetzelfde, zowel op het bureaublad als op mobiele apparaten. Audio bijhouden werkt momenteel op mobiele platforms. Voor alle volgende vraag zijn er een paar zeer belangrijke universele variabelen die moeten worden bevestigd:

## SDK 1.x-documentatie {#sdk-1x-documentation}

| Video Analytics 1.x SDKs  |  Ontwikkelaarshulplijnen (alleen PDF&#39;s) |
| --- | --- |
| Android | [ vormen voor Android ](vhl-dev-guide-v15_android.pdf) |
| APPLE TV | [ vormen voor Apple TV ](vhl-dev-guide-v1x_appletv.pdf) |
| Chromecast | [ vormt voor Chromecast ](chromecast_1.x_sdk.pdf) |
| iOS | [ vormen voor iOS ](vhl-dev-guide-v15_ios.pdf) |
| JavaScript | [ vormen voor JavaScript ](vhl-dev-guide-v15_js.pdf) |
| Primetime | <ul> <li> Android:   [ vorm Analytics van Media ](https://help.adobe.com/en_US/primetime/psdk/android/1.4/index.html) </li> <li> DHLS:   [ vorm Analytics van Media ](https://help.adobe.com/en_US/primetime/psdk/dhls/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> iOS:   [ vorm Analytics van Media ](https://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> </ul> |
| TVML | [ vormt voor TVML ](vhl_tvml.pdf) |

## SDK-documentatie voor primetime media {#primetime-docs}

* [ Gidsen van de Gebruiker Primetime ](https://helpx.adobe.com/nl/primetime/user-guide.html)
