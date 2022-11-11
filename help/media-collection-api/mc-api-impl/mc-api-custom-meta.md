---
title: Ondersteuning voor aangepaste metadata
description: "Leer hoe te om douanesleutel te verstrekken:waardeparen op sessionStart, chapterStart, en adStart gebeurtenissen."
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: d89b2af2e2ae5a170ce98f62656cdeed6fe31f19
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 3%

---

# Ondersteuning voor aangepaste metagegevens{#custom-metadata-support}

U kunt een aangepaste sleutel opgeven:waardeparen op het tabblad `sessionStart`, `chapterStart`, en `adStart` gebeurtenissen. Deze informatie moet in de sleutel van JSON worden verstrekt, `customMetadata`, geplaatst naast de `params` toets.

De `customMetadata` JSON-sleutel moet een object met sleutel:waardeparen bevatten. De sleutel mag alleen alfanumerieke tekens, onderstreping en punt/punt bevatten.

[API-gebeurtenissen voor MA-verzameling](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

## Voorbeeld

U kunt op dit moment een `sessionStart` gebeurtenis met de volgende toets:waardepaar:

```
params: { "media.channel": "channel-1" },
  customMetadata: { "a.media.channel": "channel-2" }
```

Voor de bovenstaande configuratie worden de volgende gegevens naar Analytics verzonden:

`c.a.media.channel=channel-2`

### Aanbeveling

We raden u aan een aparte naamruimte te gebruiken voor aangepaste metagegevens. Bijvoorbeeld:

```
params: { "media.channel": "channel-1" },
  customMetadata: { "clientnamespace.media.channel": "channel-2" }
```

In het aanbevolen voorbeeld zijn de rapportgegevens voor aangepaste metagegevens die naar analytics worden verzonden als volgt:

`c.a.media.channel=channel-1`
`c.clientnamespace.media.channel=channel-2`
