---
title: Informatie over hartslagen
description: Leer hoe hartslagen worden gebruikt om videometrics te verzamelen.
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: 180dd9b1-877a-4ec1-8e81-c293800069c0
source-git-commit: 0079116bcf39bb6d20b4fd5f14bd3c19137c46e3
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 26%

---

# Informatie over hartslagmeting

De Adobe Streaming Media Collection Add-on gebruikt ‘hartslagen’ om videometrics te verzamelen. Tijdens het afspelen van video worden heartbeats naar de heartbeat-trackingserver verzonden om de afspeeltijd te meten. De heartbeatsignalen worden om de tien seconden verzonden. Heartbeats resulteren in gedetailleerde videobetrokkenheidsstatistieken en nauwkeurigere video-uitvalrapporten. Streaming Media meet hartslagen met behulp van Adobe Launch met de Media Analytics-extensie, de Media SDK en de Media Collection API. De componenten `AppMeasurement` en `VisitorID` worden gebruikt om videodata te ontvangen.

Het gebruik van hartslagen in de Streaming Media Collection Add-on verstrekt de volgende voordelen:

| Functie | Beschrijving |
|---|---|
| Mediagebeurtenissen | Gedetailleerde en aangepaste gebeurtenissen worden elke 10 seconden verzonden voor de hoofdinhoud en elke seconde voor advertenties |
| Statistieken en dimensies | Duidelijk gestandaardiseerde metrics, dimensies en benchmarks voor verschillende leveranciers. Met een gestandaardiseerde oplossing voor alle platforms, kun je consistente, gestandaardiseerde variabelen gebruiken voor al je media en platforms, zodat je een efficiëntere vergelijking tussen campagnes, apparaten en leveranciers kunt maken. |
| Integraties | Experience Cloud-id is gekoppeld aan Adobe Experience Cloud voor een eenvoudigere kruisanalyse. Dankzij de automatische Adobe Experience Cloud-integratie kun je je mediapubliek segmenteren, targeten en mediaaanbevelingen doen op basis van gebruikersvoorkeuren. |
| Prijzen | Transparant bijhouden via mediastream (enkel) |
| Implementatie en ondersteuning | Gestroomlijnde configuratie met doorlopende updates en verbeteringen. Met een gestroomlijnd implementatieproces kun je snel variabelen toewijzen via de speler-API en implementaties valideren met de Adobe Foutopsporing-tool om ervoor te zorgen dat alle benodigde variabelen correct worden bijgehouden. |
| Delen via partners | Federated Media en Certified Metrics. Met gedeelde data via Federated Media, kun je profiteren van onze branchespecifieke mogelijkheden voor media-delen, om data holistisch te evalueren in al je media-distributiepartners, -operators, -programmeurs en -distributeurs. |
| Geavanceerde tracking | Gedownloade inhoud bijhouden, foutherstel bijhouden en gelijktijdige viewers. U kunt streaming media-inhoud bijhouden die op een apparaat wordt gedownload en afgespeeld, ongeacht de connectiviteit. |
