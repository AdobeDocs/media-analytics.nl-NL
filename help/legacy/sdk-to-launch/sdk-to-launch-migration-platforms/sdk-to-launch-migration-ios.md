---
title: "Migreren van de standalone Media SDK naar Adobe Launch - iOS"
description: Leer hoe u van de SDK van Media naar Launch voor iOS migreert.
exl-id: f70b8e1b-cb9f-4230-86b2-171bdaed4615
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# Migreren van de standalone Media SDK naar Adobe Launch - iOS

>[!NOTE]
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=en) voor een geconsolideerde referentie van de terminologische wijzigingen.

## Configuratie

### Standalone Media SDK

In de standalone SDK van Media, vormt u de het volgen configuratie in app, en gaat het tot SDK over wanneer u de trekker creeert.

```objective-c
ADBMediaHeartbeatConfig *config =
  [[ADBMediaHeartbeatConfig alloc] init];

config.trackingServer = @"namespace.hb.omtrdc.net";
config.channel = @"sample-channel";
config.appVersion = @"v2.0.0";
config.ovp = @"video-provider";
config.playerName = @"native-player";
config.ssl = YES;
config.debugLogging = YES;

ADBMediaHeartbeat* tracker =
  [[ADBMediaHeartbeat alloc] initWithDelegate:self config:config];
```

### Extensie starten

1. Klik in het Experience Platform Launch op de knop [!UICONTROL Extensions] tab voor uw mobiele eigenschap
1. Op de [!UICONTROL Catalog] , zoekt u de Adobe Media Analytics for Audio and Video-extensie en klikt u op [!UICONTROL Install].
1. In de pagina van de uitbreidingsmontages, vorm de volgende parameters.
De uitbreiding van Media zal de gevormde parameters voor het volgen gebruiken.

   ![](assets/launch_config_mobile.png)

