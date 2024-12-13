---
title: Wat is kenmerk van mediastream?
description: Leer hoe u handelingen van toepassingen koppelt aan gegevens voor mediatracering zonder dat u extra verwerkingsregels en aangepaste variabelen nodig hebt.
exl-id: 75cc9088-776d-4b10-b358-9fff956a7eb7
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 1%

---

# Attributie van mediastroom {#media-stream-attribution}

Met de Attributie van de Stroom van Media, kunt u toepassingsacties met media volgende gegevens verbinden zonder de behoefte aan extra verwerkingsregels en douanevariabelen.

## Media-Dimensionen buiten mediatracering

U kunt mediumafmetingen toevoegen aan analytische aanroepen, zoals paginaweergaven en aangepaste koppelingen. Tijdens implementatie, moet u de gegevensparameters van de media context aan de het spoorvraag van Analytics toevoegen. Om de volledige lijst van beschikbare parameters van contextgegevens te bekijken die voor media worden gebruikt, zie [ Audio en videoparameters.](/help/implementation/variables/audio-video-parameters.md)

Om deze eigenschap voor een specifiek rapport toe te laten, re-enable de media volgende configuratie van de Admin console.

>[!NOTE]
>
>De media metriek zijn _niet_ beschikbaar voor gebruik buiten media het volgen omdat de meeste van deze gegevens door de Streaming Inzameling van Media die op hartslaggebeurtenissen worden gebaseerd worden gegevens verwerkt. Ook, is het belangrijk dat de media metriek niet door verschillende implementaties worden opgeblazen.

## Kenmerken van mediastroom gebruiken

In het onderstaande JavaScript-voorbeeld wordt een aanroep voor het bijhouden van een aangepaste koppeling gegenereerd waarvoor de naam is ingesteld op &quot;Hero Banner&quot;.

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

Bij Analytics-rapportage kunt u de `Show` -eVar gebruiken om de gegevens op te splitsen en u kunt de instanties van trackkoppelingen tellen. De rapportage zou er ongeveer als volgt uitzien:

![](/assets/myShow-rpt-1.png)

## Gebruiksscenario’s

In het volgende voorbeeld worden praktijkgevallen getoond voor het volgende:

* Plaatsing categorie
* Hero Placement
* Betrokkenheid
* Abonnementen

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)
