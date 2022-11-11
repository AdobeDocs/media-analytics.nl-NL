---
title: Leer de kwaliteit van de ervaring bij te houden met JavaScript 2.x
description: "Leer over het uitvoeren van kwaliteit van ervaring (QoE, QoS) het volgen gebruikend Media SDK in browser apps gebruikend JavaScript 2.x."
uuid: 3bc762a2-9706-4b62-aa91-747f461dd13d
exl-id: 5924eba4-15a9-405b-9a05-8a7308ddec47
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 2%

---

# Kwaliteit van ervaring bijhouden met JavaScript 2.x{#track-quality-of-experience-on-javascript}

De volgende instructies bieden richtlijnen voor implementatie voor alle 2.x SDK&#39;s.

>[!IMPORTANT]
>
>Als u een 1.x-versie van de SDK implementeert, kunt u de 1.x-handleidingen voor ontwikkelaars hier downloaden: [SDK&#39;s downloaden.](/help/getting-started/download-sdks.md)

## QOS implementeren

1. Bepaal wanneer de bitsnelheid verandert tijdens het afspelen van media en maak de opdracht `MediaObject` instantie die de informatie QoS gebruikt.

   QoSObject-variabelen:

   >[!TIP]
   >
   >Deze variabelen zijn slechts vereist als u van plan bent om QoS te volgen.

   | Variabele | Beschrijving | Vereist |
   | --- | --- | :---: |
   | `bitrate` | Huidige bitsnelheid | Ja |
   | `startupTime` | Opstarttijd | Ja |
   | `fps` | FPS-waarde | Ja |
   | `droppedFrames` | Aantal gedropte frames | Ja |

   Maken van QoS-objecten:

   ```js
   // Replace <bitrate>, <startuptime>, <fps> and  
   // <droppeFrames> with the current playback QoS values.  
   var qosObject = MediaHeartbeat.createQoSObject(<bitrate>,  
                                                  <startuptime>,  
                                                  <fps>,  
                                                  <droppedFrames>);
   ```

1. Als bij het afspelen wordt geschakeld naar een andere bitsnelheid, roept u de `BitrateChange` -gebeurtenis in de Media Heartbone-instantie:

   ```js
   _onBitrateChange = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, qosObject);
   };
   ```

   >[!IMPORTANT]
   >
   >Werk het object QoS bij en roep de gebeurtenis Bitrate change aan bij elke wijziging in de bitsnelheid. Dit verstrekt de nauwkeurigste gegevens QoS.

1. Controleer of `getQoSObject()` De methode keert de meest bijgewerkte informatie QoS terug.
1. Wanneer de mediaspeler een fout aantreft en de foutgebeurtenis beschikbaar is voor de speler-API, gebruikt u `trackError()` om de foutinformatie vast te leggen. (Zie [Overzicht](/help/use-cases/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Fouten bij het bijhouden van mediaspeler stoppen de mediatrackingsessie niet. Als de fout in de mediaspeler voorkomt dat het afspelen wordt voortgezet, controleert u of de mediatrackingsessie is gesloten door `trackSessionEnd()` na het aanroepen `trackError()`.
