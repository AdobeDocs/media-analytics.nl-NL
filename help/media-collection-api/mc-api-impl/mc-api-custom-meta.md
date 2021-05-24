---
title: Ondersteuning voor aangepaste metagegevens
description: Ondersteuning voor aangepaste metagegevens
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
source-git-commit: 962bb8b6859ca8964efcb2f3ba0dc566a5e24c3e
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 1%

---

# Ondersteuning voor aangepaste metagegevens{#custom-metadata-support}

U kunt aangepaste key:value-paren opgeven voor de gebeurtenissen `sessionStart`, `chapterStart` en `adStart`. Deze informatie moet worden verstrekt in de sleutel JSON, `customMetadata`, die naast `params` sleutel wordt geplaatst.

De JSON-toets `customMetadata` moet een object key:value-paren bevatten. De sleutel mag alleen alfanumerieke tekens, onderstreping en punt/punt bevatten.

[API-gebeurtenissen voor MA-verzameling](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

## Voorbeeld

U kunt op dit moment een gebeurtenis `sessionStart` verzenden met de volgende sleutel:waardepaar:

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
