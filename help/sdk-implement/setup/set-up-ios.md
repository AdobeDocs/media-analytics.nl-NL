---
title: Media-SKD instellen op iOS
description: Voer de volgende stappen uit om de Media SDK-toepassing op iOS in te stellen.
uuid: a1c6be79-a6dc-47b6-93b3-ac7b42f1f3eb
exl-id: fe7662b5-1700-4bd6-b542-66aa8493459d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 5%

---

# iOS instellen{#set-up-ios}

>[!IMPORTANT]
>
>Aan het einde van de ondersteuning voor versie 4 Mobile SDK&#39;s op 31 augustus 2021 beëindigt Adobe ook de ondersteuning voor de Media Analytics SDK voor iOS en Android.  Voor extra informatie, zie [Van begin tot eind - van - de Veelgestelde vragen van de Analyse van Media SDK](/help/sdk-implement/end-of-support-faqs.md).

## Vereisten

* **Verkrijg geldige configuratieparameters voor de Media**
SDKTDeze parameters kunnen van een vertegenwoordiger van Adobe worden verkregen nadat u opstelling uw analytische rekening.
* **ADBMobile for iOS implementeren in uw**
toepassingZie  [iOS SDK 4.x voor Experience Cloud Solutions voor meer informatie over de documentatie van de Adobe Mobile SDK.](https://experienceleague.adobe.com/docs/mobile-services/ios/overview.html)

   >[!IMPORTANT]
   >
   >Vanaf iOS 9 introduceerde Apple de functie App Transport Security (ATS). Deze functie is bedoeld om de netwerkbeveiliging te verbeteren door ervoor te zorgen dat uw apps alleen industriestandaard protocollen en ciphers gebruiken. Deze functie is standaard ingeschakeld, maar u hebt configuratieopties die u opties bieden voor het werken met ATS. Voor details op ATS, zie [de Veiligheid van het Vervoer van de app.](https://experienceleague.adobe.com/docs/mobile-services/ios/config-ios/app-transport-security.html)

* **Biedt de volgende mogelijkheden in uw mediaspeler:**

   * _Een API die zich moet abonneren op spelergebeurtenissen_ . De Media SDK vereist dat u een set eenvoudige API&#39;s aanroept wanneer gebeurtenissen in de speler plaatsvinden.
   * _Een API die spelerinformatie_  verschaft. Deze informatie bevat details zoals de medianaam en de positie van de afspeelkop.

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

1. Voeg uw [gedownloade](/help/sdk-implement/download-sdks.md#download-2x-sdks) SDK van Media aan uw project toe.

   1. Verifieer dat de volgende softwarecomponenten in `libs` folder bestaan:

      * `ADBMediaHeartbeat.h`: Het objectc-headerbestand dat wordt gebruikt voor iOS-API&#39;s voor het bijhouden van hartslagen.
      * `ADBMediaHeartbeatConfig.h`: Het objectief-C kopbaldossier voor de configuratie van SDK.
      * `MediaSDK.a`: Een binaire bitcode met vet die de bibliotheekbuilds voor iOS-apparaten (armv7, armv7s, arm64) en simulatoren (i386 en x86_64) bevat.

         Dit binaire bestand moet worden gekoppeld wanneer het doel is bedoeld voor een iOS-app.

      * `MediaSDK_TV.a`: Een binaire bitcode met vet die de bibliotheek bevat, wordt gemaakt voor nieuwe Apple TV-apparaten (arm64) en simulator (x86_64).

         Dit binaire bestand moet worden gekoppeld wanneer het doel is bedoeld voor een Apple TV-app (tvOS).
   1. Voeg de bibliotheek aan uw project toe:

      1. Start de Xcode-IDE en open uw app.
      1. In **[!UICONTROL Project Navigator]**, sleep `libs` folder en laat vallen het onder uw project.

      1. Zorg ervoor dat het selectievakje **[!UICONTROL Copy Items if Needed]** is ingeschakeld, dat **[!UICONTROL Create Groups]** is geselecteerd en dat geen van de selectievakjes in **[!UICONTROL Add to Target]** zijn geselecteerd.

         ![](assets/choose-options_ios.png)

      1. Klik op **[!UICONTROL Finish]**.
      1. Selecteer uw app in **[!UICONTROL Project Navigator]** en selecteer uw doelen.
      1. Koppel de vereiste frameworks en bibliotheken in de secties **[!UICONTROL Linked Frameworks]** en **[!UICONTROL Libraries]** op het tabblad **[!UICONTROL General]**.

         **iOS App-doelen:**

         * **AdobeMobileLibrary.a**
         * **MediaSDK.a**
         * **libsqlite3.0.tbd**

         **Doelstellingen van Apple TV (tvOS):**

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

1. Maak een `ADBMediaHeartbeatConfig`-instantie.

   Deze sectie helpt u om de `MediaHeartbeat` configuratieparameters te begrijpen, en correcte configuratiewaarden op uw &lt;a1 te plaatsen/> instantie voor nauwkeurige het volgen.`MediaHeartbeat`

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

1. Implementeer het `ADBMediaHeartbeatDelegate`-protocol.

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

1. Gebruik `ADBMediaHeartBeatConfig` en `ADBMediaHeartBeatDelegate` om de `ADBMediaHeartbeat` instantie tot stand te brengen.

   ```
   //Replace <ADBMediaHeartBeatDelegate> with your delegate instance
   _mediaHeartbeat = [[ADBMediaHeartbeat alloc] initWithDelegate:
     <ADBMediaHeartBeatDelegate> config:config];
   ```

   >[!IMPORTANT]
   >
   >Zorg ervoor dat uw `ADBMediaHeartbeat` instantie toegankelijk is en *wordt niet deassigned tot het eind van de zitting*. Deze instantie wordt gebruikt voor alle volgende gebeurtenissen tracking.

## Migreren van versie 1.x naar 2.x in iOS {#migrate-to-two-x}

In versie 2.x, worden alle openbare methodes geconsolideerd in de `ADBMediaHeartbeat` klasse om het voor ontwikkelaars gemakkelijker te maken. Alle configuraties zijn geconsolideerd in de klasse `ADBMediaHeartbeatConfig`.

Voor meer informatie over het migreren van 1.x aan 2.x, zie [VHL 1.x aan Migratie 2.x.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)

## Een native app voor tvOS configureren

Met de release van de nieuwe Apple TV kunt u nu toepassingen maken die in de systeemeigen tvOS-omgeving kunnen worden uitgevoerd. U kunt een puur eigen app maken met behulp van een van de verschillende frameworks die beschikbaar zijn in iOS, of u kunt uw app maken met XML-sjablonen en JavaScript. Vanaf MediaSDK versie 2.0 is ondersteuning voor tvOS beschikbaar. Zie [tvOS Developer-site](https://developer.apple.com/tvos/) voor meer informatie over tvOS.

Voer de volgende stappen in uw project Xcode uit. In deze handleiding wordt ervan uitgegaan dat uw project een doel heeft dat een Apple TV-app voor tvOS is:

1. Sleep het `VideoHeartbeat_TV.a` bibliotheekdossier in `lib` omslag van uw project.

1. Vouw op het tabblad **[!UICONTROL Build Phases]** van het doel van uw tvOS-app de sectie **[!UICONTROL Link Binary with Libraries]** uit en voeg de volgende bibliotheken toe:

   * `MediaSDK_TV.a`
   * `AdobeMobileLibrary_TV.a`
   * `libsqlite3.0.tbd`
   * `SystemConfiguration.framework`
