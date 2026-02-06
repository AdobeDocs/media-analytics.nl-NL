---
title: Leer de kwaliteit van de ervaring bij te houden met JavaScript 3.x
description: Leer hoe u het bijhouden van de kwaliteit van de ervaring (QoE, QoS) implementeert met de Media SDK in browser-apps met JavaScript 3x.
exl-id: b5570e9c-8fb1-4458-bd1a-86ff6fce7813
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 1%

---

# Trackkwaliteit van ervaringen met JavaScript 3.x{#track-quality-of-experience-on-javascript}

De volgende instructies bieden richtlijnen voor implementatie voor alle 2.x SDK&#39;s.

>[!IMPORTANT]
>
>Als u om het even welke vorige versies van SDK uitvoert, kunt u de Gidsen van Ontwikkelaars hier downloaden: [ Download SDKs.](/help/getting-started/download-sdks.md)

## QOE implementeren

1. Bepaal wanneer de bitsnelheid verandert tijdens het afspelen van media en maak de `qoeObject` -instantie met behulp van de QoE-informatie.

   QoEObject-variabelen:

   >[!TIP]
   >
   >Deze variabelen zijn slechts vereist als u van plan bent om QoS te volgen.

   | Variabele | Type | Beschrijving |
   | --- | --- | --- |
   | `bitrate` | getal | Huidige bitsnelheid |
   | `startupTime` | getal | Opstarttijd |
   | `fps` | getal | FPS-waarde |
   | `droppedFrames` | getal | Aantal gedropte frames |

   Maken van QoE-object:

   ```js
   // Replace <bitrate>, <startuptime>, <fps> and
   // <droppeFrames> with the current playback QoE values.
   var qoeObject = ADB.Media.createQoEObject(<bitrate>,
                                                  <startuptime>,
                                                  <fps>,
                                                  <droppedFrames>);
   tracker.updateQoEObject(qoeObject);
   ```

1. Roep de gebeurtenis `BitrateChange` in de Media Heartbeat-instantie aan wanneer er wordt geschakeld naar een andere bitsnelheid:

   ```js
   _onBitrateChange = function() {
       // If the new bitrate value is available provide it to the tracker.
       var qoeObject = ADB.Media.createQoEObject(1000000, 2.4, 25, 10);
       tracker.updateQoEObject(qoeObject);
   
       tracker.trackEvent(ADB.Media.Event.BitrateChange);
   };
   ```

   >[!IMPORTANT]
   >
   >Werk het object QoE bij en roep de gebeurtenis bitsnelheidwijziging aan bij elke wijziging in de bitsnelheid. Dit verstrekt de nauwkeurigste gegevens QoE.

1. Roep de methode `updateQoEObject()` aan om de meest bijgewerkte QoE-gegevens aan de SDK te verstrekken.
1. Wanneer de mediaspeler een fout aantreft en de foutgebeurtenis beschikbaar is voor de speler-API, gebruikt u `trackError()` om de foutinformatie vast te leggen. (Zie [ Overzicht ](/help/use-cases/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Fouten bij het bijhouden van mediaspeler stoppen de mediatrackingsessie niet. Als de fout in de mediaspeler voorkomt dat het afspelen wordt voortgezet, controleert u of de mediatrackingsessie is gesloten door `trackSessionEnd()` aan te roepen na het aanroepen van `trackError()` .
