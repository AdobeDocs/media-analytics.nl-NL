---
title: De SDK van Media instellen in Android
description: Voer de volgende stappen uit om de Media SDK-toepassing in Android in te stellen.
uuid: 3ffe3276-a104-4182-9220-038729e9f3d5
exl-id: 261445bf-3c8b-4658-891d-9a878e0b26ea
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 6%

---

# Android instellen{#set-up-android}

Leer hoe u de invoegtoepassing voor de verzameling van streaming media instelt voor Android-apparaten.

>[!IMPORTANT]
>
>Met het einde van de ondersteuning voor versie 4 Mobile SDK&#39;s op 31 augustus 2021 beëindigt Adobe ook de ondersteuning voor de Media Analytics SDK voor iOS en Android.  Zie voor meer informatie [Veelgestelde vragen over einde van ondersteuning voor Media Analytics SDK](/help/additional-resources/end-of-support-faqs.md).


## Vereisten

* **Geldige configuratieparameters verkrijgen voor de Media SDK**
Deze parameters kunt u verkrijgen van een Adobe-medewerker nadat u uw analyseaccount hebt ingesteld.
* **ADBMobile for Android in uw toepassing implementeren**
Voor meer informatie over de documentatie van de Adobe Mobiele SDK, zie [Android SDK 4.x voor Experience Cloud Solutions.](https://experienceleague.adobe.com/docs/mobile-services/android/overview.html)

* **Biedt de volgende mogelijkheden in uw mediaspeler:**
   * *Een API die zich moet abonneren op spelergebeurtenissen* - De SDK van Media vereist dat u een set eenvoudige API&#39;s oproept wanneer gebeurtenissen in de speler plaatsvinden.
   * *Een API die spelerinformatie biedt* - Deze informatie bevat details zoals de medianaam en de positie van de afspeelkop.

## SDK-implementatie

1. Voeg de gedownloade SDK van Media toe aan uw project.

   1. Het ZIP-bestand van Android uitvouwen (bijvoorbeeld `MediaSDK-android-v2.*.zip`).
   1. Controleer of de `MediaSDK.jar` bestand bestaat in `libs/` directory.

   1. Voeg de bibliotheek aan uw project toe.

      **IntelliJ IDEA:**

      1. Klik met de rechtermuisknop op uw project in het deelvenster **[!UICONTROL Project navigation]**.
      1. Selecteren **[!UICONTROL Open Module Settings]**.
      1. Onder **[!UICONTROL Project Settings]**, selecteert u **[!UICONTROL Libraries]**.

      1. Klikken **[!UICONTROL +]** een nieuwe bibliotheek toevoegen.
      1. Selecteren **[!UICONTROL Java]** en navigeer naar de `MediaSDK.jar` bestand.

      1. Selecteer de modules waarin u de mobiele bibliotheek wilt gebruiken.
      1. Klik op **[!UICONTROL Apply]** en vervolgens op **[!UICONTROL OK]** om het venster met module-instellingen te sluiten.

      **Eclipse:**

      1. In winde van de Verduistering, klik op de projectnaam met de rechtermuisknop aan.
      1. Klikken  **[!UICONTROL Build Path]** > **[!UICONTROL Add External Archives]** .
      1. Selecteren `MediaSDK.jar`.
      1. Klik op **[!UICONTROL Open]**.
      1. Klik nogmaals met de rechtermuisknop op het project en klik op  **[!UICONTROL Build Path]** > **[!UICONTROL Configure Build Path]** .
      1. Klik op de tabbladen **[!UICONTROL Order]** en **[!UICONTROL Export]**.

      1. Zorg ervoor dat de `MediaSDK.jar` bestand is geselecteerd.

1. Importeer de bibliotheek.

   ```java
   import com.adobe.primetime.va.simple.MediaHeartbeat;
   import com.adobe.primetime.va.simple.MediaHeartbeat.MediaHeartbeatDelegate;
   import com.adobe.primetime.va.simple.MediaHeartbeatConfig;
   import com.adobe.primetime.va.simple.MediaObject;
   ```

1. Maak de `MediaHeartbeatConfig` -instantie.

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

1. Maak de `MediaHeartbeat` -instantie.

   Gebruik de `MediaHeartbeatConfig` en de `MediaHertbeatDelegate` instantie om de `MediaHeartbeat` -instantie.

   ```java
   // Replace <MediaHertbeatDelegate> with your delegate instance
   MediaHeartbeat _heartbeat =  
     new MediaHeartbeat(<MediaHeartbeatDelegate>, config);
   ```

   >[!IMPORTANT]
   >
   >Zorg ervoor dat uw `MediaHeartbeat` -instantie toegankelijk is en *wordt pas aan het einde van de sessie detoegewezen*. Deze instantie wordt gebruikt voor alle volgende gebeurtenissen tracking.

**Toepassingsmachtigingen toevoegen**

Uw toepassing die de SDK van Media gebruikt vereist de volgende toestemmingen om gegevens te verzenden bij het volgen van vraag:

* `INTERNET`
* `ACCESS_NETWORK_STATE`

Voeg de volgende regels toe aan uw `AndroidManifest.xml` bestand in de projectmap van de toepassing:

* `<uses-permission android:name="android.permission.INTERNET" />`
* `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />`

**Migreren van versie 1.x naar 2.x in Android**

In versies 2.x, worden alle openbare methodes geconsolideerd in `com.adobe.primetime.va.simple.MediaHeartbeat` om het voor ontwikkelaars gemakkelijker te maken. Bovendien worden alle configuraties nu geconsolideerd in de `com.adobe.primetime.va.simple.MediaHeartbeatConfig` klasse.

Raadpleeg de documentatie bij Legacy Implementation voor informatie over het migreren van 1.x naar 2.x.
