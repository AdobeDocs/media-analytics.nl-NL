---
title: Meer informatie over de veelgestelde vragen over Einde van ondersteuning voor Media Analytics SDK
description: Dit onderwerp omvat FAQs over het eind van steun voor Media Analytics SDKs.
exl-id: 9601ec17-8421-49d0-9d81-1cfa5e8f37cf
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b955b20495a504020a214c3a9e32b676701ee4cc
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 0%

---

# Veelgestelde vragen over einde ondersteuning voor Media Analytics Mobile SDK

Met het einde van de ondersteuning voor versie 4 Mobile SDK&#39;s op 31 augustus 2021 beëindigde Adobe ook de ondersteuning voor de Media Analytics Mobile SDK&#39;s voor iOS en Android. (Dit omvat niet de Media Analytics SDK voor Web (JS) en OTT platforms zoals Chromecast en Roku, die nog worden gesteund.)

Dit betekent dat Adobe niet langer oplossingen, updates met betrekking tot het besturingssysteem of ondersteuning voor de Media Analytics Mobile SDK biedt. Houd er bij het migreren naar de nieuwe Experience Platform-SDK&#39;s rekening mee dat de [Media Analytics-extensies](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) moet worden geïmplementeerd om Adobe Analytics voor Streaming Media in te schakelen.


## Top 5 van dingen die u moet weten

1. Mobiele v4-SDK&#39;s worden niet meer ondersteund vanaf 31 augustus 2021. Migreer naar de Adobe Experience Platform (AEP) Mobile SDK&#39;s voor iOS en Android. Zie voor meer informatie [Versie 4 Veelgestelde vragen over de end-of-support van mobiele SDK&#39;s](https://developer.adobe.com/client-sdks/documentation/v4-end-of-life-faq/).

1. Voor analyse voor de implementatie van Streaming Media is de AEP Mobile SDK en het gebruik van de extensies Analytics en Media Analytics vereist. Vanaf 1 september 2021 moet u de nieuwe AEP Mobile SDK&#39;s en uitbreidingen gebruiken.  De uitbreidingen van de Analytics van media worden gevormd gebruikend de Markeringen van Adobe (gegevensinzameling). Zie voor meer informatie [Migreren van zelfstandige media SDK naar Adobe Launch](/help/legacy/sdk-to-launch/sdk-to-launch-migration.md)

1. De ontwikkeling van functies voor de Media Analytics SDK&#39;s voor iOS en Android is beëindigd. Nieuwe functies die zijn geïntroduceerd vanaf Fall 2019 worden ingeschakeld met de extensies Media Analytics en Media Collection API.

1. De SDK&#39;s van Roku en Chromecast blijven beschikbaar voor Analytics voor klanten van Streaming Media. De SDK&#39;s van Roku en Chromecast zullen verder worden verbeterd en ondersteund als zelfstandige SDK&#39;s. Als u JS SDK voor de Analytics van Media gebruikt, kunt u de stand-alone SDK blijven gebruiken of de uitbreiding van de Analyse van Media toelaten gebruikend de Inzameling van Gegevens van Adobe (vroeger de Lancering van de Adobe).

Neem contact op met uw Adobe-accountteam als u vragen hebt.

## Veelgestelde vragen

1. **Zal de steun voor Roku en Chromecast SDKs worden beïnvloed? &#x200B;**

   Nee.  Roku en Chromecast SDK&#39;s blijven voorlopig ondersteund als zelfstandige SDK&#39;s. &#x200B; &#x200B;
1. **Zal deze wijziging invloed hebben op de implementatie van JS SDK voor Media Analytics? &#x200B;**

   Nee.  Klanten die de JS SDK voor Media Analytics gebruiken, kunnen de SDK blijven gebruiken of inschakelen via Adobe Launch. &#x200B;
1. **Wat is de mate van inspanning om naar de uitbreidingen van de Analyse van Media te migreren? &#x200B;**

   LOE is afhankelijk van de implementatie van elke klant, dus het zal variëren.  Nadat u de migratiedocumentatie hieronder hebt bekeken, neemt u contact op met de consultant en/of de klantenservice voor extra ondersteuning.

[Extensies voor media-analyse: Android-migratie](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)

[Extensies voor media-analyse: iOS-migratie](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)

   [Extensies voor media-analyse: nieuwe implementaties](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)

1. **Moet ik Starten als systeem voor tagbeheer hebben? Wat gebeurt er als ik Launch niet wil gebruiken?**

   Voor het gebruik van de mobiele app wordt Launch niet gebruikt als een systeem voor tagbeheer zoals voor het web. Het gebruiken van de UI van de Lancering wordt vereist voor het vormen van de uitbreidingen van SDK. Dit is vergelijkbaar met de manier waarop u de gebruikersinterface van Adobe Mobile Services gebruikt om de mobiele v4 SDK te configureren. Voor installatie, is het voordeel van het gebruiken van Lancering dat het u aangepaste installatieinstructies geeft die op de uitbreiding worden gebaseerd u kiest.

1. **Heeft dit einde van de ondersteuning invloed op de SDK voor tvOS?**

   Ja, voor tvOS (versie 10+) is de aanbevolen implementatie het migreren naar de Media Analytics Extensions. Zie voor meer informatie [Migreren van de standalone Media SDK naar Adobe Launch - iOS](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md).

1. **Heeft dit einde van de ondersteuning invloed op de SDK voor Fire TV en AndroidTV? &#x200B;**

   Ja, voor Fire TV en AndroidTV is de aanbevolen implementatie het migreren naar de Media Analytics Extensions. Zie voor meer informatie [Migreren van de standalone Media SDK naar Adobe Launch - Android](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md).
