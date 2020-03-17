---
title: De volgorde van gebeurtenissen bepalen
description: null
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# De volgorde van gebeurtenissen bepalen{#controlling-the-order-of-events}

Aangezien de API van de Inzameling van Media RESTful is, en video het volgen een hoogst tijdsafhankelijke verrichting is, zou een implementor zich over de het volgen vraag van de Inzameling van Media kunnen ongerust zijn die bij het achtereind van orde aankomt. Het achterste einde *probeert* gebeurtenissen op basis van de opgegeven tijdstempel in het `playerTime` object in een wachtrij te plaatsen en opnieuw te ordenen. Deze mogelijkheid is echter beperkt. Momenteel kan de herschikking mislukken als de vertragingen tussen aanroepen buiten de orde meer dan één seconde zijn. Deze &quot;aanvaardbare vertragingstijd&quot; kan in toekomstige updates worden geoptimaliseerd en/of configureerbaar zijn.
