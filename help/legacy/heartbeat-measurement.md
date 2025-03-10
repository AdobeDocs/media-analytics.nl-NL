---
title: Hartmaatmeting
description: Leer hoe hartslagen worden gebruikt om videometriek te verzamelen.
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: 180dd9b1-877a-4ec1-8e81-c293800069c0
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 27%

---

# Informatie over hartslagmeting

In de Adobe Streaming Media Collection worden &#39;hartslagen&#39; gebruikt voor het verzamelen van videomeetgegevens. Tijdens het afspelen van video worden heartbeats naar de heartbeat-trackingserver verzonden om de afspeeltijd te meten. De heartbeatsignalen worden om de tien seconden verzonden. Heartbeats resulteren in gedetailleerde videobetrokkenheidsstatistieken en nauwkeurigere video-uitvalrapporten. Streaming media meet hartslagen met de extensie Media Analytics, Media SDK en Media Collection API van Adobe Launch. De componenten `AppMeasurement` en `VisitorID` worden gebruikt om videodata te ontvangen.

Het gebruik van hartslagen in de Streaming Media Collection biedt de volgende voordelen:

| Functie | Beschrijving |
|---|---|
| Mediagebeurtenissen | Gedetailleerde en aangepaste gebeurtenissen worden elke 10 seconden verzonden voor de hoofdinhoud en elke seconde voor advertenties |
| Statistieken en dimensies | Duidelijk gestandaardiseerde metriek, dimensies, en benchmarks over verkopers. Met een gestandaardiseerde oplossing voor alle platforms kunt u consistente, gestandaardiseerde variabelen gebruiken voor al uw media en platforms, zodat u een efficiëntere vergelijking tussen campagne, apparaat en leverancier kunt maken. |
| Integraties | Experience Cloud-id is gekoppeld aan Adobe Experience Cloud voor een gemakkelijkere kruisanalyse. Dankzij de automatische Adobe Experience Cloud-integratie kunt u uw mediapubliek segmenteren, doelframes opgeven en mediumaanbevelingen doen op basis van de gebruikersvoorkeuren. |
| Prijzen | Transparant bijhouden via mediastream (enkel) |
| Implementatie en ondersteuning | Gestroomlijnde configuratie met doorlopende updates en verbeteringen. Met een gestroomlijnd implementatieproces kunt u snel variabelen toewijzen via de speler-API en implementaties valideren met het gereedschap Adobe debuggen om ervoor te zorgen dat alle benodigde variabelen correct worden bijgehouden. |
| Delen via partners | Federated Media en Certified Metrics. Met gedeelde gegevens door Federated Media, kunt u op onze industrie-eerste media het delen mogelijkheden, om gegevens holistisch over al uw media distributie partners-exploitanten, programmeurs, en verdelers te evalueren. |
| Geavanceerde tracking | Gedownloade Inhoud bijhouden, Foutherstel bijhouden en gelijktijdige viewers. U kunt streaming media-inhoud bijhouden die op een apparaat wordt gedownload en afgespeeld, ongeacht de connectiviteit ervan. |
