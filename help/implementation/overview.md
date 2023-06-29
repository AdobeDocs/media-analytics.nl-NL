---
title: Streaming media implementeren voor Adobe Analytics of Customer Journey Analytics
description: Leer meer over de implementatiepaden voor Streaming Media.
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: ed9297b1-6487-4099-bc62-0c3a40572255
source-git-commit: a26e4e283646e5ceb352f357789748f376f5c747
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---

# Streaming media implementeren voor Adobe Analytics of Customer Journey Analytics

Er zijn verschillende manieren om streaming media te implementeren. Voor een gedetailleerde vergelijking van ondersteunde apparaten en platforms voor de implementatiemethoden die op deze pagina worden beschreven, raadpleegt u [Ondersteunde apparaten en platforms](/help/getting-started/supported-devices.md).

## Implementatiemethoden voor Edge

We raden u aan Edge te gebruiken bij de implementatie van Media Analytics voor alle nieuwe Adobe Analytics- of Customer Journey Analytics-klanten.

* **Media voor Edge Network SDK / Extensie:** Verzamelt gegevens van iOS- en Android-apparaten en verzendt deze naar Edge. Gegevens kunnen vervolgens naar Customer Journey Analytics of Adobe Analytics worden verzonden.

  Voor meer informatie over Media voor het Netwerk SDK van Edge/de Uitbreiding, zie [Media Analytics installeren met Experience Platform Edge](/help/implementation/edge/implementation-edge.md).

  >[!NOTE]
  >
  >Deze implementatiemethode steunt momenteel niet het Web SDK of Roku. Beide toepassingen worden echter ondersteund bij de implementatie met de Media Edge-API.

* **Mediarand-API:** Kan worden aangepast om gegevens van om het even welk apparaat of formaat (met inbegrip van, mobiele, Web, en over-de-hoogste apparaten) te verzamelen en gegevens naar Rand te verzenden. Gegevens kunnen vervolgens naar Customer Journey Analytics of Adobe Analytics worden verzonden.

  <!-- For more information about the Media Edge API, see (link to John's docs when they're ready) -->

![CJA-workflow](assets/cja-implementation.png)

## Implementatiemethoden die alleen voor Adobe Analytics gelden

De hierboven beschreven Edge-implementatiemethoden worden aanbevolen voor zowel Customer Journey Analytics als Adobe Analytics, vooral voor nieuwe implementaties.

Naast de implementatiemethoden van Edge zijn er andere implementatiemethoden beschikbaar. Deze implementatiemethoden zijn ontworpen voor gebruik met Adobe Analytics. Bestaande klanten met een van de volgende implementatiemethoden kunnen echter nog steeds gegevens beschikbaar stellen in Customer Journey Analytics door een [Bronverbinding voor analyse](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/adobe-applications/analytics.html).

* **Media Extension met tags:** De Adobe Media Analytics voor Audio en Video uitbreiding verstrekt de functionaliteit voor het toevoegen van de instantie van de Tracker van Media aan een markering-toegelaten plaats of een project. Gegevens worden naar Adobe Analytics verzonden.

  Voor informatie over het installeren, configureren en implementeren van de Media Extension met tags raadpleegt u [Overzicht van Adobe Media Analytics (3.x SDK) voor audio- en video-extensie](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/media-analytics-3x/overview.html).

* **Media SDK:**  Gegevens worden naar Adobe Analytics verzonden.

  Voor informatie over het downloaden en installeren van Media SDKs en uitbreidingen, zie [SDK&#39;s van media, extensies met tags en OTT SDK&#39;s ophalen](/help/getting-started/download-sdks.md).

* **Media Collection-API:** Audio- en videogebeurtenissen bijhouden met RESTful HTTP-aanroepen. Gegevens worden naar Adobe Analytics verzonden.

  Voor informatie over het gebruiken van de Inzameling APIs van Media, zie [Media Collection-API&#39;s](media-collection-api/mc-api-overview.md).


![Workflow Analytics](assets/analytics-implementation.png)

<!--
(Not sure if we need the following paragraph and graphic. Paragraph is somewhat redundant with the intro paragraph of this article)
Choose the implementation method depending on the supported platforms. Some players are not supported by the Media SDKs or the Adobe Experience Platform Media Extensions. The Media Collection APIs provide a way to support those players. For information on supported devices, see [Supported devices and platforms](/help/getting-started/supported-devices.md).

![Media Flow](media-sdk/assets/choose-media-flow2.png)
-->
