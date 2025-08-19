---
title: Media SDK instellen op Android
description: Voer de volgende stappen uit om de Media SDK-toepassing in Android in te stellen.
uuid: 3ffe3276-a104-4182-9220-038729e9f3d5
exl-id: 261445bf-3c8b-4658-891d-9a878e0b26ea
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 6%

---

# Android instellen{#set-up-android}

Leer hoe u streaming-mediaservices instelt voor Android-apparaten.

>[!IMPORTANT]
>
>Met het einde van de ondersteuning voor versie 4 Mobile SDK&#39;s op 31 augustus 2021 beëindigt Adobe ook de ondersteuning voor Media Analytics SDK voor iOS en Android.  Voor extra informatie, zie [ Analytics SDK End-of-Support FAQs ](/help/additional-resources/end-of-support-faqs.md).


## Vereisten

* **verkrijg geldige configuratieparameters voor de Media SDK**
Deze parameters kunt u verkrijgen van een Adobe-medewerker nadat u uw analyseaccount hebt ingesteld.
* **voert ADBMobile voor Android in uw toepassing uit**
Voor meer informatie over de documentatie van Adobe Mobile SDK, zie [ Android SDK 4.x voor de Oplossingen van Experience Cloud.](https://experienceleague.adobe.com/docs/mobile-services/android/overview.html?lang=nl-NL)

* **verstrek de volgende mogelijkheden in uw media speler:**
   * *API om aan spelergebeurtenissen* in te tekenen - de Media SDK vereist dat u een reeks eenvoudige APIs roept wanneer de gebeurtenissen in uw speler voorkomen.
   * *API die spelerinformatie* verstrekt - Deze informatie omvat details zoals de media naam en de positie van het spelhoofd.

## SDK-implementatie

1. Voeg uw gedownloade Media SDK toe aan uw project.

   1. Vouw het ZIP-bestand van Android uit (bijvoorbeeld `MediaSDK-android-v2.*.zip` ).
   1. Controleer of het `MediaSDK.jar` -bestand in de map `libs/` staat.

   1. Voeg de bibliotheek aan uw project toe.

      **IntelliJ IDEA:**

      1. Klik met de rechtermuisknop op uw project in het deelvenster **[!UICONTROL Project navigation]**.
      1. Selecteer **[!UICONTROL Open Module Settings]** .
      1. Selecteer onder **[!UICONTROL Project Settings]** de optie **[!UICONTROL Libraries]** .

      1. Klik op **[!UICONTROL +]** om een nieuwe bibliotheek toe te voegen.
      1. Selecteer **[!UICONTROL Java]** en ga naar het `MediaSDK.jar` -bestand.

      1. Selecteer de modules waarin u de mobiele bibliotheek wilt gebruiken.
      1. Klik op **[!UICONTROL Apply]** en vervolgens op **[!UICONTROL OK]** om het venster met module-instellingen te sluiten.

      **Verduistering:**

      1. In winde van de Verduistering, klik op de projectnaam met de rechtermuisknop aan.
      1. Klik op **[!UICONTROL Build Path]** > **[!UICONTROL Add External Archives]** .
      1. Selecteer `MediaSDK.jar` .
      1. Klik op **[!UICONTROL Open]**.
      1. Klik nogmaals met de rechtermuisknop op het project en klik op **[!UICONTROL Build Path]** > **[!UICONTROL Configure Build Path]** .
      1. Klik op de tabbladen **[!UICONTROL Order]** en **[!UICONTROL Export]**.

      1. Zorg ervoor dat het `MediaSDK.jar` -bestand is geselecteerd.

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

1. Implementeer de interface `MediaHeartbeatDelegate` .

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

   Gebruik de instantie `MediaHeartbeatConfig` en de instantie `MediaHertbeatDelegate` om de instantie `MediaHeartbeat` te maken.

   ```java
   // Replace <MediaHertbeatDelegate> with your delegate instance
   MediaHeartbeat _heartbeat =  
     new MediaHeartbeat(<MediaHeartbeatDelegate>, config);
   ```

   >[!IMPORTANT]
   >
   >Zorg ervoor dat uw `MediaHeartbeat` instantie toegankelijk is en *wordt niet gedealloceerd tot het eind van de zitting*. Deze instantie wordt gebruikt voor alle volgende gebeurtenissen tracking.

**Toevoegend app toestemmingen**

Uw toepassing die Media SDK gebruikt, vereist de volgende machtigingen om gegevens te verzenden bij het bijhouden van aanroepen:

* `INTERNET`
* `ACCESS_NETWORK_STATE`

Voeg de volgende regels toe aan uw `AndroidManifest.xml` -bestand in de projectmap van de toepassing om deze machtigingen toe te voegen:

* `<uses-permission android:name="android.permission.INTERNET" />`
* `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />`

**migrerend van versie 1.x aan 2.x in Android**

In versies 2.x worden alle methoden van het type public geconsolideerd in de klasse `com.adobe.primetime.va.simple.MediaHeartbeat` , zodat ontwikkelaars deze eenvoudiger kunnen gebruiken. Bovendien worden alle configuraties nu geconsolideerd in de klasse `com.adobe.primetime.va.simple.MediaHeartbeatConfig` .

Raadpleeg de documentatie bij Legacy Implementation voor informatie over het migreren van 1.x naar 2.x.
