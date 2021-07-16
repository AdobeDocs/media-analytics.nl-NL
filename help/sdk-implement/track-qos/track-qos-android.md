---
title: Leer hoe u de kwaliteit van ervaring kunt bijhouden op Android
description: '"Leer over het uitvoeren van kwaliteit van ervaring (QoE, QoS) het volgen gebruikend Media SDK op Android."'
uuid: 81ff3939-48a6-45c1-8837-ddfa33490559
exl-id: cee8b119-bca2-4a5c-8111-2b49f7eede66
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 3%

---

# Traceerkwaliteit van ervaringen op Android{#track-quality-of-experience-on-android}

De volgende instructies bieden richtlijnen voor implementatie voor alle 2.x SDK&#39;s.

>[!IMPORTANT]
>
>Als u een 1.x-versie van de SDK implementeert, kunt u de 1.x-handleidingen voor ontwikkelaars hier downloaden: [SDK&#39;s downloaden.](/help/sdk-implement/download-sdks.md)

## QoS implementeren

1. Bepaal wanneer de bitsnelheid verandert tijdens het afspelen van media en maak de `MediaObject`-instantie met behulp van de QoS-informatie.

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

   ```java
   MediaObject qosObject =  
     MediaHeartbeat.createQoSObject(<BITRATE>,  
                                    <STARTUP_TIME>,  
                                    <FPS>,  
                                    <DROPPED_FRAMES>);
   ```

1. Zorg ervoor dat `getQoSObject()` de methode de meest bijgewerkte informatie QoS terugkeert.
1. Roep de gebeurtenis `BitrateChange` in de Media Heartmaatinstantie aan wanneer er wordt geschakeld naar een andere bitsnelheid:

   ```java
   public void onBitrateChange(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, null, null);
   }
   ```

   >[!IMPORTANT]
   >
   >Werk het object QoS bij en roep de gebeurtenis Bitrate change aan bij elke wijziging in de bitsnelheid. Dit verstrekt de nauwkeurigste gegevens QoS.
