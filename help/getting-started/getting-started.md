---
title: Aan de slag
description: Ga aan de slag met Adobe Analytics for Streaming Media.
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 1%

---


# Aan de slag {#getting-started}

Adobe Analytics for Streaming Media biedt twee belangrijke implementatiemethoden: de Media SDK&#39;s en de Media Collection API&#39;s.

![methoden](assets/getting-started2.png)

De ingebouwde logica van het **SDK&#39;s voor media**, kunt u nauwkeurig meerdere mediaplatforms meten, zoals websites, mobiele telefoons, aangesloten tv&#39;s, tablets, OTT-apparaten, set-top boxes en gameconsoles. U kunt zelfs gedownloade inhoud meten. De inzichten die u krijgt gaan diep in de kijkbetrokkenheid van gebruikers, zodat u kunt begrijpen hoe lang, wanneer en waar de kijkers zich engageren. De Media SDK&#39;s gebruiken de **Media Collection-API&#39;s** voor reeksspatiëring. De API&#39;s voor de verzameling van media kunnen worden aangepast, als uw toepassing aangepaste volgmogelijkheden nodig heeft. Voor apparaten die niet worden ondersteund door de Media SDK&#39;s kunt u de Media Collection API&#39;s gebruiken.

De Adobe Analytics Streaming Media-oplossing is beschikbaar voor de volgende mediaplatforms:

* Web
* Mobile
* Boven aan boven
* Een aangesloten apparaat dat kan worden gebruikt voor streaming media of voor integratie van server naar server

Zie voor meer informatie [Ondersteunde apparaten en Platforms](#_Supported_devices_and).

>[!IMPORTANT]
>
>Als u Adobe Analytics Streaming Media wilt implementeren, neemt u contact op met uw Adobe Sales-vertegenwoordiger of accountmanager om ervoor te zorgen dat Streaming Media deel uitmaakt van uw productportfolio.

## Media SDK&#39;s voor streamingmedia {#media-sdks}

SDK&#39;s voor media voor streaming media zijn beschikbaar voor JavaScript-, Android-, iOS-, tvOS-, Chromecast- en Roku-platforms.

Voor informatie over het downloaden en installeren van Media SDKs, zie [SDK&#39;s van media, extensies met tags en OTT SDK&#39;s ophalen](/help/getting-started/download-sdks.md).


## Media Collection-API&#39;s {#media-collection-apis}

De **Media Collection-API&#39;s** kunt u de implementatie van de mediacontrole aanpassen. Gebruik de Inzameling APIs van Media om Adobe direct te roepen die u bijna om het even welke actie kunt uitvoeren gebruikend SDKs en meer. Pas uw gegevensverzameling aan om rapporten te maken die belangrijke vragen over uw streaming mediagegevens verkennen, begrijpen of beantwoorden.

Voor informatie over het gebruiken van de Inzameling APIs van Media, zie [Steaming Media API-documentatie](/help/implementation/media-collection-api/mc-api-overview.md).

## Adobe-extensies {#adobe-extensions}

>[!NOTE]
>
>INTRO NODIG VOOR DE EXTENSIES

* De [**Adobe Media Analytics voor audio- en video-extensie**](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=en) (Media Analytics-extensie) is vereist voor iOS- en tvOS-implementaties. Het verstrekt de functionaliteit voor het toevoegen van de tracker instantie aan een markeringsplaats of een project. De extensie MA vereist ook de extensie Analytics en de extensie Experience Cloud ID.

* [Analyse Extension v1.6 of hoger](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=en)—Met deze extensie kunt u de Javascript-bibliotheek van de Adobe Experience Platform Web SDK laden om gegevens naar Adobe-oplossingen te verzenden.

* [Experience Cloud ID-extensie](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=en)—Deze extensie implementeert de Experience Cloud ID Service, die bezoekers identificeert voor alle Experience Cloud-oplossingen. De Experience Cloud ID Service is een personalisatie-uitbreiding in Adobe Experience Platform.
