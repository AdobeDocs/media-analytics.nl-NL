---
title: Attributie van mediastream
description: null
translation-type: tm+mt
source-git-commit: cab9724476f7864ac23c4293e402e0443771cb1e
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 2%

---


# Attributie van mediastream

Met deze functie kunt u toepassingshandelingen koppelen aan gegevens voor het bijhouden van media zonder dat u aanvullende verwerkingsregels en aangepaste variabelen nodig hebt.

## Media-afmetingen buiten mediatracering

Met de Attributie van de Stroom van Media, kunnen de klanten om het even welke media dimensie aan alle andere analytische vraag, zoals paginameningen en douaneverbindingen nu toevoegen. Tijdens implementatie, moet u de gegevensparameters van de media context aan de spoorvraag van Analytics toevoegen. De volledige lijst met contextegegevensparameters die voor media worden gebruikt, is hier beschikbaar: [Parameters voor audio en video.](/help/metrics-and-metadata/audio-video-parameters.md)

U zult ook media volgende configuratie van de Admin console voor elk rapport moeten re-toelaten dat u deze eigenschap voor wilt toelaten.

>[!NOTE]
>
>De mediummetriek is _niet_ beschikbaar voor gebruik buiten mediatracering, omdat de meeste hiervan door Media Analytics worden berekend op basis van hartslaggebeurtenissen. Ook, is het belangrijk dat de media metriek niet door verschillende implementaties worden opgeblazen.

## Procedure

In het onderstaande JavaScript-voorbeeld wordt een aanroep voor het bijhouden van aangepaste koppelingen gegenereerd waarvoor de naam is ingesteld op &quot;Hero Banner&quot;.

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

In Analytics-rapportages kunt u de `Show` Var gebruiken om de gegevens op te splitsen, en u zult de instanties van de spoorverbinding kunnen tellen. De rapportage zou er ongeveer als volgt uitzien:

![](/assets/myShow-rpt-1.png)

## Gevallen gebruiken

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)

