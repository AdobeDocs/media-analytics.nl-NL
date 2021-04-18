---
title: Ondersteuning voor aangepaste metagegevens
description: Ondersteuning voor aangepaste metagegevens
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---

# Ondersteuning voor aangepaste metagegevens{#custom-metadata-support}

U kunt aangepaste key:value-paren opgeven voor de gebeurtenissen `sessionStart`, `chapterStart` en `adStart`. Deze informatie moet worden verstrekt in de sleutel JSON, `customMetadata`, die naast `params` sleutel wordt geplaatst.

De JSON-toets `customMetadata` moet een object key:value-paren bevatten. De sleutel mag alleen alfanumerieke tekens, onderstreping en punt/punt bevatten.

[API-gebeurtenissen voor MA-verzameling](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)
