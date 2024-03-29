---
title: Foutopsporing in SDK
description: Leer over het volgen/registreren beschikbaar in de SDK van Media.
uuid: a5972d87-c593-4b4f-a56f-dca6e25268e1
exl-id: c2de6454-8538-4d07-a099-e278b153d894
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 2%

---

# Foutopsporing in SDK{#sdk-debugging}

U kunt logbestanden in- en uitschakelen. De Media SDK biedt een uitgebreid mechanisme voor overtrekken/registreren in de stapel voor het bijhouden van media. U kunt registreren toelaten of onbruikbaar maken door te plaatsen `debugLogging` markering op het Config-object.

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

De ADBMobile-bibliotheek biedt foutopsporingslogboekregistratie via de `setDebugLogging` methode. Foutopsporingslogbestand moet worden ingesteld op `false` voor alle productie-apps.

#### Roku

```
ADBMobile().setDebugLogging(true)
```

#### Chromecast

```
ADBMobile.config.setDebugLogging(true)
```

## Logberichten

Logberichten hebben deze indeling:

```js
Format: [<timestamp>] [<level>] [<tag>] [<message>]
Example: [16:10:29 GMT­0700 (PDT).245] [DEBUG] [plugin::player] Resolving qos.startupTime: 0
```

* **tijdstempel:** Dit is de huidige CPU-tijd (tijdzone voor GMT)
* **niveau:** Er zijn vier berichtniveaus gedefinieerd:
   * INFO - Meestal worden de invoergegevens van de toepassing (naam van speler valideren, video-id enzovoort)
   * DEBUG - zuivert logboeken, die door de ontwikkelaars worden gebruikt om complexere kwesties te zuiveren
   * WAARSCHUWING - Geeft mogelijke integratie-/configuratiefouten of fouten in de SDK van Heartbeats aan
   * FOUT - Geeft belangrijke integratiefouten of fouten in de SDK van Heartbeats aan
* **tag:** De naam van de subcomponent die het logboekbericht heeft uitgegeven (gewoonlijk de klassenaam)
* **bericht:** Het daadwerkelijke spoorbericht

U kunt de logboekoutput door de bibliotheek van SDK van Media gebruiken om de implementatie te verifiëren. Een goede strategie is door de logboeken naar de tekenreeks te zoeken `#track`. Hiermee worden alle `track*()` oproepen die door uw toepassing worden gemaakt.

Dit is bijvoorbeeld waar de logbestanden voor zijn gefilterd `#track` zou er als volgt kunnen uitzien:

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
