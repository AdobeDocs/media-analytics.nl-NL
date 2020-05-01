---
title: iOS instellen
description: Installatie van Media SDK-toepassingen voor implementatie op iOS.
uuid: a1c6be79-a6dc-47b6-93b3-ac7b42f1f3eb
translation-type: tm+mt
source-git-commit: be82be2eb58f89344f2125288599fef461db441e

---


# iOS instellen{#set-up-ios}

>[!IMPORTANT]
>
>Vanaf oktober 2020 beëindigt Adobe de ondersteuning voor versie 4 Mobile SDK&#39;s en de standalone Media Analytics SDK&#39;s voor iOS. U kunt de SDK&#39;s van versie 4 blijven downloaden en gebruiken, maar de ondersteuning van de klantenservice en de toegang tot forums zullen worden beëindigd. Migreer naar de SDK&#39;s van het Adobe Experience Platform (AEP) voor iOS. De AEP Mobile SDK (voorheen v5 genoemd) biedt uitsluitend ondersteuning voor functies en functies van Adobe Experience Cloud. Voor meer informatie over deze verandering, zie [versie 4 Mobiele SDKs het Eind van de Veelgestelde vragen](https://aep-sdks.gitbook.io/docs/version-4-sdk-end-of-support-faq)van de Steun. We raden u aan te migreren naar de nieuwe AEP Mobile SDK.
Nadat u naar de AEP Mobile SDK hebt gemigreerd, moet u de extensie Analytics Launch en de extensie Media Analytics Launch implementeren om Adobe Analytics voor Audio en Video in te schakelen. Zie [Migreren van zelfstandige media SDK naar Adobe Launch voor meer informatie over migreren naar de nieuwe AEP Mobile SDK ](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration.html)


## Vereisten

