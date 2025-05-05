---
title: Koppelingen openen om Media Analytics SDK's te downloaden
description: Koppelingen naar SDK-downloads voor beschikbare platforms, zoals Android, iOS, JavaScript, Chromecast en Roku.
uuid: a619fbb8-693e-4583-8dad-0ff875e715f8
exl-id: d211fa2e-d5b0-4e9f-bdb7-eda838194f3d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 9%

---

# SDK&#39;s van media, extensies met tags en OTT SDK&#39;s ophalen {#download-sdks}

De informatie op deze pagina bevat koppelingen waarmee u de huidige media-SDK&#39;s kunt downloaden en de media-extensies kunt ophalen die tags gebruiken.

Tags in Adobe Experience Platform zijn de volgende generatie websitetags en beheermogelijkheden voor mobiele SDK van de Adobe. Tags bieden een eenvoudige manier om de oplossingen voor analyse, marketing en reclame die nodig zijn om relevante ervaringen van klanten te verbeteren, in te zetten en te beheren. Voor extra informatie over markeringen, zie [ overzicht van Markeringen ](https://experienceleague.adobe.com/docs/platform-learn/data-collection/overview.html?lang=en).


>[!NOTE]
>
>Voor informatie over het downloaden van erfenis SDKs, zie [ verouderd-download SDKs ](/help/legacy/legacy-download-sdks.md).<br>
>Voor belangrijke informatie over eind-van-steun, zie [ Einde van de Veelgestelde vragen van de Steun ](/help/additional-resources/end-of-support-faqs.md).

## Media-SDK&#39;s en mobiele bibliotheken {#media-sdks-libraries}

### Webimplementatie {#download-web-sdk}

| Ondersteund platform | Ondersteunde oplossingen | Implementatiemethode | Versie |  API&#39;s   |  Documentatie  |  Monster  |
|:---:|---|---|---|---| ---| ---|
| ![ het pictogram van JavaScript ](assets/javascript-icon.png)</br>**JavaScript API** | Adobe Analytics | Alleen analyse | Web - [ Media SDK voor JS v3.0.2 ](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2) | [ JavaScript API Verwijzing ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) | [ installeer de Media SDK gebruikend JavaScript ](/help/implementation/media-sdk/setup/web-implementation.md) | [ Media SDK voor JS v3.0.2 Steekproef ](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/js/3.x) |
| ![ het pictogram van JavaScript ](assets/javascript-icon.png)</br>**JavaScript API** | Adobe Analytics | Alleen analyse | Web - Media Extension |  | [ Analytics van Adobe Media (3.x SDK) voor Audio en Video uitbreiding - gebruikend Markeringen (de Inzameling van Gegevens) ](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=en) | [ Analytics van Adobe Media (3.x SDK) voor Audio en de VideoSteekproef van de Uitbreiding ](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x) |
| </br>**Web** | Adobe Analytics<p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | Web - Experience Platform Edge |  | [ voer de Streaming Inzameling van Media uit gebruikend de Edge Network ](/help/implementation/edge/implementation-edge.md) <p>en</p><p>[ verzendt de gegevens van het Web naar Edge met het Web SDK van Adobe Experience Platform ](/help/implementation/edge/edge-web-sdk.md)</p> | |

### Mobiele implementatie {#get-mobile-extension}

| Ondersteund platform | Ondersteunde oplossingen | Implementatiemethode | Versie |  Documentatie   |  Voorbeelden  |
|:---:|---|---|---|---|---|
| ![ het pictogram van Android ](assets/android-icon.png)</br>**Android** | Adobe Analytics | Alleen analyse | Android - Media Extension | [ Mobiele documentatie van SDK ](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [ Adobe Analytics - Analytics van Media voor Audio en Videosteekproef ](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/mobile/android) |
| ![&#128279;](assets/ios-icon.png)<br>**tvOS** het pictogram van iOS van 0&rbrace; Apple | Adobe Analytics | Alleen analyse | iOS / tvOS - Media Extension | [ Mobiele documentatie van SDK ](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [ Adobe Analytics - Analytics van Media voor Audio en Videosteekproef ](https://github.com/adobe/aepsdk-media-ios/tree/main/TestApp) |
| ![ het pictogram van Android ](assets/android-icon.png)</br>**Android** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | ANDROID - EXPERIENCE PLATFORM EDGE | [ installeer de Media SDK gebruikend JavaScript ](/help/implementation/edge/implementation-edge.md) | |
| ![&#128279;](assets/ios-icon.png)<br>**tvOS** het pictogram van iOS van 0&rbrace; Apple | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | iOS / tvOS - Experience Platform Edge | [ installeer de Media SDK gebruikend JavaScript ](/help/implementation/edge/implementation-edge.md) |  |

### Bovenste implementatie {#download-ott-libraries}

| Ondersteund platform | Ondersteunde oplossingen | Implementatiemethode | Versie |  API&#39;s   |  Documentatie  |
|:---:|---|---|---|---|---|
| ![ Chromecast pictogram ](assets/chromecast-icon.png)</br>**Chromecast** | Adobe Analytics | Alleen analyse | [ SDK voor Chromecast v3.0.3 ](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3) | [ Chromecast API Verwijzing ](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/) | [ Mobiele SDK v3.x van de Opstelling voor Chromecast ](/help/implementation/media-sdk/setup/set-up-chromecast.md) |
| ![ het pictogram van Roku ](assets/roku-icon.png)</br>**Roku** | Adobe Analytics | Alleen analyse | [ SDK voor Roku v2.2.6 ](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.6) |  | [ Mobiele SDK v2.x van de Opstelling voor Roku ](/help/implementation/media-sdk/setup/set-up-roku.md) |
| ![ het pictogram van Roku ](assets/roku-icon.png)</br>**Roku** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | [ Adobe Experience Platform Roku SDK ](https://github.com/adobe/aepsdk-roku/tree/main) |  | [ installeer de Media SDK gebruikend JavaScript ](/help/implementation/edge/implementation-edge.md) |
