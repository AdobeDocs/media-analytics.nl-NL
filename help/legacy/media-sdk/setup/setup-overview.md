---
title: Uitvoeren van Uitgevoerde Media SDKs
description: "Leer hoe u de SDK van Media instelt voor het bijhouden van media in uw mobiele, OTT- en browser-toepassingen."
uuid: 06fefedb-b0c8-4f7d-90c8-e374cdde1695
exl-id: a175332e-0bdc-44aa-82cb-b3f879e7abfc
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 2%

---

# Verouderd - Overzicht van de installatie van Media SDK {#setup-overview}

Nadat u de SDK van Media voor uw video-app of -speler hebt gedownload, volgt u de informatie in deze sectie om de SDK van Media in te stellen en te implementeren.


## Algemene uitvoeringsrichtsnoeren {#general-implementation-guidelines}

Er worden drie belangrijke SDK-componenten gebruikt voor het bijhouden van Adobe-streaming media:
* Configuratie van de mediaritmische hartslag: `MediaHeartbeatConfig` bevat de basisinstellingen voor rapportage.
* Media Heartbeat Delegate—De `MediaHeartbeatDelegate` Bepaalt de afspeeltijd en het object QoS.
* Media Heartbone—De `MediaHeartbeat` is de primaire bibliotheek met leden en methoden.

## De SDK voor streaming media implementeren

Voer de volgende implementatiestappen uit om de SDK voor Streaming Media in te stellen en te gebruiken:

1. Een `MediaHeartbeatConfig` instantie en stel de parameterwaarden voor de configuratie in.

   |  Naam variabele  | Beschrijving  | Vereist |  Standaardwaarde  |
   |---|---|:---:|---|
   | `trackingServer` | Volgserver voor mediaanalyses. Dit is anders dan de analysetrackserver. | Ja | Lege tekenreeks |
   | `channel` | Kanaalnaam | Nee | Lege tekenreeks |
   | `ovp` | Naam van het online-mediaplatform waarmee inhoud wordt gedistribueerd | Nee | Lege tekenreeks |
   | `appVersion` | Versie van de mediaspeler-app/SDK | Nee | Lege tekenreeks |
   | `playerName` | Naam van de mediaspeler in gebruik, d.w.z. &quot;AVPlayer&quot;, &quot;HTML5 Player&quot;, &quot;My Custom Player&quot; | Nee | Lege tekenreeks |
   | `ssl` | Geeft aan of aanroepen moeten worden uitgevoerd via HTTPS | Nee | false |
   | `debugLogging` | Geeft aan of foutopsporingslogbestand is ingeschakeld | Nee | false |

1. Implementeer de `MediaHeartbeatDelegate`.

   |  Naam van methode  |  Beschrijving  | Vereist |
   | --- | --- | :---: |
   | `getQoSObject()` | Hiermee wordt het `MediaObject` instantie die de huidige informatie QoS bevat. Deze methode wordt meerdere keren aangeroepen tijdens een afspeelsessie. De implementatie van de speler moet altijd de recentst beschikbare gegevens terugkeren QoS. | Ja |
   | `getCurrentPlaybackTime()` | Retourneert de huidige positie van de afspeelkop. <br /> Voor het bijhouden van VOD wordt de waarde opgegeven in seconden vanaf het begin van het media-item. <br /> Wanneer de speler voor live streaming geen informatie over de duur van de inhoud geeft, kan de waarde worden opgegeven als het aantal seconden dat is verstreken sinds middernacht UTC van die dag. <br /> Opmerking: Wanneer u voortgangsmarkeringen gebruikt, is de duur van de inhoud vereist en moet de afspeelkop worden bijgewerkt als het aantal seconden vanaf het begin van het media-item, te beginnen met 0. | Ja |

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

   Gebruik de `MediaHertbeatConfig` en `MediaHertbeatDelegate` om de `MediaHeartbeat` -instantie.

   >[!IMPORTANT]
   >
   >Zorg ervoor dat uw `MediaHeartbeat` -instantie is toegankelijk en wordt pas aan het einde van de sessie toegewezen. Deze instantie wordt gebruikt voor alle volgende gebeurtenissen voor het bijhouden van media.

   >[!TIP]
   >
   >`MediaHeartbeat` vereist een instantie van `AppMeasurement` om oproepen naar Adobe Analytics te verzenden.

1. Combineer alle stukken.

   De volgende voorbeeldcode gebruikt onze JavaScript 2.x SDK voor een HTML5 videospeler:

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

* **Adobe Analytics-server (AppMeasurement)**
Voor meer informatie over het volgen van serveropties, zie [De variabelen trackingServer en trackingServerSecure correct vullen.](https://helpx.adobe.com/analytics/kb/determining-data-center.html)

   >[!IMPORTANT]
   >
   >Voor de Experience Cloud Bezoeker-id-service is een RDC-trackingserver of CNAME vereist die een RDC-server oplost.

   De analysetrackingserver moet eindigen op &quot;`.sc.omtrdc.net`&quot; of een CNAME zijn.

* ** Media Analytics (Heartbeats) server** Dit heeft altijd de indeling &quot;`[your_namespace].hb.omtrdc.net`&quot;. De waarde van &quot;`[your_namespace]`&quot; geeft uw bedrijf aan en wordt opgegeven door Adobe.

Mediatracering werkt op alle platformen hetzelfde, zowel op het bureaublad als op mobiele apparaten. Audio bijhouden werkt momenteel op mobiele platforms. Voor alle volgende vraag zijn er een paar zeer belangrijke universele variabelen die moeten worden bevestigd:
