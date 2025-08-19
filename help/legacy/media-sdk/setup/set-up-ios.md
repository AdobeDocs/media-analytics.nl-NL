---
title: Media SDK instellen op iOS
description: Voer de volgende stappen uit om de Media SDK-toepassing in iOS in te stellen.
uuid: a1c6be79-a6dc-47b6-93b3-ac7b42f1f3eb
exl-id: fe7662b5-1700-4bd6-b542-66aa8493459d
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 3%

---

# IOS instellen{#set-up-ios}

Leer de streaming-mediaservices voor iOS-apparaten in te stellen.

>[!IMPORTANT]
>
>Met het einde van de ondersteuning voor versie 4 Mobile SDK&#39;s op 31 augustus 2021 beëindigt Adobe ook de ondersteuning voor Media Analytics SDK voor iOS en Android.  Voor extra informatie, zie [ Analytics SDK End-of-Support FAQs ](/help/additional-resources/end-of-support-faqs.md).

## Vereisten

* **verkrijg geldige configuratieparameters voor de Media SDK**
Deze parameters kunt u verkrijgen van een Adobe-medewerker nadat u uw analyseaccount hebt ingesteld.
* **voert ADBMobile voor iOS in uw toepassing uit**
Voor meer informatie over de documentatie van Adobe Mobile SDK, zie [ iOS SDK 4.x voor de Oplossingen van Experience Cloud.](https://experienceleague.adobe.com/docs/mobile-services/ios/overview.html)

  >[!IMPORTANT]
  >
  >Vanaf iOS 9 introduceerde Apple de functie App Transport Security (ATS). Deze functie is bedoeld om de netwerkbeveiliging te verbeteren door ervoor te zorgen dat uw apps alleen industriestandaard protocollen en ciphers gebruiken. Deze functie is standaard ingeschakeld, maar u hebt configuratieopties die u opties bieden voor het werken met ATS. Voor details op ATS, zie [ de Veiligheid van het Vervoer van de Toepassing.](https://experienceleague.adobe.com/docs/mobile-services/ios/config-ios/app-transport-security.html)

* **verstrek de volgende mogelijkheden in uw media speler:**

   * _API om aan spelergebeurtenissen_ in te tekenen - de Media SDK vereist dat u een reeks eenvoudige APIs roept wanneer de gebeurtenissen in uw speler voorkomen.
   * _API die spelerinformatie_ verstrekt - Deze informatie omvat details zoals de media naam en de positie van het spelhoofd.

## SDK-implementatie

>[!IMPORTANT]
>
>Vanaf versie 2.3.0 wordt de SDK gedistribueerd via XCFrameworks.
>
>Versie 2.3.0 van de SDK vereist Xcode 12.0 of nieuwer en, indien van toepassing, Cocoapods 1.10.0 of hoger.

* Telkens wanneer een binair bibliotheekdossier wordt vermeld, zou zijn vervanging XCFraframework in plaats daarvan moeten worden gebruikt:
   * MediaSDK.a > MediaSDK.xcframework
   * MediaSDK_TV.a > MediaSDKTV.xframework
* Als u de Adobe XCFrameworks handmatig aan uw project toevoegt, moet u ervoor zorgen dat deze niet zijn ingesloten.

1. Voeg uw [ gedownloade ](/help/getting-started/download-sdks.md) Media SDK aan uw project toe.

   1. Controleer of de volgende softwarecomponenten in de map `libs` staan:

      * `ADBMediaHeartbeat.h`: Het objectc-headerbestand dat wordt gebruikt voor API&#39;s voor het bijhouden van hartslagen van iOS.
      * `ADBMediaHeartbeatConfig.h`: Het objectc-headerbestand voor de SDK-configuratie.
      * `MediaSDK.a`: Een binaire bitcode voor vet die de bibliotheekbuilds bevat voor iOS-apparaten (armv7, armv7s, arm64) en -simulatoren (i386 en x86_64).

        Dit binaire bestand moet worden gekoppeld wanneer het doel is bedoeld voor een iOS-app.

      * `MediaSDK_TV.a`: Een binair vet met bitcode dat de bibliotheek bevat voor nieuwe Apple TV-apparaten (arm64) en simulator (x86_64).

        Dit binaire bestand moet worden gekoppeld wanneer het doel is bedoeld voor een Apple TV-app (tvOS).

   1. Voeg de bibliotheek aan uw project toe:

      1. Start de Xcode-IDE en open uw app.
      1. Sleep de map **[!UICONTROL Project Navigator]** in `libs` naar de map onder het project.

      1. Zorg ervoor dat het selectievakje **[!UICONTROL Copy Items if Needed]** is ingeschakeld, dat **[!UICONTROL Create Groups]** is geselecteerd en dat geen van de selectievakjes in **[!UICONTROL Add to Target]** is geselecteerd.

      ![ kies Opties ](assets/choose-options_ios.png)

      1. Klik op **[!UICONTROL Finish]**.
      1. Selecteer in **[!UICONTROL Project Navigator]** uw app en selecteer uw doelen.
      1. Koppel de vereiste frameworks en bibliotheken in de secties **[!UICONTROL Linked Frameworks]** en **[!UICONTROL Libraries]** op het tabblad **[!UICONTROL General]**.

         **iOS App Doelen:**

         * **AdobeMobileLibrary.a**
         * **MediaSDK.a**
         * **libsqlite3.0.tbd**

         **Apple TV (tvOS) Doelen:**

         * **AdobeMobileLibrary_TV.a**
         * **MediaSDK_TV.a**
         * **libsqlite3.0.tbd**
         * **SystemConfiguration.framework**

      1. Controleer of uw app zonder fouten is opgebouwd.

1. Importeer de bibliotheek.

   ```
   #import "ADBMediaHeartbeat.h"
   #import "ADBMediaHeartbeatConfig.h"
   ```

1. Maak een `ADBMediaHeartbeatConfig` -instantie.

   Deze sectie helpt u om de `MediaHeartbeat` config parameters te begrijpen, en correcte config waarden op uw `MediaHeartbeat` instantie voor nauwkeurige het volgen te plaatsen.

   Hier volgt een voorbeeld van initialisatie van `ADBMediaHeartbeatConfig`:

   ```
   // Media Heartbeat Initialization
   ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init];
   config.trackingServer = <SAMPLE_HEARTBEAT_TRACKING_SERVER>;
   config.channel        = <SAMPLE_HEARTBEAT_CHANNEL>;
   config.appVersion     = <SAMPLE_HEARTBEAT_SDK_VERSION>;
   config.ovp            = <SAMPLE_HEARTBEAT_OVP_NAME>;
   config.playerName     = <SAMPLE_PLAYER_NAME>;
   config.ssl            = <YES/NO>;
   config.debugLogging   = <YES/NO>;
   ```

1. Implementeer het protocol `ADBMediaHeartbeatDelegate` .

   ```
   @interface VideoAnalyticsProvider : NSObject <ADBMediaHeartbeatDelegate>
   
   @end
   
   @implementation VideoAnalyticsProvider
   
   // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames>  
   // with the current playback QoS values.
   - (ADBMediaObject *)getQoSObject {
       return [ADBMediaHeartbeat createQoSObjectWithBitrate:<bitrate>  
                                 startupTime:<startuptime>   
                                 fps:<fps>  
                                 droppedFrames:<droppedFrames>];
   }
   
   // Return the current video player playhead position.
   // Replace <currentPlaybackTime> with the video player current playback time
   - (NSTimeInterval)getCurrentPlaybackTime {
       return <currentPlaybackTime>;
   }
   
   @end
   ```

1. Gebruik `ADBMediaHeartBeatConfig` en `ADBMediaHeartBeatDelegate` om de instantie `ADBMediaHeartbeat` te maken.

   ```
   //Replace <ADBMediaHeartBeatDelegate> with your delegate instance
   _mediaHeartbeat = [[ADBMediaHeartbeat alloc] initWithDelegate:
     <ADBMediaHeartBeatDelegate> config:config];
   ```

   >[!IMPORTANT]
   >
   >Zorg ervoor dat uw `ADBMediaHeartbeat` instantie toegankelijk is en *wordt niet gedealloceerd tot het eind van de zitting*. Deze instantie wordt gebruikt voor alle volgende gebeurtenissen tracking.

## Migreren van versie 1.x naar 2.x in iOS {#migrate-to-two-x}

In versie 2.x worden alle methoden van het type public geconsolideerd in de klasse `ADBMediaHeartbeat` , zodat ontwikkelaars deze eenvoudiger kunnen gebruiken. Alle configuraties zijn geconsolideerd in de klasse `ADBMediaHeartbeatConfig` .

Raadpleeg de documentatie bij Oudere implementatie voor informatie over het migreren van 1.x naar 2.x.)

## Een native app voor tvOS configureren

Met de release van de nieuwe Apple TV kunt u nu toepassingen maken die in de native tvOS-omgeving kunnen worden uitgevoerd. U kunt een puur eigen app maken met behulp van een van de verschillende frameworks die beschikbaar zijn in iOS, of u kunt uw app maken met XML-sjablonen en JavaScript. Vanaf MediaSDK versie 2.0 is ondersteuning voor tvOS beschikbaar. Voor meer informatie over tvOS, zie {de plaats van de Ontwikkelaar 0} tvOS.[](https://developer.apple.com/tvos/)

Voer de volgende stappen in uw project Xcode uit. In deze handleiding wordt ervan uitgegaan dat uw project een doel heeft dat een Apple TV-app voor tvOS is:

1. Sleep het bibliotheekbestand van `VideoHeartbeat_TV.a` naar de map `lib` van uw project.

1. Vouw op het tabblad **[!UICONTROL Build Phases]** van het doel van uw tvOS-app de sectie **[!UICONTROL Link Binary with Libraries]** uit en voeg de volgende bibliotheken toe:

   * `MediaSDK_TV.a`
   * `AdobeMobileLibrary_TV.a`
   * `libsqlite3.0.tbd`
   * `SystemConfiguration.framework`
