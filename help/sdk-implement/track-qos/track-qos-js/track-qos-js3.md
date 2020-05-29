---
title: Kwaliteit van ervaring bijhouden met JavaScript 3.x
description: In dit onderwerp wordt beschreven hoe u het bijhouden van de kwaliteit van de ervaring (QoE, QoS) implementeert met de SDK van Media in browsertoepassingen met behulp van JavaScript 3x.
translation-type: tm+mt
source-git-commit: fa161e2d41629fdfe77100d87d6a44728e23d77f
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---


# Kwaliteit van ervaring bijhouden met JavaScript 3.x{#track-quality-of-experience-on-javascript}

>[!IMPORTANT]
>
>De volgende instructies bieden richtlijnen voor implementatie voor alle 3.x SDK&#39;s. Als u eerdere versies van de SDK implementeert, kunt u de ontwikkelaarsgidsen hier downloaden: [SDK&#39;s downloaden.](/help/sdk-implement/download-sdks.md)

## Implemement QOE

1. Identify when the bitrate changes during media playback and create the `qoeObject` instance using the QoE information.

   QoEObject variables:

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

1. Roep de `BitrateChange` gebeurtenis in de Media Heartmaatinstantie aan wanneer bij het afspelen wordt geschakeld naar een andere bitsnelheid:

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
   >Werk het object QoE bij en roep de gebeurtenis Bitrate change aan bij elke wijziging in de bitsnelheid. Dit verstrekt de nauwkeurigste gegevens QoE.

1. Zorg ervoor om methode te roepen `updateQoEObject()` om de meest bijgewerkte informatie QoE aan SDK te verstrekken.
1. Wanneer de mediaspeler een fout aantreft en de foutgebeurtenis beschikbaar is voor de speler-API, gebruikt u deze `trackError()` om de foutinformatie vast te leggen. (Zie [Overzicht](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Fouten bij het bijhouden van mediaspeler stoppen de mediatrackingsessie niet. Als de fout in de mediaspeler voorkomt dat het afspelen wordt voortgezet, controleert u of de sessie voor het bijhouden van media is gesloten door het aanroepen `trackSessionEnd()` na het aanroepen `trackError()`.
