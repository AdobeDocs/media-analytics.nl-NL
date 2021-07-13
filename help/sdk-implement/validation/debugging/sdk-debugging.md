---
title: Foutopsporing in SDK
description: Leer over het volgen/registreren beschikbaar in de SDK van Media.
uuid: a5972d87-c593-4b4f-a56f-dca6e25268e1
exl-id: c2de6454-8538-4d07-a099-e278b153d894
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 1%

---

# Foutopsporing in SDK{#sdk-debugging}

U kunt logbestanden in- en uitschakelen. De Media SDK biedt een uitgebreid mechanisme voor overtrekken/registreren in de stapel voor het bijhouden van media. U kunt registreren toelaten of onbruikbaar maken door de `debugLogging` vlag op het voorwerp te plaatsen Config.

## Voorbeeldcode voor foutopsporingslogboekregistratie

### Android

```java
// Media Heartbeat initialization 
MediaHeartbeatConfig config = new MediaHeartbeatConfig(); 
config.debugLogging = true; 

// Use this space for setting other config values 
MediaHeartbeat _heartbeat = new MediaHeartbeat(this, config); 
```

### iOS

```
// Media Heartbeat Initialization 
ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init]; 
config.debugLogging = YES; 

// Use this space for setting other config values 
ADBMediaHeartbeat *_mediaHeartbeat =  
[[ADBMediaHeartbeat alloc] initWithDelegate:self config:config]; 
```

### JavaScript

```js
// Media Heartbeat initialization 
var mediaConfig = new MediaHeartbeatConfig(); 
mediaConfig.debugLogging = true; 
this._mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement); 
```

### OTT (Chromecast, Roku)

De bibliotheek ADBMobile verstrekt zuivert registreren door de `setDebugLogging` methode. Foutopsporingslogbestand moet worden ingesteld op `false` voor alle productie-apps.

#### Roku

```
ADBMobile().setDebugLogging(true)
```

#### Chromecast

```
ADBMobile.config.setDebugLogging(true)
```

## Het gebruiken van Adobe Bloodhound om Chromecast Toepassingen te testen

Tijdens toepassingsontwikkeling, staat Bloodhound u toe om servervraag plaatselijk te bekijken, en naar keuze door:sturen de gegevens aan de servers van de Adobe inzameling.

<!--
For more information about Bloodhound, see the following guides:

* [Bloodhound 3.x for Mac](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=2ahUKEwiimfSUypDpAhVZHzQIHS6WDQIQFjABegQIChAD&url=https%3A%2F%2Fmarketing.adobe.com%2Fresources%2Fhelp%2Fen_US%2Fmobile%2Fbloodhound%2F&usg=AOvVaw3t4s0gcvuWEpLIqBkhKdGH) 
* [Bloodhound 2.2 for Windows](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=3&cad=rja&uact=8&ved=0ahUKEwjil9aM87jRAhUExlQKHTYZCjoQFggoMAI&url=https%3A%2F%2Fmarketing.adobe.com%2Fresources%2Fhelp%2Fen_US%2Fmobile%2Fbloodhound_win_2x%2F&usg=AFQjCNEW-gZp1IdbifWFDgDNEaQcGlBobg&sig2=K0waTKxdMj_2kfNXdMI2yg)
-->

>[!IMPORTANT]
>
>Op 30 april 2017 is Adobe Bloodhound zonsondergang. Vanaf 1 mei 2017 worden er geen aanvullende verbeteringen aangebracht en wordt er geen extra ondersteuning voor Engineering of Adobe Expert Care geboden.

## Logberichten

Logberichten hebben deze indeling:

```js
Format: [<timestamp>] [<level>] [<tag>] [<message>] 
Example: [16:10:29 GMT­0700 (PDT).245] [DEBUG] [plugin::player] Resolving qos.startupTime: 0
```

* **timestamp:** This is the current CPU time (time-zone for GMT)
* **niveau:** Er zijn 4 berichtniveaus gedefinieerd:
   * INFO - Meestal worden de invoergegevens van de toepassing (naam van speler valideren, video-id enzovoort)
   * DEBUG - zuivert logboeken, die door de ontwikkelaars worden gebruikt om complexere kwesties te zuiveren
   * WAARSCHUWING - Geeft mogelijke integratie-/configuratiefouten of fouten in de SDK van Heartbeats aan
   * FOUT - Geeft belangrijke integratiefouten of fouten in de SDK van Heartbeats aan
* **tag:** De naam van de subcomponent die het logbericht heeft uitgegeven (gewoonlijk de klassenaam)
* **bericht:** het daadwerkelijke spoorbericht

U kunt de logboekoutput door de bibliotheek van SDK van Media gebruiken om de implementatie te verifiëren. Een goede strategie is door de logboeken voor het koord `#track` te zoeken. Dit zal alle `track*()` vraag benadrukken die door uw toepassing wordt gemaakt.

Dit is bijvoorbeeld wat de voor `#track` gefilterde logboeken eruit zouden kunnen zien:

```js
[16:10:29 GMT­0700 (PDT).222] [INFO] [plugin::player] #trackVideoLoad() 
[16:10:29 GMT­0700 (PDT).230] [INFO] [plugin::player] #trackSessionStart() 
[16:10:29 GMT­0700 (PDT).250] [INFO] [plugin::player] #trackPlay() 
[16:10:29 GMT­0700 (PDT).759] [INFO] [plugin::player] #trackChapterStart() 
[16:10:44 GMT­0700 (PDT).769] [INFO] [plugin::player] #trackAdStart() 
[16:10:59 GMT­0700 (PDT).752] [INFO] [plugin::player] #trackAdComplete() 
[16:10:59 GMT­0700 (PDT).770] [INFO] [plugin::player] #trackChapterStart() 
[16:11:29 GMT­0700 (PDT).734] [INFO] [plugin::player] #trackPause() 
[16:11:29 GMT­0700 (PDT).764] [INFO] [plugin::player] #trackComplete() 
[16:11:29 GMT­0700 (PDT).766] [INFO] [plugin::player] #trackVideoUnload()
```
