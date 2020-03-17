---
title: Ondersteuning voor aangepaste metagegevens
description: null
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Ondersteuning voor aangepaste metagegevens{#custom-metadata-support}

U kunt een aangepaste sleutel opgeven:waardeparen voor de gebeurtenissen `sessionStart`, `chapterStart`en `adStart` gebeurtenissen. Deze informatie moet worden verstrekt in de sleutel van JSON, `customMetadata`, die naast de `params` sleutel wordt geplaatst.

De `customMetadata` JSON-toets moet een object key:value-paren bevatten. De sleutel mag alleen alfanumerieke tekens, onderstreping en punt/punt bevatten.

[API-gebeurtenissen voor MA-verzameling](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

