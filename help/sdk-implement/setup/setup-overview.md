---
title: Uitvoeren van Uitgevoerde Media SDKs
description: '"Leer hoe u de SDK van Media instelt voor het bijhouden van media in uw mobiele, OTT- en browser-toepassingen."'
uuid: 06fefedb-b0c8-4f7d-90c8-e374cdde1695
exl-id: a175332e-0bdc-44aa-82cb-b3f879e7abfc
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 3%

---

# Overzicht van setup{#setup-overview}

De volgende instructies zijn van toepassing op 2.x Media SDKs. Als u een 1.x versie van Media SDK uitvoert, zie [1.x de Documentatie van SDK van Media.](/help/sdk-implement/download-sdks.md) Voor Primetime-integrators, zie de  _documentatie_ bij Primetime Media SDK hieronder.

>[!IMPORTANT]
>
>Aan het einde van de ondersteuning voor versie 4 Mobile SDK&#39;s op 31 augustus 2021 beëindigt Adobe ook de ondersteuning voor de Media Analytics SDK&#39;s voor iOS en Android.  Voor extra informatie, zie [Van begin tot eind - van - de Veelgestelde vragen van de Analyse van Media SDK](/help/sdk-implement/end-of-support-faqs.md).


## Ondersteuning voor minimale versie van Platform {#minimum-platform-version}

In de volgende tabel worden de minimale platformversies beschreven die worden ondersteund voor elke SDK, vanaf 19 februari 2019.

| OS/Browser | Minimumversie vereist |
| --- | --- |
| iOS | iOS 6+ |
| Android | Android 5.0+ - Lollipop |
| Chroom | v22+ |
| Mozilla | v27+ |
| Safari | v7+ |
| IE | v11+ |

## Algemene uitvoeringsrichtsnoeren {#general-implementation-guidelines}

Er zijn drie belangrijke componenten van SDK betrokken bij media het volgen:
* Configuratie van de Hartslag van media - config bevat de basismontages voor het melden.
* De Afgevaardigde van het Hoogtepunt van media - de afgevaardigde controleert playbacktijd en het voorwerp QoS.
* Mediahartslag - De primaire bibliotheek met leden en methoden.

Voer de volgende stappen uit voor de implementatie:

1. Creeer een `MediaHeartbeatConfig` instantie en plaats uw configuratieparameterwaarden.

   |  Naam variabele  | Beschrijving  | Vereist |  Standaardwaarde  |
   |---|---|:---:|---|
   | `trackingServer` | Volgserver voor mediaanalyses. Dit is anders dan de analysetrackserver. | Ja | Lege tekenreeks |
   | `channel` | Kanaalnaam | Nee | Lege tekenreeks |
   | `ovp` | Naam van het online-mediaplatform waarmee inhoud wordt gedistribueerd | Nee | Lege tekenreeks |
   | `appVersion` | Versie van de mediaspeler-app/SDK | Nee | Lege tekenreeks |
   | `playerName` | Naam van de mediaspeler in gebruik, d.w.z. &quot;AVPlayer&quot;, &quot;HTML5 Player&quot;, &quot;My Custom Player&quot; | Nee | Lege tekenreeks |
   | `ssl` | Geeft aan of aanroepen moeten worden uitgevoerd via HTTPS | Nee | false |
   | `debugLogging` | Geeft aan of foutopsporingslogbestand is ingeschakeld | Nee | false |

1. Implementeer `MediaHeartbeatDelegate`.

   |  Naam van methode  |  Beschrijving  | Vereist |
   | --- | --- | :---: |
   | `getQoSObject()` | Retourneert de instantie `MediaObject` die de huidige QoS-informatie bevat. Deze methode wordt meerdere keren aangeroepen tijdens een afspeelsessie. De implementatie van de speler moet altijd de recentst beschikbare gegevens terugkeren QoS. | Ja |
   | `getCurrentPlaybackTime()` | Retourneert de huidige positie van de afspeelkop. Voor het bijhouden van VOD wordt de waarde opgegeven in seconden vanaf het begin van het media-item. Voor LINEAR/LIVE tracking wordt de waarde opgegeven als het aantal seconden sinds middernacht UTC op die dag. | Ja |

   >[!TIP]
   >
   >Het object Quality of Service (QoS) is optioneel. Als QoS-gegevens beschikbaar zijn voor uw speler en u wilt die gegevens bijhouden, zijn de volgende variabelen vereist:

   | Naam variabele | Beschrijving   | Vereist |
   | --- | --- | :---: |
   | `bitrate` | De bitsnelheid van media in bits per seconde. | Ja |
   | `startupTime` | De opstarttijd van media in milliseconden. | Ja |
   | `fps` | De frames die per seconde worden weergegeven. | Ja |
   | `droppedFrames` | Het aantal gedropte frames tot nu toe. | Ja |

