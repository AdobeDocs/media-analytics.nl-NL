---
title: Foutopsporing in SDK
description: Meer informatie over het bijhouden/registreren in Media SDK.
uuid: a5972d87-c593-4b4f-a56f-dca6e25268e1
exl-id: c2de6454-8538-4d07-a099-e278b153d894
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# Foutopsporing in SDK{#sdk-debugging}

U kunt logbestanden in- en uitschakelen. Media SDK verstrekt een uitgebreid het vinden/registreren mechanisme door de media-volgende stapel. U kunt registratie in- of uitschakelen door de markering `debugLogging` op het Config-object in te stellen.

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

De bibliotheek ADBMobile biedt foutopsporingslogboekregistratie via de methode `setDebugLogging` . Foutopsporingslogbestand moet worden ingesteld op `false` voor alle productie-apps.

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

* **timestamp:** dit is de huidige tijd van CPU (tijd-die voor GMT wordt geplaatst)
* **niveau:** er zijn 4 bepaalde berichtniveaus:
   * INFO - Meestal worden de invoergegevens van de toepassing (naam van speler valideren, video-id enzovoort)
   * DEBUG - zuivert logboeken, die door de ontwikkelaars worden gebruikt om complexere kwesties te zuiveren
   * WARN - Geeft mogelijke integratie-/configuratiefouten of Heartbeats SDK-bugs aan
   * FOUT - Geeft belangrijke integratiefouten of Heartbeats SDK-bugs aan
* **markering:** de naam van sub-component die het logboekbericht (gewoonlijk de klassennaam) uitbracht
* **bericht:** het daadwerkelijke spoorbericht

U kunt de logboekoutput door de bibliotheek van Media SDK gebruiken om de implementatie te verifiëren. Een goede strategie is door de logboeken naar de tekenreeks `#track` te zoeken. Hiermee worden alle `track*()` -aanroepen van uw toepassing gemarkeerd.

Zo zouden de voor `#track` gefilterde logboeken er bijvoorbeeld als volgt kunnen uitzien:

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
