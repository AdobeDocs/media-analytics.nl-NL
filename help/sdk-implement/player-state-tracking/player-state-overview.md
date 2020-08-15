---
title: Over Player State Tracking
description: Dit onderwerp beschrijft de het volgen eigenschap van de spelerstaat met inbegrip van vereisten en richtlijnen voor het uitvoeren van en het melden van spelerstaten.
translation-type: tm+mt
source-git-commit: 4c11efd0b8bb457246c746621e7fbb9fbda621b2
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# Over Player State Tracking

Om uw productervaring te optimaliseren en waarde voor uw bedrijf te verhogen, is het belangrijk om het gedrag van de klant te begrijpen bij het bekijken van video&#39;s. Dit omvat de tijd die in verschillende spelerstaten wordt doorgebracht.  Het is ook belangrijk om de flexibiliteit te hebben om nieuwe spelerstaten en gebeurtenissen tot stand te brengen en te meten zoals nodig.

Het Volgen van de Staat van de speler verstrekt het vermogen om kijkersinteractie tijdens playback te vangen gebruikend een standaardreeks oplossingsvariabelen voor het volledige scherm, gesloten ondertiteling, stomme, beeld in beeld, en in nadruk.  Het Volgen van de Staat van de speler verstrekt ook de flexibiliteit om de staten van de douanespeler tot stand te brengen. U kunt het Volgen van de Staat van de Speler variabelen voor rapportering in de Werkruimte van de Analyse gebruiken.

Om veranderingen in de spelerstaat te vangen, werkt het Volgen van de Staat van de Speler de videometa-gegevens van de meting bij. Bijvoorbeeld, om de &quot;ware&quot;videoovereenkomst te bepalen, meet de Staat van de Speler die tijd doorbrengt met het geluid aan tegenover de passieve of niet betrokken videomeningen wanneer het geluid of de tijd die in Normale tegenover Volledige wijze van het Scherm wordt doorgebracht weg is.

Het Volgen van de Staat van de speler levert de volgende voordelen:

* Verstrekt standaardvariabelen die gemeenschappelijke staten zoals het volledige scherm of het gesloten captioning meten
* Verstrekt klantgerichte variabelen om douanestatus tijdens een playbackzitting te meten
* De tijd die binnen een staat van de douanespeler wordt doorgebracht
* Meet veelvoudige staten die gelijktijdig kunnen zijn

![Status van speler volgen](assets/player_state_tracking.png)

## Vereisten

De Staat die van de speler het Volgen vereist één van het volgende voor gegevensinzameling volgt:
* Media JS SDK 3.0+
* Chromecast 3.0 SDK voor de Oplossingen van de Wolk van de Marketing van Adobe
* Media Analytics Extension (voor gebruik met het Adobe Experience Platform (AEP) SDK)
   * Web: Adobe Media Analytics (3.x SDK) voor audio en video v1.0+
   * Mobiel: Adobe Media Analytics voor audio en video v2.0+
* Media Collection-API

## Richtsnoeren

Alvorens de staat van de Speler het volgen uit te voeren overweeg de volgende richtlijnen.

* De spelerstaat wordt gegevens verwerkt over alle playbackstaten (geen het verdelen).
* U kunt veelvoudige spelerstaten tezelfdertijd meten.
* Het maximumaantal spelerstaten dat tijdens een playback kan worden gevolgd is 10.
* De de staatsmetriek van de speler wordt verzonden naar Analytics voor het melden van de Dichte vraag van Media slechts.
* De kennis van de toepassingsstatus wordt niet gehandhaafd nadat een staat ophoudt. Nadat een staat beëindigt, moet de staat opnieuw zijn begonnen om het volgen voort te zetten. Voor elke nieuwe playbackstaat, moet de staat van de speler opnieuw zijn begonnen.
* De staten van de speler worden gevangen voor elke individuele playbackzitting-spelerstaat niet over playbacks gegevens verwerkt.
