---
title: Implementeer de streamingmedia-verzameling
description: Leer over de implementatiepaden voor de Streaming Media Collection.
uuid: null
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: ed9297b1-6487-4099-bc62-0c3a40572255
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---

# Implementeer de streamingmedia-verzameling

Er zijn verschillende manieren om de Adobe Streaming Media Collection te implementeren. Voor een gedetailleerde vergelijking van gesteunde apparaten en platforms voor de implementatiemethodes die op deze pagina worden beschreven, zie [ Gesteunde apparaten en platforms ](/help/getting-started/supported-devices.md).

## Edge-implementatiemethoden

We raden u aan Edge te gebruiken bij de implementatie van de Streaming Media Collection voor alle nieuwe Adobe Analytics- of Customer Journey Analytics-klanten.

* **Media voor Edge Network SDK/Uitbreiding:** verzamelt gegevens van het Web, de apparaten van iOS en van Android, of de apparaten van Roku en verzendt het naar Edge Network. De gegevens kunnen vervolgens naar Customer Journey Analytics of Adobe Analytics worden verzonden.

  Voor meer informatie over de Media voor Edge Network SDK/Uitbreiding, zie [ de Streaming Inzameling van Media uitvoeren gebruikend Edge Network ](/help/implementation/edge/implementation-edge.md).

* **Media Edge API:** kan worden aangepast om gegevens van om het even welk apparaat of formaat (met inbegrip van, mobiel, Web, en over-de-hoogste apparaten) te verzamelen en gegevens naar Edge Network te verzenden. De gegevens kunnen vervolgens naar Customer Journey Analytics of Adobe Analytics worden verzonden.

  Voor meer informatie over de Media Edge API, zie [ het overzicht van Edge API van Media ](https://developer.adobe.com/cja-apis/docs/endpoints/media-edge/).

![ het werkschema van CJA ](assets/streaming-media-edge.png)

## Implementatiemethoden die alleen voor Adobe Analytics gelden

De hierboven beschreven Edge-implementatiemethoden worden aanbevolen voor zowel Customer Journey Analytics als Adobe Analytics, vooral voor nieuwe implementaties.

Naast de implementatiemethoden van Edge zijn andere implementatiemethoden beschikbaar. Deze implementatiemethoden zijn ontworpen voor gebruik met Adobe Analytics. Nochtans, kunnen de bestaande klanten met om het even welke volgende implementatiemethodes nog gegevens in Customer Journey Analytics ter beschikking stellen door een [ bronVerbinding van de Analyse ](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/adobe-applications/analytics.html) te creëren.

* **Uitbreiding van Media met markeringen:** De Analytics van de Media van Adobe voor Audio en Video uitbreiding verstrekt de functionaliteit voor het toevoegen van de instantie van de Tracker van Media aan een markering-toegelaten plaats of project. Gegevens worden naar Adobe Analytics verzonden.

  Voor informatie bij het installeren van, het vormen van, en het uitvoeren van de Uitbreiding van Media met markeringen, zie [ Analytics van de Media van Adobe (3.x SDK) voor Audio en Video uitbreidingsoverzicht ](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/media-analytics-3x/overview.html).

* **Media SDK:** Media SDK staat u toe om veelvoudige media platforms, met inbegrip van websites, mobiele telefoons, aangesloten TVs, tablets, ETT apparaten, reeks-hoogste dozen, en gokkenconsoles te meten. (Voor meer informatie, zie [ Ondersteunde apparaten en platforms ](/help/getting-started/supported-devices.md).)

  De Media SDK&#39;s gebruiken de Media Collection API&#39;s voor het bijhouden van gegevens. Gegevens worden naar Adobe Analytics verzonden.

  Voor informatie over het downloaden van en het installeren van Media SDKs en uitbreidingen, zie [ Media SDKs, Uitbreidingen gebruikend Markeringen, en OTT SDKs ](/help/getting-started/download-sdks.md) krijgen.

* **de Inzameling APIs van Media:** Omdat de Inzameling APIs van Media klantgericht zijn, kunnen zij voor toepassingen worden gebruikt die douane volgende mogelijkheden en voor apparaten vereisen die niet door Media SDKs worden gesteund. De API&#39;s van de Media Collection houden audio- en videogebeurtenissen bij met behulp van RESTful HTTP-aanroepen. Gegevens worden naar Adobe Analytics verzonden.

  Voor informatie over het gebruiken van de Inzameling APIs van Media, zie [ Inzameling APIs van Media ](media-collection-api/mc-api-overview.md).


![ het werkschema van Analytics ](assets/analytics-implementation.png)

<!--
(Not sure if we need the following paragraph and graphic. Paragraph is somewhat redundant with the intro paragraph of this article)
Choose the implementation method depending on the supported platforms. Some players are not supported by the Media SDKs or the Adobe Experience Platform Media Extensions. The Media Collection APIs provide a way to support those players. For information on supported devices, see [Supported devices and platforms](/help/getting-started/supported-devices.md).

![Media Flow](media-sdk/assets/choose-media-flow2.png)
-->
