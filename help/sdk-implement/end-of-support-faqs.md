---
title: Veelgestelde vragen over einde ondersteuning van Media Analytics SDK
description: Dit onderwerp omvat FAQs over het eind van steun voor Media Analytics SDKs.
translation-type: tm+mt
source-git-commit: fdec4da99a43d889690638f1ff3579e145548b69
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 1%

---


# Veelgestelde vragen over einde ondersteuning van Media Analytics SDK

Aan het einde van de ondersteuning voor versie 4 Mobile SDK&#39;s op 31 augustus 2021 beëindigt Adobe ook de ondersteuning voor de Media Analytics SDK&#39;s voor iOS en Android. Na 31 augustus 2021 biedt Adobe geen oplossingen, updates voor het besturingssysteem of ondersteuning voor de Media Analytics SDK.  Houd er tijdens het migratieproces naar deze nieuwe SDK&#39;s voor Experience Platforms rekening mee dat de [Media Analytics-extensies](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics) moet worden geïmplementeerd om Adobe Analytics for Streaming Media in te schakelen.

## Top 5 van dingen die u moet weten

1. Mobiele v4-SDK&#39;s worden na 31 augustus 2021 niet meer ondersteund. Migreer naar de Adobe Experience Platform (AEP) SDK&#39;s voor iOS en Android. Zie voor meer informatie [Versie 4 Veelgestelde vragen over de end-of-support van mobiele SDK&#39;s](https://aep-sdks.gitbook.io/docs/version-4-sdk-end-of-support-faq).

1. Voor analyse voor de implementatie van STROOMmedia is de AEP SDK en het gebruik van de extensies Analytics en Media Analytics vereist. Vanaf 1 september 2021 moet u de nieuwe SDK&#39;s en uitbreidingen van AEP gebruiken.  De extensies voor Media Analytics worden geconfigureerd met Adobe Launch.  Zie voor meer informatie [Migreren van zelfstandige media SDK naar Adobe Launch](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration.html)

1. De ontwikkeling van functies voor de Media Analytics-SDK&#39;s voor iOS en Android is beëindigd.  Nieuwe functies die zijn geïntroduceerd vanaf Fall 2019 worden ingeschakeld met de extensies Media Analytics en Media Collection API.

1. De SDK&#39;s van Roku en Chromecast blijven beschikbaar voor Analytics voor klanten van Steaming Media. De SDK&#39;s van Roku en Chromecast zullen verder worden verbeterd en ondersteund als zelfstandige SDK&#39;s.  Als u de SDK van JS voor Media Analytics gebruikt, kunt u de stand-alone SDK blijven gebruiken of de uitbreiding van de Analyse van Media toelaten gebruikend de Lancering van Adobe.

1. Vóór 1 september 2021 kan Adobe naar eigen goeddunken nieuwe correcties voor problemen met een hoog technisch effect of blootstelling van ondernemingen ontwikkelen. Op basis van de input van de klant bepaalt Adobe de mate van impact en blootstelling en de daaruit voortvloeiende activiteiten.

Neem contact op met uw Adobe Customer Success Manager als u vragen hebt.

## Veelgestelde vragen

1. **Zal de steun voor Roku en Chromecast SDKs worden beïnvloed? &#x200B;**

   Nee.  Roku en Chromecast SDK&#39;s blijven voorlopig ondersteund als zelfstandige SDK&#39;s. &#x200B; &#x200B;
1. **Zal deze wijziging invloed hebben op de implementatie van JS SDK voor Media Analytics? &#x200B;**

   Nee.  Klanten die de JS SDK voor Media Analytics gebruiken, kunnen de SDK blijven gebruiken of inschakelen via Adobe Launch. &#x200B;
1. **Wat is de mate van inspanning om naar de uitbreidingen van de Analyse van Media te migreren? &#x200B;**

   LOE hangt van de implementatie van elke klant af, zodat zal het variëren.  Nadat u de migratiedocumentatie hieronder hebt bekeken, neemt u contact op met de consultant en/of de klantenservice voor extra ondersteuning.

   [Extensies voor media-analyse: Android-migratie](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html)

   [Extensies voor media-analyse: iOS-migratie](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html)

   [Extensies voor media-analyse: nieuwe implementaties](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

1. **Moet ik Starten als systeem voor tagbeheer hebben? Wat gebeurt er als ik Launch niet wil gebruiken?**

   Voor het gebruik van de mobiele app wordt Launch niet gebruikt als een systeem voor tagbeheer zoals voor het web.  Het gebruiken van de UI van de Lancering wordt vereist voor het vormen van de uitbreidingen van SDK. Dit is vergelijkbaar met de manier waarop u de gebruikersinterface van Adobe Mobile Services gebruikt om de mobiele v4 SDK te configureren. Voor installatie, is het voordeel van het gebruiken van Lancering dat het u aangepaste installatieinstructies geeft die op de uitbreiding worden gebaseerd u kiest.

1. **Heeft dit einde van de ondersteuning invloed op de SDK voor tvOS?**

   Ja, voor tvOS (versie 10+) is de aanbevolen implementatie het migreren naar de Media Analytics Extensions.  Zie voor meer informatie [Migreren van de standalone Media SDK naar Adobe Launch - iOS](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html).

1. **Heeft dit einde van de ondersteuning invloed op de SDK voor FireTV en AndroidTV? &#x200B;**

   Ja, voor FireTV en AndroidTV is de aanbevolen implementatie het migreren naar de Media Analytics Extensions.  Zie voor meer informatie [Migreren van de standalone Media SDK naar Adobe Launch - Android](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html).
