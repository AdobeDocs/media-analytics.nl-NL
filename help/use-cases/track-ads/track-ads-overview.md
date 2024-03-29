---
title: Extra's bijhouden
description: Overzicht van het implementeren en volgen van de Media SDK.
uuid: 1607798b-c6ef-4d60-8e40-e958c345b09c
exl-id: c714d31f-3d08-4ded-a413-2762d53bec75
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 2%

---

# Overzicht{#overview}

De volgende instructies bieden richtlijnen voor implementatie met behulp van de 2.x SDK&#39;s.

>[!IMPORTANT]
>
>Als u een 1.x-versie van de SDK implementeert, kunt u hier de 1.x-handleidingen voor ontwikkelaars downloaden: [SDK&#39;s downloaden.](/help/getting-started/download-sdks.md)

Het afspelen van advertenties omvat het bijhouden en afbreken, het starten, voltooien en het overslaan van advertenties. Gebruik de API van de mediaspeler om toetsspelergebeurtenissen te identificeren en de vereiste en optionele advertentievariabelen te vullen. Zie de uitgebreide lijst met metagegevens hier: [Toegevoegde parameters.](../../implementation/variables/ad-parameters.md)

## Gebeurtenissen van Player {#player-events}


### Bij starten van advertentie-einde

>[!NOTE]
>Met inbegrip van voorrol

* Een `adBreak` -objectinstantie voor het ad-einde. Bijvoorbeeld, `adBreakObject`.

* Bellen `trackEvent` voor het afbreken van de advertentie begint u met uw `adBreakObject`.

### Bij elke advertentie-asset start

* Maak een instantie van een advertentieobject voor het advertentie-element. Bijvoorbeeld, `adObject`.
* De metagegevens van de advertentie invullen, `adCustomMetadata`.
* Bellen `trackEvent` voor het begin van de advertentie.

### Op elke advertentie compleet

* Bellen `trackEvent` voor de advertentie is voltooid.

### Op advertentie slaat u over

* Bellen `trackEvent` voor de advertentie.

### Bij voltooiing van advertentie

* Bellen `trackEvent` voor het advertentieeinde is voltooid.

## Toevoegen en bijhouden {#implement-ad-tracking}

### Constanten voor bijhouden van advertenties

| Naam van constante | Beschrijving   |
|---|---|
| `AdBreakStart` | Constante voor het bijhouden van de gebeurtenis AdBreak Start |
| `AdBreakComplete` | Constante voor het bijhouden van de gebeurtenis AdBreak Complete |
| `AdStart` | Constante voor het bijhouden van de gebeurtenis Ad Start |
| `AdComplete` | Constante voor het bijhouden van de gebeurtenis Advertentie voltooid |
| `AdSkip` | Constante voor het bijhouden van de gebeurtenis Advertentie overslaan |

### Uitvoeringsstappen

1. Identificeer wanneer de grens van de advertentie begint, met inbegrip van pre-rol, en creeer een `AdBreakObject` met behulp van de informatie over het advertentieeinde.

   `AdBreakObject` referentie:

   | Naam variabele | Beschrijving | Vereist |
   | --- | --- | :---: |
   | `name` | De naam van het invoegpunt, zoals pre-roll, mid-roll en post-roll. | Ja |
   | `position` | De getalpositie van het advertentierak binnen de inhoud, beginnend met 1. | Ja |
   | `startTime` | Waarde van afspeelkop aan het begin van het advertentieeinde. | Ja |

1. Bellen `trackEvent()` with `AdBreakStart` in de `MediaHeartbeat` -instantie om het ad-einde te volgen.

1. Identificeer wanneer de advertentie begint en creeer `AdObject` -instantie die de advertentiegegevens gebruikt.

   `AdObject` referentie:

   | Naam variabele | Beschrijving | Vereist |
   | --- | --- | :---: |
   | `name` | Vriendelijke naam van de advertentie. | Ja |
   | `adId` | De unieke id voor de advertentie. | Ja |
   | `position` | De numerieke positie van de advertentie binnen het advertentiespoor, beginnend met 1. | Ja |
   | `length` | Ad-lengte | Ja |

1. Voeg desgewenst standaard- en/of advertentiemetagegevens toe aan de volgende sessie via de variabelen van de contextgegevens.

   * **Standaard en metagegevens -** Voor standaard- en metagegevens maakt u een woordenboek van standaard- en metagegevenssleutelwaardeparen met de toetsen voor uw platform.
   * **Aangepaste en metagegevens -** Voor aangepaste metagegevens maakt u een variabelenobject voor de aangepaste gegevensvariabelen en vult u de gegevens voor de huidige advertentie in.

1. Bellen `trackEvent()` met de `AdStart` in de `MediaHeartbeat` -instantie om het afspelen van de advertentie te volgen.

   Neem een verwijzing naar de aangepaste metagegevensvariabele (of een leeg object) op als de derde parameter in de gebeurtenisaanroep.

1. Wanneer het afspelen van de advertentie het einde van de advertentie heeft bereikt, roept u `trackEvent()` met de `AdComplete` gebeurtenis.

1. Als het afspelen van de advertentie niet is voltooid omdat de gebruiker de advertentie heeft overgeslagen, voert u de `AdSkip` gebeurtenis.
1. Als er extra advertenties zijn binnen dezelfde `AdBreak`Herhaal stap 3 tot en met 7 opnieuw.
1. Wanneer het advertentieeinde is voltooid, gebruikt u de `AdBreakComplete` om de gebeurtenis te volgen.

>[!IMPORTANT]
>
>Zorg ervoor dat u de afspeelkop van de inhoudsspeler NIET verhoogt (`l:event:playhead`) tijdens het afspelen van advertenties (`s:asset:type=ad`). Als u dat wel doet, hebben de meetgegevens voor Tijd van inhoud een negatief effect.

In de volgende voorbeeldcode wordt de JavaScript 2.x SDK gebruikt voor een HTML5-mediaspeler.

```js
/* Call on ad break start */

if (e.type == "ad break start") {
    var adBreakObject = MediaHeartbeat.createAdBreakObject("mid-roll", 2, 500);
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);
};

/* Call on ad start */
if (e.type == "ad start") {
    var adObject = MediaHeartbeat.createAdObject("PepsiOne", "123456ab", 1, 30);
    /* Set custom context data */
    var adCustomMetadata = {
        affiliate:"Sample affiliate",
        campaign:"Sample ad campaign",
        creative:"Sample creative"
    }
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata);
};

/* Call on ad complete */
if (e.type == "ad complete") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete);
};

/* Call on ad skip */
if (e.type == "ad skip") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip);
};

/* Call on ad break complete */
if (e.type == "ad break complete") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete);
};
```
