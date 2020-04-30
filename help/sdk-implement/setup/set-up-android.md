---
title: Android instellen
description: Setup van de Media SDK-toepassing voor implementatie op Android.
uuid: 3ffe3276-a104-4182-9220-038729e9f3d5
translation-type: tm+mt
source-git-commit: ccdc3e170d125a76d798be7ce1fa5c12eef1f76a

---


# Android instellen{#set-up-android}

## Vereisten

* **Verkrijg geldige configuratieparameters voor de Media SDK** Deze parameters kunnen bij een vertegenwoordiger van Adobe worden verkregen nadat u uw analyseaccount hebt ingesteld.
* **ADBMobile for Android implementeren in uw toepassing**. Raadpleeg [Android SDK 4.x voor Experience Cloud Solutions voor meer informatie over de documentatie van Adobe Mobile SDK.](https://docs.adobe.com/content/help/en/mobile-services/android/overview.html)
* **Biedt de volgende mogelijkheden in uw mediaspeler:**
   * *Een API die zich moet abonneren op spelergebeurtenissen* - De Media SDK vereist dat u een set eenvoudige API&#39;s aanroept wanneer gebeurtenissen in de speler plaatsvinden.
   * *Een API die spelerinformatie* verschaft - Deze informatie bevat details zoals de medianaam en de positie van de afspeelkop.

## SDK-implementatie

1. Voeg uw [gedownloade](/help/sdk-implement/download-sdks.md#download-2x-sdks) SDK van Media aan uw project toe.

   1. Vouw het ZIP-bestand van Android uit (bijvoorbeeld `MediaSDK-android-v2.*.zip`).
   1. Controleer of het `MediaSDK.jar` bestand in de `libs/` map staat.

   1. Voeg de bibliotheek aan uw project toe.

      **IntelliJ IDEA:**

      1. Klik met de rechtermuisknop op uw project in het deelvenster **[!UICONTROL Project navigation]**.
      1. Selecteer **[!UICONTROL Open Module Settings]**.
      1. Selecteer onder **[!UICONTROL Project Settings]** de optie **[!UICONTROL Libraries]**.

      1. Klik **[!UICONTROL +]** om een nieuwe bibliotheek toe te voegen.
      1. Selecteer **[!UICONTROL Java]** en navigeer naar het `MediaSDK.jar` bestand.

      1. Selecteer de modules waarin u de mobiele bibliotheek wilt gebruiken.
      1. Klik op **[!UICONTROL Apply]** en vervolgens op **[!UICONTROL OK]** om het venster met module-instellingen te sluiten.
      **Eclipse:**

      1. In winde van de Verduistering, klik op de projectnaam met de rechtermuisknop aan.
      1. Klik op  **[!UICONTROL Build Path]** > **[!UICONTROL Add External Archives]** .
      1. Selecteer `MediaSDK.jar`.
      1. Klik op **[!UICONTROL Open]**.
      1. Klik nogmaals met de rechtermuisknop op het project en klik op **[!UICONTROL Build Path]** > **[!UICONTROL Configure Build Path]** .
      1. Klik op de tabbladen **[!UICONTROL Order]** en **[!UICONTROL Export]**.

      1. Zorg ervoor dat het `MediaSDK.jar` bestand is geselecteerd.


1. Importeer de bibliotheek.

   ```java
   import com.adobe.primetime.va.simple.MediaHeartbeat; 
   import com.adobe.primetime.va.simple.MediaHeartbeat.MediaHeartbeatDelegate; 
   import com.adobe.primetime.va.simple.MediaHeartbeatConfig; 
   import com.adobe.primetime.va.simple.MediaObject; 
   ```

1. Maak de `MediaHeartbeatConfig` instantie.

   Hier volgt een voorbeeld van initialisatie van `MediaHeartbeatConfig`:

   ```java
   // Media Heartbeat Initialization 
   config.trackingServer = _<SAMPLE_HEARTBEAT_TRACKING_SERVER>_; 
   config.channel = <SAMPLE_HEARTBEAT_CHANNEL>; 
   config.appVersion = <SAMPLE_HEARTBEAT_SDK_VERSION>; 
   config.ovp =  <SAMPLE_HEARTBEAT_OVP_NAME>; 
   config.playerName = <SAMPLE_PLAYER_NAME>; 
   config.ssl = <true/false>; 
   config.debugLogging = <true/false>; 
   ```

1. Implementeer de `MediaHeartbeatDelegate` interface.

   ```java
   public class VideoAnalyticsProvider implements Observer, MediaHeartbeatDelegate{}
   ```

   ```java
   // Replace <bitrate>, <startupTime>, <fps>, and  
   // <droppeFrames> with the current playback QoS values.  
   @Override 
   public MediaObject getQoSObject() { 
       return MediaHeartbeat.createQoSObject(<bitrate>,  
                                             <startupTime>,  
                                             <fps>,  
                                             <droppedFrames>); 
   } 
   
   //Replace <currentPlaybackTime> with the video player current playback time 
   @Override 
   public Double getCurrentPlaybackTime() { 
       return <currentPlaybackTime>; 
   }
   ```

1. Maak de `MediaHeartbeat` instantie.

   Gebruik de `MediaHeartbeatConfig` instantie en de `MediaHertbeatDelegate` instantie om de `MediaHeartbeat` instantie te maken.

   ```java
   // Replace <MediaHertbeatDelegate> with your delegate instance 
   MediaHeartbeat _heartbeat =  
     new MediaHeartbeat(<MediaHeartbeatDelegate>, config);
   ```

   >[!IMPORTANT]
   >
   >Zorg ervoor dat uw `MediaHeartbeat` instantie toegankelijk is en *niet tot het eind van de zitting* wordt gedealloceerd. Deze instantie wordt gebruikt voor alle volgende gebeurtenissen tracking.

**Toepassingsmachtigingen toevoegen**

Uw toepassing die de SDK van Media gebruikt vereist de volgende toestemmingen om gegevens te verzenden bij het volgen van vraag:

* `INTERNET`
* `ACCESS_NETWORK_STATE`

U voegt deze machtigingen toe door de volgende regels toe te voegen aan uw `AndroidManifest.xml` bestand in de projectmap van de toepassing:

* `<uses-permission android:name="android.permission.INTERNET" />`
* `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />`

**Migreren van versie 1.x naar 2.x in Android**

In versies 2.x worden alle methoden van het type public geconsolideerd in de `com.adobe.primetime.va.simple.MediaHeartbeat` klasse om dit voor ontwikkelaars eenvoudiger te maken. Bovendien worden alle configuraties nu geconsolideerd in de `com.adobe.primetime.va.simple.MediaHeartbeatConfig` klasse.

Voor gedetailleerde informatie over het migreren van 1.x aan 2.x, zie [mig-1x-2x-overview.md.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
