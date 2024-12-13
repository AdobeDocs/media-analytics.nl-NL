---
title: Meer informatie over de veelgestelde vragen over Media Analytics SDK End of Support
description: Dit onderwerp omvat FAQs over het eind van steun voor Media Analytics SDKs.
exl-id: 9601ec17-8421-49d0-9d81-1cfa5e8f37cf
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 0%

---

# Veelgestelde vragen over einde van ondersteuning voor Media Analytics Mobile SDK

Met het einde van de ondersteuning voor versie 4 Mobile SDK&#39;s op 31 augustus 2021 beëindigde Adobe ook de ondersteuning voor de Media Analytics Mobile SDK&#39;s voor iOS en Android. (Hieronder vallen niet de Media Analytics SDK for web (JS) en OTT-platforms zoals Chromecast en Roku, die nog steeds worden ondersteund.)

Dit betekent dat Adobe niet langer oplossingen, updates met betrekking tot het besturingssysteem of ondersteuning voor Media Analytics Mobile SDK biedt. Wanneer het migreren aan het nieuwe Experience Platform SDKs, me ervan bewust ben dat de [ uitbreidingen van de Analyse van Media ](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) moeten worden uitgevoerd om de Adobe toe te laten die de Inzameling van Media stromen.


## Top 5 van dingen die u moet weten

1. Mobiele v4-SDK&#39;s worden niet meer ondersteund vanaf 31 augustus 2021. Migreer naar de Adobe Experience Platform (AEP) Mobile SDK&#39;s voor iOS en Android.

1. Voor Analytics para medios de streaming-implementatie is de AEP Mobile SDK vereist en gebruik van de extensies Analytics en Media Analytics. Vanaf 1 september 2021 moet u de nieuwe AEP Mobile SDK&#39;s en uitbreidingen gebruiken.  De uitbreidingen van de Analytics van media worden gevormd gebruikend de Markeringen van de Adobe (gegevensinzameling). Voor extra informatie, zie [ Migrerend van Stand-alone Media SDK aan de Lancering van de Adobe ](/help/legacy/sdk-to-launch/sdk-to-launch-migration.md)

1. De ontwikkeling van functies voor de Media Analytics SDK&#39;s voor iOS en Android is beëindigd. Nieuwe functies die zijn geïntroduceerd vanaf Fall 2019 worden ingeschakeld met de extensies Media Analytics en Media Collection API.

1. De SDK&#39;s van Roku en Chromecast blijven beschikbaar voor Analytics para medios de streaming-klanten. De SDK&#39;s van Roku en Chromecast zullen verder worden verbeterd en ondersteund als zelfstandige SDK&#39;s. Als u JS SDK for Media Analytics gebruikt, kunt u de stand-alone SDK blijven gebruiken of de uitbreiding van de Analyse van Media toelaten gebruikend de Inzameling van de Gegevens van de Adobe (vroeger de Lancering van de Adobe).

Neem contact op met het accountteam van uw Adobe als u vragen hebt.

## Veelgestelde vragen

1. **zal steun voor Roku en Chromecast SDKs worden beïnvloed? &#x200B;**

   Nee.  Roku- en Chromecast SDK&#39;s blijven voorlopig ondersteund als zelfstandige SDK&#39;s. &#x200B;
&#x200B;
1. **zal de implementaties van JS SDK van de Analytics van Media door deze verandering worden beïnvloed? &#x200B;**

   Nee.  Klanten die de JS SDK for Media Analytics gebruiken, kunnen de SDK blijven gebruiken of inschakelen via het starten van de Adobe.
&#x200B;
1. **wat is het niveau van inspanning om aan de uitbreidingen van de Analytics van Media te migreren? &#x200B;**

   LOE is afhankelijk van de implementatie van elke klant, dus het zal variëren.  Nadat u de migratiedocumentatie hieronder hebt bekeken, neemt u contact op met de consultant en/of de klantenservice voor extra ondersteuning.

[Media Analytics Extensions: Android-migratie](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)

[Media Analytics Extensions: iOS-migratie](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)

   [ Uitbreidingen van de Analytics van Media: nieuwe implementaties ](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)

1. **moet ik Lanceren als systeem van het markeringsbeheer hebben? Wat als ik geen Lancering wil gebruiken?**

   Voor het gebruik van de mobiele app wordt Launch niet gebruikt als een systeem voor tagbeheer zoals voor het web. Voor het configureren van de SDK-extensies is het gebruik van de opstartinterface vereist. Dit is vergelijkbaar met de manier waarop u de gebruikersinterface van Adobe Mobile Services gebruikt om de mobiele v4 SDK te configureren. Voor installatie, is het voordeel van het gebruiken van Lancering dat het u aangepaste installatieinstructies geeft die op de uitbreiding worden gebaseerd u kiest.

1. **beïnvloedt dit eind van steun SDK voor tvOS?**

   Ja, voor tvOS (versie 10+) is de aanbevolen implementatie het migreren naar de Media Analytics Extensions. Voor extra informatie, zie [ Migrerend van de standalone SDK van Media aan de Lancering van de Adobe - iOS ](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md).

1. **beïnvloedt dit eind van steun SDK voor VuurTV en AndroidTV? &#x200B;**

   Ja, voor Fire TV en AndroidTV is de aanbevolen implementatie het migreren naar de Media Analytics Extensions. Voor extra informatie, zie [ Migrerend van de standalone SDK van Media aan de Lancering van de Adobe - Android ](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md).
