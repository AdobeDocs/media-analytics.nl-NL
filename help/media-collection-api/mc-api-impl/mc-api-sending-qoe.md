---
title: QoE-data verzenden
description: Meer informatie over het verzenden van gebeurtenissen met een JavaData JSON-toets.
uuid: 52a02d92-195d-4ce8-8ce3-585ed68969f9
exl-id: 41a20410-78e6-481d-bd5c-0febadb290d8
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '57'
ht-degree: 5%

---

# QoE-gegevens verzenden{#sending-qoe-data}

Elke gebeurtenis kan worden versierd met een extra sleutel JSON genoemd `qoeData`, die naast `params` sleutel in het JSON verzoeklichaam wordt geplaatst.

>[!NOTE]
>
>Controleer de [JSON-validatieschema&#39;s](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md) om te controleren of parametertypen verplicht of optioneel zijn.