* **Verkrijg geldige configuratieparameters voor de Media SDK** Deze parameters kunnen bij een vertegenwoordiger van Adobe worden verkregen nadat u uw analyseaccount hebt ingesteld.
* **ADBMobile for iOS implementeren in uw toepassing**. Raadpleeg [iOS SDK 4.x voor Experience Cloud Solutions voor meer informatie over de documentatie van Adobe Mobile SDK.](https://docs.adobe.com/content/help/en/mobile-services/ios/overview.html)

   >[!IMPORTANT]
   >
   >Vanaf iOS 9 introduceerde Apple de functie App Transport Security (ATS). Deze functie is bedoeld om de netwerkbeveiliging te verbeteren door ervoor te zorgen dat uw apps alleen industriestandaard protocollen en ciphers gebruiken. Deze functie is standaard ingeschakeld, maar u hebt configuratieopties die u opties bieden voor het werken met ATS. Voor details op ATS, zie de Veiligheid van het Vervoer van de [app.](https://docs.adobe.com/content/help/en/mobile-services/ios/config-ios/app-transport-security.html)

* **Biedt de volgende mogelijkheden in uw mediaspeler:**

   * _Een API die zich moet abonneren op spelergebeurtenissen_ - De Media SDK vereist dat u een set eenvoudige API&#39;s aanroept wanneer gebeurtenissen in de speler plaatsvinden.
   * _Een API die spelerinformatie_ verschaft - Deze informatie bevat details zoals de medianaam en de positie van de afspeelkop.

## SDK-implementatie

1. Voeg uw [gedownloade](/help/sdk-implement/download-sdks.md#download-2x-sdks) SDK van Media aan uw project toe.

   1. Controleer of de volgende softwarecomponenten in de `libs` map aanwezig zijn:

      * `ADBMediaHeartbeat.h`: Het objectc-headerbestand dat wordt gebruikt voor iOS-API&#39;s voor het bijhouden van hartslagen.
      * `ADBMediaHeartbeatConfig.h`: Het objectief-C kopbaldossier voor de configuratie van SDK.
      * `MediaSDK.a`: Een binaire bitcode met vet die de bibliotheekbuilds voor iOS-apparaten (armv7, armv7s, arm64) en simulatoren (i386 en x86_64) bevat.

         Dit binaire bestand moet worden gekoppeld wanneer het doel is bedoeld voor een iOS-app.

      * `MediaSDK_TV.a`: Een binaire bitcode met vet die de bibliotheek bevat, wordt gemaakt voor nieuwe Apple TV-apparaten (arm64) en simulator (x86_64).

         Dit binaire bestand moet worden gekoppeld wanneer het doel is bedoeld voor een Apple TV-app (tvOS).
   1. Voeg de bibliotheek aan uw project toe:

      1. Start de Xcode-IDE en open uw app.
      1. In **[!UICONTROL Project Navigator]**, sleep de `libs` folder en laat vallen het onder uw project.

      1. Zorg ervoor dat het **[!UICONTROL Copy Items if Needed]** selectievakje is ingeschakeld, **[!UICONTROL Create Groups]** is geselecteerd en dat geen van de selectievakjes in **[!UICONTROL Add to Target]** zijn ingeschakeld.

         ![](assets/choose-options_ios.png)

      1. Klik op **[!UICONTROL Finish]**.
      1. Selecteer **[!UICONTROL Project Navigator]** in uw toepassing en selecteer uw doelen.
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

1. Maak een `ADBMediaHeartbeatConfig` instantie.

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

1. Implementeer het `ADBMediaHeartbeatDelegate` protocol.

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

1. Gebruik het `ADBMediaHeartBeatConfig` en `ADBMediaHeartBeatDelegate` om de `ADBMediaHeartbeat` instantie te maken.

   ```
   //Replace <ADBMediaHeartBeatDelegate> with your delegate instance
   _mediaHeartbeat = [[ADBMediaHeartbeat alloc] initWithDelegate:
     <ADBMediaHeartBeatDelegate> config:config];
   ```

   >[!IMPORTANT]
   >
   >Zorg ervoor dat uw `ADBMediaHeartbeat` instantie toegankelijk is en *niet tot het eind van de zitting* wordt gedealloceerd. Deze instantie wordt gebruikt voor alle volgende gebeurtenissen tracking.

## Migreren van versie 1.x naar 2.x in iOS {#migrate-to-two-x}

In versie 2.x worden alle methoden van het type public geconsolideerd in de `ADBMediaHeartbeat` klasse om het voor ontwikkelaars eenvoudiger te maken. Alle configuraties zijn geconsolideerd in de `ADBMediaHeartbeatConfig` klasse.

Zie [VHL 1.x naar 2.x Migratie voor meer informatie over migreren van 1.x naar 2.x.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)

## Een native app voor tvOS configureren

Met de release van de nieuwe Apple TV kunt u nu toepassingen maken die in de systeemeigen tvOS-omgeving kunnen worden uitgevoerd. U kunt een puur eigen app maken met behulp van een van de verschillende frameworks die beschikbaar zijn in iOS, of u kunt uw app maken met XML-sjablonen en JavaScript. Vanaf MediaSDK versie 2.0 is ondersteuning voor tvOS beschikbaar. Zie de [tvOS Developer-site voor meer informatie over tvOS.](https://developer.apple.com/tvos/)

Voer de volgende stappen in uw project Xcode uit. In deze handleiding wordt ervan uitgegaan dat uw project een doel heeft dat een Apple TV-app voor tvOS is:

1. Sleep het `VideoHeartbeat_TV.a` bibliotheekbestand naar de `lib` map van uw project.

1. Vouw op het tabblad **[!UICONTROL Build Phases]** van het doel van uw tvOS-app de sectie **[!UICONTROL Link Binary with Libraries]** uit en voeg de volgende bibliotheken toe:

   * `MediaSDK_TV.a`
   * `AdobeMobileLibrary_TV.a`
   * `libsqlite3.0.tbd`
   * `SystemConfiguration.framework`
