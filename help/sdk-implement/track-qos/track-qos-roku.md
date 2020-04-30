---
title: Traceerkwaliteit van ervaring op Roku
description: Dit onderwerp beschrijft het uitvoeren van kwaliteit van ervaring (QoE, QoS) het volgen gebruikend Media SDK op Roku.
uuid: a8b242ab-da3c-4297-9eef-f0b9684ef56a
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Traceerkwaliteit van ervaring op Roku{#track-quality-of-experience-on-roku}

>[!IMPORTANT]
>
>De volgende instructies bieden richtlijnen voor implementatie voor alle 2.x SDK&#39;s. Als u een 1.x-versie van de SDK implementeert, kunt u de 1.x-handleidingen voor ontwikkelaars hier downloaden: SDK&#39;s [downloaden.](/help/sdk-implement/download-sdks.md)

## QOS implementeren

1. Bepaal wanneer de bitsnelheid verandert tijdens het afspelen van media en gebruik de `mediaUpdateQoS` API om de QoS-informatie bij te werken op de Media SDK.

   QoSObject-variabelen:

   >[!TIP]
   >
   >Deze variabelen zijn alleen vereist als u QoS bijhoudt.

   | Variabele | Beschrijving | Vereist |
   | --- | --- | :---: |
   | `bitrate` | Huidige bitsnelheid | Ja |
   | `startupTime` | Opstarttijd | Ja |
   | `fps` | FPS-waarde | Ja |
   | `droppedFrames` | Aantal gedropte frames | Ja |

   Bijvoorbeeld:

   ```
   bitrate = 200000
   fps = 0
   droppedFrames = 1
   startupTime = 2
   qosinfo = adb_media_init_qosinfo(bitrate, startupTime, fps, droppedFrames)
   
   ADBMobile().mediaUpdateQoS(qosinfo)
   ```

   <!--
    QoS object creation:
 
    ```
    qosInfo=adb_media_init_qosinfo()
    qosInfo.bitrate = 200000
    qosInfo.fps = 0
    qosInfo.droppedFrames = 1
    qosInfo.startupTime = 2
    ```
    -->

1. Wanneer bij het afspelen van bitsnelheden wordt gewisseld, roept u `trackEvent(BitrateChange)` de Media SDK op de hoogte te stellen van het feit dat de bitsnelheid is gewijzigd.

   ```
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_BITRATE_CHANGE)
   ```

   >[!NOTE]
   >
   >U moet bellen `updateQoSObject` met de bijgewerkte bitsnelheidwaarde.

   <!--
    ```
    qosContextData = {}
    ADBMobile().mediaTrackEvent(MEDIA_BITRATE_CHANGE, qosInfo, qosContextData)
    ```
 
    >[!IMPORTANT]
    >
    >Update the QoS object and call the bitrate change event on every bitrate change. This provides the most accurate QoS data.
    -->

1. Wanneer de mediaspeler een fout aantreft en de foutgebeurtenis beschikbaar is voor de speler-API, gebruikt u deze `trackError()` om de foutinformatie vast te leggen. (Zie [Overzicht](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Fouten bij het bijhouden van mediaspeler stoppen de mediatrackingsessie niet. Als de fout in de mediaspeler voorkomt dat het afspelen wordt voortgezet, controleert u of de sessie voor het bijhouden van media is gesloten door het aanroepen `trackSessionEnd()` na het aanroepen `trackError()`.
