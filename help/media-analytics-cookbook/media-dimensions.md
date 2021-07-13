---
title: Wat is kenmerk van mediastream?
description: Leer hoe u handelingen van toepassingen koppelt aan gegevens voor mediatracering zonder dat u extra verwerkingsregels en aangepaste variabelen nodig hebt.
exl-id: 75cc9088-776d-4b10-b358-9fff956a7eb7
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 1%

---

# Attributie van mediastream

Met deze functie kunt u toepassingshandelingen koppelen aan gegevens voor het bijhouden van media zonder dat u aanvullende verwerkingsregels en aangepaste variabelen nodig hebt.

## Media-Dimension buiten mediatracering

Met de Attributen van de Stream van Media, kunnen de klanten om het even welke media afmetingen toevoegen
naar alle andere analytische aanroepen, zoals paginaweergaven en aangepaste koppelingen. Tijdens de uitvoering
u moet de gegevensparameters van de media context aan de het spoorvraag van de Analyse toevoegen. De volledige lijst
van de parameters voor contextgegevens die voor media worden gebruikt , zijn hier beschikbaar : [Parameters voor audio en video.](/help/metrics-and-metadata/audio-video-parameters.md)

U zult ook media volgende configuratie van de Admin console voor elk rapport moeten re-toelaten dat u deze eigenschap voor wilt toelaten.

>[!NOTE]
>
>De media metriek zijn _not_ beschikbaar om buiten media het volgen te worden gebruikt omdat de meeste van deze door de Analytics van Media op hartslaggebeurtenissen worden berekend die. Ook, is het belangrijk dat de media metriek niet door verschillende implementaties worden opgeblazen.

## Procedure

In het onderstaande JavaScript-voorbeeld wordt een aanroep voor het bijhouden van aangepaste koppelingen gegenereerd waarvoor de naam is ingesteld op &quot;Hero Banner&quot;.

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

Bij Analytics-rapportage kunt u de `Show`-eVar gebruiken om de gegevens op te splitsen en u kunt de instanties van trackkoppelingen tellen. De rapportage zou er ongeveer als volgt uitzien:

![](/assets/myShow-rpt-1.png)

## Gevallen gebruiken

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)
