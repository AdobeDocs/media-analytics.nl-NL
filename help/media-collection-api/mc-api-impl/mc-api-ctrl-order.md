---
title: De volgorde van gebeurtenissen bepalen
description: De volgorde van gebeurtenissen bepalen
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# De volgorde van gebeurtenissen bepalen{#controlling-the-order-of-events}

Aangezien de API van de Inzameling van Media RESTful is, en video het volgen een hoogst tijdsafhankelijke verrichting is, zou een implementor zich over de het volgen vraag van de Inzameling van Media kunnen ongerust zijn die bij het achtereind van orde aankomt. Met het back-end *wordt* geprobeerd gebeurtenissen in de wachtrij te plaatsen en opnieuw te ordenen op basis van de opgegeven tijdstempel in het object `playerTime`. Deze mogelijkheid is echter beperkt. Momenteel kan de herschikking mislukken als de vertragingen tussen aanroepen buiten de orde meer dan één seconde zijn. Deze &quot;aanvaardbare vertragingstijd&quot; kan in toekomstige updates worden geoptimaliseerd en/of configureerbaar zijn.
