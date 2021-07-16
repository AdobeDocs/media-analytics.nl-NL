---
title: Leer de kwaliteit van de ervaring bij te houden met JavaScript 3.x
description: '"Leer hoe u het bijhouden van de kwaliteit van de ervaring (QoE, QoS) implementeert met de SDK van Media in browsertoepassingen met behulp van JavaScript 3x."'
exl-id: b5570e9c-8fb1-4458-bd1a-86ff6fce7813
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 1%

---

# Kwaliteit van ervaring bijhouden met JavaScript 3.x{#track-quality-of-experience-on-javascript}

De volgende instructies bieden richtlijnen voor implementatie voor alle 2.x SDK&#39;s.

>[!IMPORTANT]
>
>Als u eerdere versies van de SDK implementeert, kunt u de ontwikkelaarsgidsen hier downloaden: [SDK&#39;s downloaden.](/help/sdk-implement/download-sdks.md)

## QOE voor implementatie

1. Bepaal wanneer de bitsnelheid verandert tijdens het afspelen van media en maak de `qoeObject`-instantie met behulp van de QoE-informatie.

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

1. Roep de gebeurtenis `BitrateChange` in de Media Heartmaatinstantie aan wanneer er wordt geschakeld naar een andere bitsnelheid:

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

1. Zorg ervoor om `updateQoEObject()` methode te roepen om de meest bijgewerkte informatie QoE aan SDK te verstrekken.
1. Wanneer de mediaspeler een fout aantreft en de foutgebeurtenis beschikbaar is voor de speler-API, gebruikt u `trackError()` om de foutinformatie vast te leggen. (Zie [Overzicht](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Fouten bij het bijhouden van mediaspeler stoppen de mediatrackingsessie niet. Als de fout in de mediaspeler voorkomt dat het afspelen wordt voortgezet, controleert u of de sessie voor het bijhouden van media is gesloten door `trackSessionEnd()` aan te roepen nadat `trackError()` is aangeroepen.
