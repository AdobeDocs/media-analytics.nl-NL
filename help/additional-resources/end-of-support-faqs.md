---
title: Meer informatie over de veelgestelde vragen over Media Analytics SDK End of Support
description: Dit onderwerp omvat FAQs over het eind van steun voor Media Analytics SDKs.
exl-id: 9601ec17-8421-49d0-9d81-1cfa5e8f37cf
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---

# Veelgestelde vragen over einde van ondersteuning voor Media Analytics Mobile SDK

Met het einde van de ondersteuning voor versie 4 Mobile SDK&#39;s op 31 augustus 2021 beëindigde Adobe ook de ondersteuning voor de Media Analytics Mobile SDK&#39;s voor iOS en Android. (Hieronder vallen niet de Media Analytics SDK for web (JS) en OTT-platforms zoals Chromecast en Roku, die nog steeds worden ondersteund.)

Dit betekent dat Adobe geen oplossingen, updates voor het besturingssysteem of ondersteuning voor Media Analytics Mobile SDK meer biedt. Wanneer het migreren aan nieuwe Experience Platform SDKs, me ervan bewust ben dat de [&#x200B; uitbreidingen van de Analyse van Media &#x200B;](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) moeten worden uitgevoerd om de het stromen van Adobe media diensten toe te laten.


## Top 5 van dingen die u moet weten

1. Mobiele v4-SDK&#39;s worden niet meer ondersteund vanaf 31 augustus 2021. Migreer naar de Adobe Experience Platform (AEP) Mobile SDK&#39;s voor iOS en Android.

1. Voor een Adobe-implementatie van streaming media services is de AEP Mobile SDK vereist en moet u de extensies Analytics en Media Analytics gebruiken. Vanaf 1 september 2021 moet u de nieuwe AEP Mobile SDK&#39;s en uitbreidingen gebruiken.  De uitbreidingen van de Analytics van media worden gevormd gebruikend de Markeringen van Adobe (gegevensinzameling). Voor extra informatie, zie [&#x200B; Migrerend van Stand-alone Media SDK aan de Lancering van Adobe &#x200B;](/help/legacy/sdk-to-launch/sdk-to-launch-migration.md)

1. De ontwikkeling van functies voor de Media Analytics SDK&#39;s voor iOS en Android is beëindigd. Nieuwe functies die zijn geïntroduceerd vanaf Fall 2019 worden ingeschakeld met de extensies Media Analytics en Media Collection API.

1. De SDK&#39;s van Roku en Chromecast blijven beschikbaar voor klanten met Adobe Analytics for Streaming Media Add-on en de invoegtoepassing Customer Journey Analytics Streaming Media Collection. De SDK&#39;s van Roku en Chromecast zullen verder worden verbeterd en ondersteund als zelfstandige SDK&#39;s. Als u de JS SDK for Media Analytics gebruikt, kunt u de zelfstandige SDK blijven gebruiken of de extensie Media Analytics inschakelen met Adobe Data Collection (voorheen Adobe Launch).

Neem contact op met uw Adobe-accountteam als u vragen hebt.

## Veelgestelde vragen

1. **zal steun voor Roku en Chromecast SDKs worden beïnvloed? &#x200B;**

   Nee.  Roku- en Chromecast SDK&#39;s blijven voorlopig ondersteund als zelfstandige SDK&#39;s. &#x200B;
&#x200B;
1. **zal de implementaties van JS SDK van de Analytics van Media door deze verandering worden beïnvloed? &#x200B;**

   Nee.  Klanten die de JS SDK for Media Analytics gebruiken, kunnen de SDK blijven gebruiken of inschakelen via Adobe Launch.
&#x200B;
1. **wat is het niveau van inspanning om aan de uitbreidingen van de Analytics van Media te migreren? &#x200B;**

   LOE is afhankelijk van de implementatie van elke klant, dus het zal variëren.  Nadat u de migratiedocumentatie hieronder hebt bekeken, neemt u contact op met de consultant en/of de klantenservice voor extra ondersteuning.

[Media Analytics Extensions: Android-migratie](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)

[Media Analytics Extensions: iOS-migratie](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)

   [&#x200B; Uitbreidingen van de Analytics van Media: nieuwe implementaties &#x200B;](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)

1. **moet ik Lanceren als systeem van het markeringsbeheer hebben? Wat als ik geen Lancering wil gebruiken?**

   Voor het gebruik van de mobiele app wordt Launch niet gebruikt als een systeem voor tagbeheer zoals voor het web. Voor het configureren van de SDK-extensies is het gebruik van de opstartinterface vereist. Dit is vergelijkbaar met de manier waarop u de gebruikersinterface van Adobe Mobile Services gebruikt om de mobiele v4 SDK te configureren. Voor installatie, is het voordeel van het gebruiken van Lancering dat het u aangepaste installatieinstructies geeft die op de uitbreiding worden gebaseerd u kiest.

1. **beïnvloedt dit eind van steun SDK voor tvOS?**

   Ja, voor tvOS (versie 10+) is de aanbevolen implementatie het migreren naar de Media Analytics Extensions. Voor extra informatie, zie [&#x200B; Migrerend van de standalone SDK van Media aan de Lancering van Adobe - iOS &#x200B;](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md).

1. **beïnvloedt dit eind van steun SDK voor VuurTV en AndroidTV? &#x200B;**

   Ja, voor Fire TV en AndroidTV is de aanbevolen implementatie het migreren naar de Media Analytics Extensions. Voor extra informatie, zie [&#x200B; Migrerend van de standalone SDK van Media aan de Lancering van Adobe - Android &#x200B;](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md).
