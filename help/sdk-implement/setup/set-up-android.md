---
title: Media-SKD instellen op Android
description: Voer de volgende stappen uit om de Media SDK-toepassing op Android in te stellen.
uuid: 3ffe3276-a104-4182-9220-038729e9f3d5
exl-id: 261445bf-3c8b-4658-891d-9a878e0b26ea
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 8%

---

# Android instellen{#set-up-android}

>[!IMPORTANT]
>
>Aan het einde van de ondersteuning voor versie 4 Mobile SDK&#39;s op 31 augustus 2021 beëindigt Adobe ook de ondersteuning voor de Media Analytics SDK voor iOS en Android.  Voor extra informatie, zie [Van begin tot eind - van - de Veelgestelde vragen van de Analyse van Media SDK](/help/sdk-implement/end-of-support-faqs.md).


## Vereisten

* **Verkrijg geldige configuratieparameters voor de Media**
SDKTDeze parameters kunnen van een vertegenwoordiger van Adobe worden verkregen nadat u opstelling uw analytische rekening.
* **ADBMobile for Android implementeren in uw**
toepassingZie  [Android SDK 4.x voor Experience Cloud Solutions voor meer informatie over de documentatie van de Adobe Mobile SDK.](https://experienceleague.adobe.com/docs/mobile-services/android/overview.html)

* **Biedt de volgende mogelijkheden in uw mediaspeler:**
   * *Een API die zich moet abonneren op spelergebeurtenissen* . De Media SDK vereist dat u een set eenvoudige API&#39;s aanroept wanneer gebeurtenissen in de speler plaatsvinden.
   * *Een API die spelerinformatie*  verschaft. Deze informatie bevat details zoals de medianaam en de positie van de afspeelkop.

## SDK-implementatie

1. Voeg uw [gedownloade](/help/sdk-implement/download-sdks.md#download-2x-sdks) SDK van Media aan uw project toe.

   1. Vouw het ZIP-bestand voor Android uit (bijvoorbeeld `MediaSDK-android-v2.*.zip`).
   1. Controleer of het `MediaSDK.jar`-bestand in de map `libs/` aanwezig is.

   1. Voeg de bibliotheek aan uw project toe.

      **IntelliJ IDEA:**

      1. Klik met de rechtermuisknop op uw project in het deelvenster **[!UICONTROL Project navigation]**.
      1. Selecteer **[!UICONTROL Open Module Settings]**.
      1. Selecteer onder **[!UICONTROL Project Settings]** de optie **[!UICONTROL Libraries]**.

      1. Klik **[!UICONTROL +]** om een nieuwe bibliotheek toe te voegen.
      1. Selecteer **[!UICONTROL Java]** en navigeer aan het `MediaSDK.jar` dossier.

      1. Selecteer de modules waarin u de mobiele bibliotheek wilt gebruiken.
      1. Klik op **[!UICONTROL Apply]** en vervolgens op **[!UICONTROL OK]** om het venster met module-instellingen te sluiten.

      **Eclipse:**

      1. In winde van de Verduistering, klik op de projectnaam met de rechtermuisknop aan.
      1. Klik op  **[!UICONTROL Build Path]** > **[!UICONTROL Add External Archives]** .
      1. Selecteer `MediaSDK.jar`.
      1. Klik op **[!UICONTROL Open]**.
      1. Klik nogmaals met de rechtermuisknop op het project en klik op **[!UICONTROL Build Path]** > **[!UICONTROL Configure Build Path]**.
      1. Klik op de tabbladen **[!UICONTROL Order]** en **[!UICONTROL Export]**.

      1. Zorg ervoor dat het `MediaSDK.jar`-bestand is geselecteerd.


1. Importeer de bibliotheek.

   ```java
   import com.adobe.primetime.va.simple.MediaHeartbeat;
   import com.adobe.primetime.va.simple.MediaHeartbeat.MediaHeartbeatDelegate;
   import com.adobe.primetime.va.simple.MediaHeartbeatConfig;
   import com.adobe.primetime.va.simple.MediaObject;
   ```

1. Maak de instantie `MediaHeartbeatConfig`.

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

1. Implementeer de interface `MediaHeartbeatDelegate`.

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

1. Maak de instantie `MediaHeartbeat`.

   Gebruik de instantie `MediaHeartbeatConfig` en de instantie `MediaHertbeatDelegate` om de instantie `MediaHeartbeat` te maken.

   ```java
   // Replace <MediaHertbeatDelegate> with your delegate instance
   MediaHeartbeat _heartbeat =  
     new MediaHeartbeat(<MediaHeartbeatDelegate>, config);
   ```

   >[!IMPORTANT]
   >
   >Zorg ervoor dat uw `MediaHeartbeat` instantie toegankelijk is en *wordt niet deassigned tot het eind van de zitting*. Deze instantie wordt gebruikt voor alle volgende gebeurtenissen tracking.

**Toepassingsmachtigingen toevoegen**

Uw toepassing die de SDK van Media gebruikt vereist de volgende toestemmingen om gegevens te verzenden bij het volgen van vraag:

* `INTERNET`
* `ACCESS_NETWORK_STATE`

Om deze toestemmingen toe te voegen, voeg de volgende lijnen aan uw `AndroidManifest.xml` dossier in de folder van het toepassingsproject toe:

* `<uses-permission android:name="android.permission.INTERNET" />`
* `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />`

**Migreren van versie 1.x naar 2.x in Android**

In versies 2.x, worden alle openbare methodes geconsolideerd in de `com.adobe.primetime.va.simple.MediaHeartbeat` klasse om het voor ontwikkelaars gemakkelijker te maken. Bovendien worden alle configuraties nu geconsolideerd in de klasse `com.adobe.primetime.va.simple.MediaHeartbeatConfig`.

Voor gedetailleerde informatie over het migreren van 1.x naar 2.x, zie [mig-1x-2x-overview.md.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
