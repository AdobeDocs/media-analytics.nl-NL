---
title: Koppelingen openen om Media Analytics SDK's te downloaden
description: Koppelingen naar SDK-downloads voor beschikbare platforms, zoals Android, iOS, JavaScript, Chromecast en Roku.
uuid: a619fbb8-693e-4583-8dad-0ff875e715f8
exl-id: d211fa2e-d5b0-4e9f-bdb7-eda838194f3d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 1%

---

# SDK&#39;s van media, extensies met tags en OTT SDK&#39;s ophalen {#download-sdks}

De informatie op deze pagina bevat koppelingen waarmee u de huidige media-SDK&#39;s kunt downloaden en de media-extensies kunt ophalen.

De informatie op deze pagina bevat koppelingen naar het downloaden van de huidige Media SDK&#39;s en naar het verkrijgen van de Media Extensions die tags gebruiken.

Tags in Adobe Experience Platform zijn de volgende generatie mogelijkheden voor websitetags en beheer van mobiele SDK&#39;s van Adobe. Tags bieden een eenvoudige manier om de oplossingen voor analyse, marketing en reclame die nodig zijn om relevante ervaringen van klanten te verbeteren, in te zetten en te beheren. Voor meer informatie over tags raadpleegt u [Overzicht van codes](https://experienceleague.adobe.com/docs/platform-learn/data-collection/overview.html?lang=nl)


>[!NOTE]
>
>Voor informatie over het downloaden van verouderde SDK&#39;s raadpleegt u [Verouderd—SDK&#39;s downloaden](/help/legacy/legacy-download-sdks.md).<br>
>Voor belangrijke informatie over eind-van-steun, zie [Veelgestelde vragen over einde ondersteuning](/help/additional-resources/end-of-support-faqs.md).

## Media SDK&#39;s en mobiele bibliotheken {#media-sdks-libraries}

### Webimplementatie {#download-web-sdk}

| Ondersteund Platform | Versie |  API&#39;s   |  Documentatie  |  Monster  |
|:---:|---|---|---|---|
| ![JavaScript-pictogram](assets/javascript-icon.png) | Web - [Media SDK voor JS v3.0.2](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2) | [JavaScript API-naslaggids](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) | [Media SDK v3.x voor JavaScript instellen](/help/implementation/media-sdk/setup/web-implementation.md) | [Media SDK voor JS v3.0.2-voorbeeld](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/js/3.x) |
| ![JavaScript-pictogram](assets/javascript-icon.png) | Web - Media-extensie |  | [Adobe Media Analytics (3.x SDK) voor audio- en videoextensie — gebruik van Tags (gegevensverzameling)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=en) | [Voorbeeld van Adobe Media-analyse (3.x SDK) voor audio- en video-extensie](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x) |

### Mobiele implementatie {#get-mobile-extension}

| Ondersteund Platform | Versie |  Documentatie   |  Voorbeelden  |
|:---:|---|---|---|
| ![Android-pictogram](assets/android-icon.png) | Android - Media-extensie | [Mobiele SDK-documentatie](https://developer.adobe.com/client-sdks/documentation/) | [Adobe Analytics - Media Analytics for Audio and Video Sample](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/mobile/android) |
| ![Apple iOS-pictogram](assets/ios-icon.png)<br>tvOS-pictogram toevoegen | iOS / tvOS - Media Extension | [Mobiele SDK-documentatie](https://developer.adobe.com/client-sdks/documentation/) | [Adobe Analytics - Media Analytics for Audio and Video Sample](https://github.com/adobe/aepsdk-media-ios/tree/main/TestApp) |

### Bovenste implementatie {#download-ott-libraries}

| Ondersteund Platform | Versie |  API&#39;s   |  Documentatie  |
|:---:|---|---|---|
| ![Chromecast-pictogram](assets/chromecast-icon.png) | [SDK voor Chromecast v3.0.3](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3) | [Referentie voor Chromecast API](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/) | [Mobile SDK v3.x voor Chromecast instellen](/help/implementation/media-sdk/setup/set-up-chromecast.md) |
| ![Roku-pictogram](assets/roku-icon.png) | [SDK voor Roku v2.2.6](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.6) | [Roku API-naslaggids](/help/implementation/media-sdk/setup/set-up-roku.md) | [Mobile SDK v2.x voor Roku instellen](/help/implementation/media-sdk/setup/set-up-roku.md) |

## Adobe-extensies {#adobe-extensions}

### Streaming media-extensie {#streaming-media-extension}

De **Adobe Media Analytics voor audio- en video-extensie** vereist Adobe Analytics for Media add-on SKU. Neem voor meer informatie contact op met uw Adobe-verkoper, accountmanager of Customer Success Manager.

Voor gedetailleerde informatie over het installeren, configureren en implementeren van de **Adobe Media Analytics voor audio- en video-extensie**, zie [Overzicht van Adobe Media Analytics voor audio- en video-extensie](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=en) en [De extensie Media Analytics configureren](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics#configure-the-media-analytics-extension).

### Extensie Analytics {#analytics-extension}

[Analyse Extension v1.6 of hoger](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=en)—Met deze extensie kunt u de Javascript-bibliotheek van de Adobe Experience Platform Web SDK laden om gegevens naar Adobe-oplossingen te verzenden. De **Extensie Analytics** v1.6 of hoger is vereist.

Voor informatie over het configureren van deze extensie raadpleegt u [De Adobe Analytics-extensie configureren](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=en).

### Experience Cloud ID-extensie {#cloud-id-extension}

[Experience Cloud ID-extensie](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=en)—Deze extensie implementeert de Experience Cloud ID Service, die bezoekers identificeert voor alle Experience Cloud-oplossingen. De Experience Cloud ID Service is een personalisatie-uitbreiding in Adobe Experience Platform.

Gebruik deze uitbreiding om de Dienst van de Identiteit van de Experience Cloud met uw bezit te integreren. Met de Experience Cloud Identity Service kunt u unieke en permanente id&#39;s voor bezoekers van uw site maken en opslaan.

Voor informatie over het configureren van deze extensie raadpleegt u [De extensie Experience Cloud-id configureren](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=en)
