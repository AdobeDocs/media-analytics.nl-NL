---
title: Mediaanalyse SDK Einde van supportvragen
description: Dit onderwerp omvat FAQs over het eind van steun voor de Analyse SDKs van Media.
translation-type: tm+mt
source-git-commit: cea8c4b31b21f1b13a55268fbcfb9100a7bdbd7c
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 1%

---


# Mediaanalyse SDK Einde van supportvragen

Met het eind van steun voor Versie 4 Mobiele SDKs op 31 Augustus, zal 2021, Adobe ook steun voor de Analytics SDKs van Media voor iOS en Android beëindigen. Na 31 Augustus, 2021, zal Adobe geen moeilijke situaties, op OS betrekking hebbende updates, of steun voor de Analyse SDK van Media verstrekken.  Tijdens het migratieproces naar dit nieuwe Ervingsplatform SDK&#39;s, houdt u er rekening mee dat de [Media Analytics-extensies](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics) moet worden geïmplementeerd om Adobe Analytics voor Audio en Video toe te laten.

## Top 5 van alles om te weten

1. Mobiele v4 SDK&#39;s worden na 31 augustus 2021 niet meer ondersteund. U zou aan het Platform van de Ervaring van Adobe (AEP) SDKs voor iOS en Android moeten migreren. Voor aanvullende informatie, zie [Versie 4 Mobiele SDKs eind-van-steun FAQ](https://aep-sdks.gitbook.io/docs/version-4-sdk-end-of-support-faq).

1. De analytica voor Audio en Video implementatie vereisen AEP SDK en gebruik van de uitbreidingen van de Analytics en van de Analyse van Media. Beginnend 1 September, 2021, zou u nieuwe AEP SDKs en uitbreidingen moeten gebruiken.  De uitbreidingen van de Analyse van media worden gevormd gebruikend de Lancering van Adobe.  Voor aanvullende informatie, zie [Migreren van stand-alone Media SDK naar Adobe Launch](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration.html)

1. De ontwikkeling van de eigenschap is beëindigd voor de Media Analytics SDKs voor iOS en Android.  De nieuwe eigenschappen die werden geïntroduceerd beginDaling 2019 worden toegelaten gebruikend de uitbreidingen van de Analyse van Media en de Inzameling API van Media.

1. Roku en Chromecast SDKs blijven beschikbaar voor Analytics voor Audio en Video klanten. Roku en Chromecast SDKs zullen blijven worden verbeterd en als stand-alone SDKs worden gesteund.  Als u JS SDK voor de Analyse van Media gebruikt, kunt u stand-alone SDK blijven gebruiken of de uitbreiding van de Analyse van Media toelaten gebruikend de Lancering van Adobe.

1. Voorafgaand aan 1 September, 2021, kan Adobe, op zijn enige discretie, nieuwe moeilijke situaties voor problemen van hoge technische invloed of bedrijfsblootstelling ontwikkelen. Gebaseerd op de klanteninput, zal Adobe de graad van effect en blootstelling en de daaruit voortvloeiende activiteiten bepalen.

Neem contact op met de Adobe Customer Success Manager als u vragen hebt.

## Veelgestelde vragen

1. **Zal de steun voor Roku en Chromecast SDKs worden beïnvloed &#x200B;?**

   Nee.  Roku en Chromecast SDKs zullen voorlopig als stand-alone SDKs worden gesteund. &#x200B; &#x200B;
1. **Zal de implementaties van JS SDK van de Analyse van Media door deze verandering worden beïnvloed? &#x200B;**

   Nee.  De klanten die JS SDK voor de Analyse van Media gebruiken kunnen SDK blijven gebruiken of het via de Lancering van Adobe toelaten. &#x200B;
1. **Wat is het niveau van inspanning om aan de uitbreidingen van de Analyse van Media te migreren? &#x200B;**

   LOE hangt van de implementatie van elke klant af, zodat zal het variëren.  Nadat u de onderstaande migratiedocumentatie hebt doorgenomen, raadpleegt u de klant en/of raadpleegt u de klant voor extra support.

   [Media Analytics Extensions: Androïde migratie](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html)

   [Media Analytics Extensions: iOS-migratie](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html)

   [Media Analytics Extensions: nieuwe implementaties](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

1. **Moet ik Lancering hebben als systeem voor tagbeheer? Wat als ik geen Lancering wil gebruiken?**

   Voor de mobiele app gebruiksdoos, wordt de Lancering niet gebruikt als systeem van het markeringsbeheer aangezien het voor Web is.  Het gebruiken van de Lancering UI wordt vereist voor het vormen van de uitbreidingen van SDK. Dit is gelijkaardig aan hoe u de Mobiele Diensten UI van Adobe gebruikt om mobiele v4 SDK te vormen. Voor installatie, is het voordeel om Lancering te gebruiken dat het u aangepaste installatieinstructies geeft die op de uitbreiding worden gebaseerd u kiest.

1. **Heeft dit einde van de ondersteuning gevolgen voor SDK voor tvOS?**

   Ja, voor tvOS (versie 10+) is de geadviseerde implementatie aan de Uitbreidingen van de Analyse van Media migreren.  Voor aanvullende informatie, zie [Migrerend van de standalone Media SDK aan de Lancering van Adobe - iOS](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html).

1. **Heeft dit einde van de ondersteuning gevolgen voor de SDK voor FireTV en AndroidTV? &#x200B;**

   Ja, voor FireTV en AndroidTV, is de geadviseerde implementatie aan de Uitbreidingen van de Analyse van Media migreren.  Voor aanvullende informatie, zie [Migrerend van de standalone Media SDK aan de Lancering van Adobe - Android](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html).