[De extensie Media Analytics configureren](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

## Beheer maken

### Standalone Media SDK

In de standalone SDK van Media maakt u handmatig de `ADBMediaHeartbeatConfig` en configureert u de volgende parameters. Implementeer de gedelegeerde interface die de
`getQoSObject()` en `getCurrentPlaybackTime()functions.`

Maak een MediaHeartbone-instantie die u wilt bijhouden:

```objective-c
@interface PlayerDelegate : NSObject<ADBMediaHeartbeatDelegate>
@end

@implementation PlayerDelegate {
}

- (NSTimeInterval) getCurrentPlaybackTime {
    // When called should return the current player time in seconds.
    return playhead_;
}

- (nonnull ADBMediaObject*) getQoSObject {
    // When called should return the latest qos values.
    return qosObject_;
}
@end

ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init];

config.trackingServer = @"namespace.hb.omtrdc.net";
config.channel = @"sample-channel";
config.appVersion = @"app-version";
config.ovp = @"video-provider";
config.playerName = @"native-player";
config.ssl = YES;
config.debugLogging = YES;
ADBMediaHeartbeatDelegate* delegate = [[PlayerDelegate alloc] init];

ADBMediaHeartbeat* tracker =
  [[ADBMediaHeartbeat alloc] initWithDelegate:delegate config:config];
```

### Extensie starten

[Referentie voor media-API: Media Beheer maken](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#create-a-media-tracker)

Registreer de media-extensie en de afhankelijke extensies bij de mobiele kern voordat u de Beheer maakt.

```objective-c
// Register the extension once during app launch
#import <ACPCore.h>
#import <ACPAnalytics.h>
#import <ACPMedia.h>
#import <ACPIdentity.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [ACPCore setLogLevel:ACPMobileLogLevelDebug];
    [ACPCore configureWithAppId:@"your-launch-app-id"];
    [ACPMedia registerExtension];
    [ACPAnalytics registerExtension];
    [ACPIdentity registerExtension];
    [ACPCore start:nil];
    return YES;
}
```

Zodra de media-extensie is geregistreerd, kan de tracker worden gemaakt met de volgende API.
Tracker selecteert automatisch de configuratie van het gevormde lanceringsbezit.

```objective-c
[ACPMedia createTracker:^(ACPMediaTracker * _Nullable mediaTracker) {
    // Use the instance for tracking media.
}];
```

## Waarden voor afspeelkop en kwaliteit van ervaring bijwerken.

### Standalone Media SDK

In de standalone SDK van Media, een afgevaardigde voorwerp dat uitvoert
`ADBMediaHeartbeartDelegate` protocol wordt overgegaan tijdens het creëren van de trekker.
De implementatie zou recentste QoE en playhead moeten terugkeren telkens als de trekker de `getQoSObject()` en `getCurrentPlaybackTime()` interfacemethoden.

### Extensie starten

De huidige afspeelkop van de speler moet worden bijgewerkt met de functie
`updateCurrentPlayhead` door de verklikker aan het licht gebrachte methode. Voor het nauwkeurig volgen zou u deze methode minstens eens per seconde moeten roepen.

[Referentie voor media-API: huidige afspeelknop bijwerken](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updatecurrentplayhead)

De implementatie moet de QoE-informatie bijwerken door de
`updateQoEObject` door de verklikker aan het licht gebrachte methode. U zou deze methode moeten roepen wanneer er een verandering in de kwaliteitsmetriek is.

[Referentie voor media-API - QoE-object bijwerken](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updateqoeobject)

## Standaardmedia/metagegevens doorgeven

### Standalone Media SDK

* Metagegevens standaardmedia:

   ```objective-c
   ADBMediaObject *mediaObject =
     [ADBMediaHeartbeat createMediaObjectWithName:@"media-name"
                        mediaId:@"media-id"
                        length:60
                        streamType:ADBMediaHeartbeatStreamTypeVod
                        mediaType:ADBMediaTypeVideo];
   
   // Standard metadata keys provided by adobe.
   NSMutableDictionary *standardMetadata = [[NSMutableDictionary alloc] init];
   [standardMetadata setObject:@"Sample show" forKey:ADBVideoMetadataKeySHOW];
   [standardMetadata setObject:@"Sample season" forKey:ADBVideoMetadataKeySEASON];
   [mediaObject setValue:standardMetadata forKey:ADBMediaObjectKeyStandardMediaMetadata];
   
   //Attaching custom metadata
   NSMutableDictionary *videoMetadata = [[NSMutableDictionary alloc] init];
   [mediaMetadata setObject:@"false" forKey:@"isUserLoggedIn"];
   [mediaMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
   
   [tracker trackSessionStart:mediaObject data:mediaMetadata];
   ```

* Standaard advertentiemetagegevens:

   ```objective-c
   ADBMediaObject* adObject =
     [ADBMediaHeartbeat createAdObjectWithName:[adData objectForKey:@"name"]
                        adId:[adData objectForKey:@"id"]
                        position:[[adData objectForKey:@"position"] doubleValue]
                        length:[[adData objectForKey:@"length"] doubleValue]];
   
   // Standard metadata keys provided by adobe.
   NSMutableDictionary *standardMetadata =
     [[NSMutableDictionary alloc] init];
   [standardMetadata setObject:@"Sample Advertiser"
                     forKey:ADBAdMetadataKeyADVERTISER];
   [standardMetadata setObject:@"Sample Campaign"
                     forKey:ADBAdMetadataKeyCAMPAIGN_ID];
   [adObject setValue:standardMetadata
                     forKey:ADBMediaObjectKeyStandardAdMetadata];
   
   //Attaching custom metadata
   NSMutableDictionary *adDictionary = [[NSMutableDictionary alloc] init];
   [adDictionary setObject:@"Sample affiliate" forKey:@"affiliate"];
   
   [tracker trackEvent:ADBMediaHeartbeatEventAdStart
            mediaObject:adObject
            data:adDictionary];
   ```

### Extensie starten

* Metagegevens standaardmedia:

   ```objective-c
   NSDictionary *mediaObject =
     [ACPMedia createMediaObjectWithName:@"media-name"
               mediaId:@"media-id"
               length:60
               streamType:ACPMediaStreamTypeVod
               mediaType:ACPMediaTypeVideo];
   
   NSMutableDictionary *mediaMetadata =
     [[NSMutableDictionary alloc] init];
   
   // Standard metadata keys provided by adobe.
   [mediaMetadata setObject:@"Sample show" forKey:ACPVideoMetadataKeyShow];
   [mediaMetadata setObject:@"Sample season" forKey:ACPVideoMetadataKeySeason];
   
   // Custom metadata keys
   [mediaMetadata setObject:@"false" forKey:@"isUserLoggedIn"];
   [mediaMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
   [_tracker trackSessionStart:mediaObject data:mediaMetadata];
   ```

* Standaard advertentiemetagegevens:

   ```objective-c
   NSDictionary* adObject =
     [ACPMedia createAdObjectWithName:@"ad-name"
               adId:@"ad-id"
               position:1
               length:15];
   
   NSMutableDictionary* adMetadata =
     [[NSMutableDictionary alloc] init];
   
   // Standard metadata keys provided by adobe.
   [adMetadata setObject:@"Sample Advertiser" forKey:ACPAdMetadataKeyAdvertiser];
   [adMetadata setObject:@"Sample Campaign" forKey:ACPAdMetadataKeyCampaignId];
   
   // Custom metadata keys
   [adMetadata setObject:@"Sample affiliate" forKey:@"affiliate"];
   
   [tracker trackEvent:ACPMediaEventAdStart mediaObject:adObject data:adMetadata];
   ```