1. Maak de instantie `MediaHeartbeat`.

   Gebruik `MediaHertbeatConfig` en `MediaHertbeatDelegate` om de `MediaHeartbeat` instantie tot stand te brengen.

   >[!IMPORTANT]
   >
   >Zorg ervoor dat uw `MediaHeartbeat` instantie toegankelijk is en niet tot het eind van de zitting wordt gedealloceerd. Deze instantie wordt gebruikt voor alle volgende gebeurtenissen voor het bijhouden van media.

   >[!TIP]
   >
   >`MediaHeartbeat` vereist een geval van  `AppMeasurement` om vraag naar Adobe Analytics te verzenden.

1. Combineer alle stukken.

   In de volgende voorbeeldcode wordt onze JavaScript 2.x SDK gebruikt voor een HTML5-videospeler:

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

* Aanroepen voor media en advertenties worden rechtstreeks naar de Adobe Analytics-server (AppMeasurement) verzonden.
* De vraag van de hartslag wordt verzonden naar de Media Analytics (hartslagen) volgende server, daar verwerkt, en tot de server van Adobe Analytics overgegaan.

* **Adobe Analytics-**
server (AppMeasurement). Zie De variabelen trackingServer en trackingServerSecure  [correct vullen voor meer informatie over opties voor het bijhouden van de server.](https://helpx.adobe.com/analytics/kb/determining-data-center.html)

   >[!IMPORTANT]
   >
   >Voor de Experience Cloud Bezoeker-id-service is een RDC-trackingserver of CNAME vereist die een RDC-server oplost.

   De analysetrackingserver moet eindigen in &quot;`.sc.omtrdc.net`&quot; of een CNAME zijn.

* ** Media Analytics (Heartbeats)-server**
Dit heeft altijd het formaat &quot;`[your_namespace].hb.omtrdc.net`&quot;. De waarde van &quot;`[your_namespace]`&quot;specificeert uw bedrijf, en door Adobe verstrekt.

Mediatracering werkt op alle platformen hetzelfde, zowel op het bureaublad als op mobiele apparaten. Audio bijhouden werkt momenteel op mobiele platforms. Voor alle volgende vraag zijn er een paar zeer belangrijke universele variabelen die moeten worden bevestigd:

## SDK 1.x-documentatie {#sdk-1x-documentation}

| Video Analytics 1.x SDKs  |  Ontwikkelaarshulplijnen (alleen PDF&#39;s) |
| --- | --- |
| Android | [Configureren voor Android  ](vhl-dev-guide-v15_android.pdf) |
| AppleTV | [Configureren voor AppleTV  ](vhl-dev-guide-v1x_appletv.pdf) |
| Chromecast | [Configureren voor Chromecast  ](chromecast_1.x_sdk.pdf) |
| iOS | [Configureren voor iOS  ](vhl-dev-guide-v15_ios.pdf) |
| JavaScript | [Configureren voor JavaScript  ](vhl-dev-guide-v15_js.pdf) |
| Primetime | <ul> <li> Android:   [Mediaanalyse configureren](https://help.adobe.com/en_US/primetime/psdk/android/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> DHLS:   [Mediaanalyse configureren](https://help.adobe.com/en_US/primetime/psdk/dhls/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> iOS:   [Mediaanalyse configureren](https://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> </ul> |
| TVML | [Configureren voor TVML  ](vhl_tvml.pdf) |

## Documentatie bij primaire media-SDK {#primetime-docs}

* [Primetime-gebruikershandleidingen](https://helpx.adobe.com/nl/primetime/user-guide.html)
