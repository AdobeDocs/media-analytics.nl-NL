---
title: Over Player State Tracking
description: In dit onderwerp wordt de functie voor het bijhouden van de spelerstatus beschreven, inclusief vereisten en richtlijnen voor het implementeren en rapporteren van spelerstatussen.
translation-type: tm+mt
source-git-commit: d317188ef664c836c7125e8bbe195baa924c0d80
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 1%

---


# Over Player State Tracking

Om uw productervaring en drijfvewaarde voor uw zaken te optimaliseren, is het belangrijk om klantengedrag te begrijpen wanneer het bekijken van video&#39;s. Dit geldt ook voor de tijd die in verschillende spelerstatussen wordt doorgebracht.  Het is ook belangrijk om de flexibiliteit te hebben om nieuwe spelerstaten en gebeurtenissen tot stand te brengen en te meten zoals nodig.

Met behulp van een standaardset oplossingsvariabelen voor volledig scherm, gesloten ondertiteling, dempen, beeld in beeld en scherpgesteld kunt u de interactie van de speler tijdens het afspelen vastleggen.  De Staat van de speler het Volgen verstrekt ook de flexibiliteit om douanespeler staten tot stand te brengen. U kunt variabelen van het Volgen van de Staat van de Speler voor het melden in de Werkruimte van de Analyse gebruiken.

Als u wijzigingen in de spelerstatus wilt vastleggen, werkt u de metagegevens van de videometing bij in het bijhouden van de spelerstatus. Bijvoorbeeld, om de &quot;ware&quot;videoovereenkomst te bepalen, meet de Staat van de Speler die tijd doorbrengt met het geluid aan tegenover de passieve of niet-betrokken videomeningen wanneer het geluid of de tijd in Normal tegenover de Volledige wijze van het Scherm wordt doorgebracht.

De Staat van de speler het Volgen levert de volgende voordelen op:

* Biedt standaardvariabelen waarmee algemene toestanden zoals volledig scherm of ondertiteling worden gemeten
* Verstrekt klantgerichte variabelen om douanestatus tijdens een playbackzitting te meten
* Hiermee wordt de tijd gemeten die in een aangepaste spelerstatus is doorgebracht
* Meerdere staten die gelijktijdig kunnen worden gemeten

![Reeksspatiëring](assets/player_state_tracking.png)

## Vereisten

Voor het bijhouden van Player-statussen is een van de volgende vereist voor gegevensverzameling:
* Media JS SDK 3.0+
* Media Analytics Extension (voor gebruik met de Adobe Experience Platform (AEP) SDK)
   * Web: Adobe Media Analytics (3.x SDK) voor Audio en Video v1.0+
   * Mobiel: Adobe Media Analytics voor Audio en Video v2.0+
* Media Collection-API

## Richtsnoeren

Houd rekening met de volgende richtlijnen voordat u Player-statussen implementeert.

* De spelerstatus wordt berekend over alle afspeelstatussen (geen splitsing)
* U kunt meerdere spelerstatussen tegelijk meten
* Het maximumaantal spelerstatussen dat tijdens het afspelen kan worden bijgehouden, is 10 
* De de staatsmetriek van de speler wordt verzonden naar Analyses voor het melden van de Dichte vraag van Media SLECHTS
* De spelerstatussen worden vastgelegd voor elke afzonderlijke afspeelsessie. De spelerstatus wordt niet berekend over afspeelsessies 
