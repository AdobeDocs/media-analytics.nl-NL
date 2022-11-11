---
title: Meer informatie over ondersteunde apparaten en Platforms
description: "Meer informatie over de belangrijkste apparaten die Adobe Analytics for Streaming Media ondersteunt, zoals iOS, Android, OTT-apparaten en JavaScript-browsers."
exl-id: 169ff7b9-e577-45b7-8927-74bdcccc0a77
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: d89b2af2e2ae5a170ce98f62656cdeed6fe31f19
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 18%

---

# Ondersteunde apparaten en platforms {#devices-supported}

>[!IMPORTANT]
>
>Aan het einde van de ondersteuning voor versie 4 Mobile SDK&#39;s op 31 augustus 2021 beëindigt Adobe ook de ondersteuning voor de Media Analytics SDK voor iOS en Android.  Zie voor meer informatie [Veelgestelde vragen over einde van ondersteuning voor Media Analytics SDK](/help/sdk-implement/end-of-support-faqs.md).

Adobe Analytics for Streaming Media ondersteunt alle belangrijke apparaten, waaronder:

* iOS- en Android-smartphones en -tablets
* OTT-apparaten voor ROKU, AppleTV, FireTV en Android TV
* JavaScript-browser voor desktop en laptop

De SDK&#39;s van Media worden regelmatig bijgewerkt wanneer nieuwe versies van apparaten worden uitgebracht en u kunt de SDK gebruiken om te integreren met de grootste mediaspelers, waaronder Brightcove en Ooyala.

Voor apparaten of platforms die momenteel geen SDK-ondersteuning hebben of in situaties waarin u geen SDK wilt gebruiken, kunt u de API voor mediagroep implementeren. Met de Media Collection API kunt u RESTful-API-aanroepen rechtstreeks van een apparaat of platform naar de achtergrond voor Media Analytics maken.

De onderstaande tabel bevat een lijst met momenteel ondersteunde apparaten en platforms. Zie [SDK&#39;s downloaden voor informatie over het downloaden van de meest recente versie van de SDK](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/download-sdks.html). Als een apparaat niet in de lijst staat, neemt u contact op met uw klantenservice of oplossingsconsultant voor de status van dat apparaat.

| Streaming Platforms en apparaten |  | Gegevensverzameling met AEP Mobile SDK | Media-SDK | Media Collection-API |
|:---------------------------:|:-----------------------------------------------:|:----------------------------:|:-------------------:|:--------------------:|
| Web/Mobiel web |  |  |  |  |
|  | JavaScript-browsers | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png)    | ![](/help/assets/icon-blue-check.png) |
| Mobiele app |  |  |  |  |
|  | iOS-apparaten | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Android-apparaten | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Windows-apparaten |  |  | ![](/help/assets/icon-blue-check.png) |
| OTT |  |  |  |  |
|  | Apple TV (tvOS) | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | ROKU |  | ![](/help/assets/icon-blue-check.png)   <br>(BrightScript)    | ![](/help/assets/icon-blue-check.png)<br>(native) |
|  | Fire TV (Fire OS) | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Android-tv | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Chromecast |  | ![](/help/assets/icon-blue-check.png)    | ![](/help/assets/icon-blue-check.png) |
|  | Gamingconsoles (bijvoorbeeld Xbox ONE, Sony PS3/PS4) |  |  | ![](/help/assets/icon-blue-check.png) |
|  | Bovenste vakken instellen (bijvoorbeeld x1 x xfinity) |  |  | ![](/help/assets/icon-blue-check.png) |
|  | Slimme tv&#39;s (bijvoorbeeld Samsung, LG, Sony, Vizio) |  | ![](/help/assets/icon-blue-check.png)   <br>(webgebaseerd)    | ![](/help/assets/icon-blue-check.png) |
| Overige |  |  |  |  |
|  | Nieuwe aangesloten apparaten |  |  | ![](/help/assets/icon-blue-check.png) |

1. De ondersteuning voor deze SDK&#39;s loopt af op 31 augustus 2021. Zie voor meer informatie [Veelgestelde vragen over einde van ondersteuning voor Media Analytics SDK](/help/sdk-implement/end-of-support-faqs.md).

Voor meer informatie over de minimale platformversies die voor elke SDK worden ondersteund, raadpleegt u [Ondersteuning voor minimale versie van Platform](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/setup/setup-overview.html)
