---
title: De SDK van Media instellen in iOS
description: Voer de volgende stappen uit om de Media SDK-toepassing in iOS in te stellen.
uuid: a1c6be79-a6dc-47b6-93b3-ac7b42f1f3eb
exl-id: fe7662b5-1700-4bd6-b542-66aa8493459d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 5%

---

# iOS instellen{#set-up-ios}

Leer hoe u de functie voor het instellen van streaming media-analyse voor iOS-apparaten instelt.

>[!IMPORTANT]
>
>Aan het einde van de ondersteuning voor versie 4 Mobile SDK&#39;s op 31 augustus 2021 beëindigt Adobe ook de ondersteuning voor de Media Analytics SDK voor iOS en Android.  Zie voor meer informatie [Veelgestelde vragen over einde van ondersteuning voor Media Analytics SDK](/help/additional-resources/end-of-support-faqs.md).

## Vereisten

* **Geldige configuratieparameters verkrijgen voor de Media SDK**
Deze parameters kunt u verkrijgen van een Adobe-medewerker nadat u uw analyseaccount hebt ingesteld.
* **ADBMobile for iOS in uw toepassing implementeren**
Voor meer informatie over de documentatie van Adobe Mobile SDK, zie [iOS SDK 4.x voor Experience Cloud Solutions.](https://experienceleague.adobe.com/docs/mobile-services/ios/overview.html)

   >[!IMPORTANT]
   >
   >Vanaf iOS 9 introduceerde Apple de functie App Transport Security (ATS). Deze functie is bedoeld om de netwerkbeveiliging te verbeteren door ervoor te zorgen dat uw apps alleen industriestandaard protocollen en ciphers gebruiken. Deze functie is standaard ingeschakeld, maar u hebt configuratieopties die u opties bieden voor het werken met ATS. Zie voor meer informatie over ATS [Toepassingstransportbeveiliging.](https://experienceleague.adobe.com/docs/mobile-services/ios/config-ios/app-transport-security.html)

* **Biedt de volgende mogelijkheden in uw mediaspeler:**

   * _Een API die zich moet abonneren op spelergebeurtenissen_ - De SDK van Media vereist dat u een set eenvoudige API&#39;s oproept wanneer gebeurtenissen in de speler plaatsvinden.
   * _Een API die spelerinformatie biedt_ - Deze informatie bevat details zoals de medianaam en de positie van de afspeelkop.

## SDK-implementatie

>[!IMPORTANT]
>
>Vanaf versie 2.3.0 wordt de SDK gedistribueerd via XCFrameworks.
>
>Versie 2.3.0 van de SDK vereist Xcode 12.0 of hoger en, indien van toepassing, Cocoapods 1.10.0 of hoger.

* Telkens wanneer een binair bibliotheekdossier wordt vermeld, zou zijn vervanging XCFraframework in plaats daarvan moeten worden gebruikt:
   * MediaSDK.a > MediaSDK.xcframework
   * MediaSDK_TV.a > MediaSDKTV.xframework
* Als manueel het toevoegen van Adobe XCFrameworks aan uw project, zorg ervoor dat zij niet ingebed zijn.

1. Voeg uw [gedownload](/help/getting-started/download-sdks.md) Media SDK voor uw project.

   1. Controleer of de volgende softwarecomponenten voorkomen in het dialoogvenster `libs` map:

      * `ADBMediaHeartbeat.h`: Het objectc-headerbestand dat wordt gebruikt voor iOS-API&#39;s voor het bijhouden van hartslagen.
      * `ADBMediaHeartbeatConfig.h`: Het objectief-C kopbaldossier voor de configuratie van SDK.
      * `MediaSDK.a`: Een binaire bitcode met vet die de bibliotheekbuilds bevat voor iOS-apparaten (armv7, armv7s, arm64) en -simulatoren (i386 en x86_64).

         Dit binaire bestand moet worden gekoppeld wanneer het doel is bedoeld voor een iOS-app.

      * `MediaSDK_TV.a`: Een binaire bitcode met vet die de bibliotheek bevat, maakt gebruik van nieuwe Apple TV-apparaten (arm64) en simulator (x86_64).

         Dit binaire bestand moet worden gekoppeld wanneer het doel is bedoeld voor een Apple TV-app (tvOS).
   1. Voeg de bibliotheek aan uw project toe:

      1. Start de Xcode-IDE en open uw app.
      1. In **[!UICONTROL Project Navigator]**, sleept u de `libs` en zet deze onder uw project neer.

      1. Zorg ervoor dat de **[!UICONTROL Copy Items if Needed]** Selectievakje is geselecteerd. **[!UICONTROL Create Groups]** is geselecteerd en zijn er geen selectievakjes ingeschakeld **[!UICONTROL Add to Target]** zijn geselecteerd.

      ![Opties kiezen](assets/choose-options_ios.png)

      1. Klik op **[!UICONTROL Finish]**.
      1. In **[!UICONTROL Project Navigator]** selecteert u uw app en selecteert u uw doelen.
      1. Koppel de vereiste frameworks en bibliotheken in de secties **[!UICONTROL Linked Frameworks]** en **[!UICONTROL Libraries]** op het tabblad **[!UICONTROL General]**.

         **iOS App-doelen:**

         * **AdobeMobileLibrary.a**
         * **MediaSDK.a**
         * **libsqlite3.0.tbd**

         **Apple TV (tvOS)-doelen:**

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

1. Een `ADBMediaHeartbeatConfig` -instantie.

   Deze sectie helpt u begrijpen `MediaHeartbeat` config parameters, en om correcte config waarden op uw te plaatsen `MediaHeartbeat` -instantie voor nauwkeurige tracering.

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

1. Implementeer de `ADBMediaHeartbeatDelegate` protocol.

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

1. Gebruik de `ADBMediaHeartBeatConfig` en `ADBMediaHeartBeatDelegate` om de `ADBMediaHeartbeat` -instantie.

   ```
   //Replace <ADBMediaHeartBeatDelegate> with your delegate instance
   _mediaHeartbeat = [[ADBMediaHeartbeat alloc] initWithDelegate:
     <ADBMediaHeartBeatDelegate> config:config];
   ```

   >[!IMPORTANT]
   >
   >Zorg ervoor dat uw `ADBMediaHeartbeat` -instantie toegankelijk is en *wordt pas aan het einde van de sessie detoegewezen*. Deze instantie wordt gebruikt voor alle volgende gebeurtenissen tracking.

## Migreren van versie 1.x naar 2.x in iOS {#migrate-to-two-x}

In versie 2.x worden alle methoden van het type public geconsolideerd in de `ADBMediaHeartbeat` om het voor ontwikkelaars gemakkelijker te maken. Alle configuraties zijn geconsolideerd in de `ADBMediaHeartbeatConfig` klasse.

Raadpleeg de documentatie bij Oudere implementatie voor informatie over het migreren van 1.x naar 2.x.)

## Een native app voor tvOS configureren

Met de release van de nieuwe Apple TV kunt u nu toepassingen maken die in de native tvOS-omgeving kunnen worden uitgevoerd. U kunt een puur eigen app maken met behulp van een van de verschillende frameworks die beschikbaar zijn in iOS, of u kunt uw app maken met XML-sjablonen en JavaScript. Vanaf MediaSDK versie 2.0 is ondersteuning voor tvOS beschikbaar. Voor meer informatie over tvOS raadpleegt u [tvOS Developer-site.](https://developer.apple.com/tvos/)

Voer de volgende stappen in uw project Xcode uit. In deze handleiding wordt ervan uitgegaan dat uw project een doel heeft dat een Apple TV-app voor tvOS is:

1. Sleep de `VideoHeartbeat_TV.a` bibliotheekbestand in het project `lib` map.

1. Vouw op het tabblad **[!UICONTROL Build Phases]** van het doel van uw tvOS-app de sectie **[!UICONTROL Link Binary with Libraries]** uit en voeg de volgende bibliotheken toe:

   * `MediaSDK_TV.a`
   * `AdobeMobileLibrary_TV.a`
   * `libsqlite3.0.tbd`
   * `SystemConfiguration.framework`
