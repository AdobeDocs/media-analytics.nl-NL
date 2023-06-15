---
title: Een mobiele SDK instellen met tags voor streaming media
description: Leer hoe u Adobe Streaming Media voor mobiele apps implementeert.
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: b4944b5f-cbae-4efc-9ef7-962d3f342240
source-git-commit: 1e4babe0df218342fc4836155139d908ba113510
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# Mobiele SDK&#39;s installeren {#install-mobile-sdks}

Als u streaming media voor mobiele apps wilt implementeren op Android of iOS, installeert en configureert u het volgende:

* **Adobe Experience Platform Mobile SDK**

  Gebruik een van de volgende twee opties om gegevens te verzamelen:
   * Tags in Adobe Experience Platform. Tags in Adobe Experience Platform zijn een oplossing voor tagbeheer waarmee u naast andere coderingsvereisten ook analytische code kunt implementeren.
   * Adobe Experience Platform Edge

* **Media SDK voor Android** of **Media SDK voor iOS**

* **Adobe Media Analytics voor audio- en video-extensie**

Zie voor informatie over het downloaden van SDK&#39;s en aanvullende documentatiebronnen de [SDK&#39;s van media, extensies met tags en OTT SDK&#39;s ophalen](/help/getting-started/download-sdks.md)

* **Geldige configuratieparameters verkrijgen**

  Deze parameters kunt u verkrijgen van een Adobe-medewerker nadat u uw analyseaccount hebt ingesteld.

* **De volgende API&#39;s opnemen in uw mediaspeler**

   * *Een API die zich moet abonneren op spelergebeurtenissen* - De SDK van Media vereist dat u een set eenvoudige API&#39;s oproept wanneer gebeurtenissen in de speler plaatsvinden.

   * *Een API die spelerinformatie biedt* - Dit omvat informatie over het momenteel afspelen, zoals de medianaam, de positie van de afspeelkop, advertenties of het hoofdstuk.
