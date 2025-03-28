---
title: Leer hoe u de kwaliteit van ervaring kunt bijhouden op Chromecast
description: Leer over het uitvoeren van kwaliteit van ervaring (QoE, QoS) het volgen gebruikend Media SDK op Chromecast.
uuid: d0cdc8cd-4db0-45ef-9470-1cba3996305b
exl-id: 04b9b888-2727-4aa6-a934-94a02c85a490
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 2%

---

# Trackkwaliteit van ervaring op Chromecast{#track-quality-of-experience-on-chromecast}

De volgende instructies bieden richtlijnen voor implementatie voor alle 2.x SDK&#39;s.

>[!IMPORTANT]
>
>Als u een 1.x versie van SDK uitvoert, kunt u de 1.x Gidsen van Ontwikkelaars hier downloaden: [ Download SDKs.](/help/getting-started/download-sdks.md)

## Overzicht {#overview}

De kwaliteit van ervaring het volgen omvat kwaliteit van de dienst (QoS) en fout het volgen, allebei zijn facultatieve elementen en **niet** vereist voor kernmedia het volgen implementaties. U kunt de mediaspeler-API gebruiken om de variabelen met betrekking tot QoS en foutcontrole te identificeren.

## Gebeurtenissen van Player {#player-events}

### Bij alle gebeurtenissen die betrekking hebben op bitsnelheden

* De instantie van het object QoS maken/bijwerken voor het afspelen, `qosObject`
* Roep `trackEvent(Media.Heartbeat.Event.BitrateChange, qosObject);`

### Bij spelerfouten

Roep `trackError("media error id");`

## Implementeren {#implement}

1. Bepaal wanneer de bitsnelheid verandert tijdens het afspelen van media en maak de `MediaObject` -instantie met behulp van de QoS-informatie.

   **variabelen QoSObject:**

   >[!TIP]
   >
   >Deze variabelen zijn slechts vereist als u van plan bent om QoS te volgen.

   | Variabele | Beschrijving | Vereist |
   | --- | --- | :---: |
   | `bitrate` | Huidige bitsnelheid | Ja |
   | `startupTime` | Opstarttijd | Ja |
   | `fps` | FPS-waarde | Ja |
   | `droppedFrames` | Aantal gedropte frames | Ja |

   **QoS objecten verwezenlijking:** [ createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createQoSObject)

   ```
   qosInfo = ADBMobile.media.createQoSObject(50000, 0, 24, 10);
   ```

1. Wanneer de playbackschakelaars bitrates, vraag de `BitrateChange` gebeurtenis in de instantie van het Geheartmaatschap van Media: [ trackEvent ](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BitrateChange);
   ```

   >[!IMPORTANT]
   >
   >Werk het object QoS bij en roep de gebeurtenis Bitrate change aan bij elke wijziging in de bitsnelheid. Dit verstrekt de nauwkeurigste gegevens QoS.

1. Zorg ervoor dat de `getQoSObject()` methode de meest bijgewerkte informatie QoS terugkeert.
1. Wanneer de mediaspeler een fout aantreft en de foutgebeurtenis beschikbaar is voor de speler-API, gebruikt u `trackError()` om de foutinformatie vast te leggen. (Zie [ Overzicht ](/help/use-cases/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Fouten bij het bijhouden van mediaspeler stoppen de mediatrackingsessie niet. Als de fout in de mediaspeler voorkomt dat het afspelen wordt voortgezet, controleert u of de mediatrackingsessie is gesloten door `trackSessionEnd()` aan te roepen na het aanroepen van `trackError()` .
