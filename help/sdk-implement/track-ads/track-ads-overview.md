---
title: Overzicht
description: Overzicht van het implementeren en volgen van de Media SDK.
uuid: 1607798b-c6ef-4d60-8e40-e958c345b09c
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Overzicht{#overview}

>[!IMPORTANT]
>
>De volgende instructies bieden richtlijnen voor implementatie met behulp van de 2.x SDK&#39;s. Als u een 1.x-versie van de SDK implementeert, kunt u hier de 1.x-handleidingen voor ontwikkelaars downloaden: SDK&#39;s [downloaden.](/help/sdk-implement/download-sdks.md)

Het afspelen van advertenties omvat het bijhouden en afbreken, het starten, voltooien en het overslaan van advertenties. Gebruik de API van de mediaspeler om toetsspelergebeurtenissen te identificeren en de vereiste en optionele advertentievariabelen te vullen. Zie de uitgebreide lijst met metagegevens hier: Parameters [toevoegen.](/help/metrics-and-metadata/ad-parameters.md)

## Gebeurtenissen van Player {#player-events}


### Bij starten van advertentie-einde

>[!NOTE]
>Met inbegrip van voorrol

* Maak een `adBreak` objectinstantie voor het advertentie-einde. Bijvoorbeeld, `adBreakObject`.

* Vraag `trackEvent` om het begin van de advertentie met uw `adBreakObject`.

### Bij elke advertentie-asset start

* Maak een instantie van een advertentieobject voor het advertentie-element. Bijvoorbeeld, `adObject`.
* De metagegevens van de advertentie vullen, `adCustomMetadata`.
* Vraag `trackEvent` om het begin van de advertentie.

### Op elke advertentie compleet

* Vraag `trackEvent` om de advertentie volledig.

### Op advertentie slaat u over

* Vraag `trackEvent` om het overslaan van de advertentie.

### Bij voltooiing van advertentie

* Vraag `trackEvent` om het volledige advertentierampen.

## Toevoegen en bijhouden {#implement-ad-tracking}

### Constanten voor bijhouden van advertenties

| Naam van constante | Beschrijving |
|---|---|
| `AdBreakStart` | Constante voor het bijhouden van de gebeurtenis AdBreak Start |
| `AdBreakComplete` | Constante voor het bijhouden van de gebeurtenis AdBreak Complete |
| `AdStart` | Constante voor het bijhouden van de gebeurtenis Ad Start |
| `AdComplete` | Constante voor het bijhouden van de gebeurtenis Advertentie voltooid |
| `AdSkip` | Constante voor het bijhouden van de gebeurtenis Advertentie overslaan |

### Uitvoeringsstappen

1. Bepaal wanneer de grens van de advertentierak begint, met inbegrip van pre-rol, en creeer een `AdBreakObject` door de informatie van de advertentierak te gebruiken.

   `AdBreakObject` referentie:

   | Naam variabele | Beschrijving | Vereist |
   | --- | --- | :---: |
   | `name` | De naam van het invoegpunt, zoals pre-roll, mid-roll en post-roll. | Ja |
   | `position` | De getalpositie van het advertentierak binnen de inhoud, beginnend met 1. | Ja |
   | `startTime` | Waarde van afspeelkop aan het begin van het advertentieeinde. | Ja |

1. Roep `trackEvent()` met `AdBreakStart` in de `MediaHeartbeat` instantie aan om het advertentieeinde te volgen.

1. Bepaal wanneer de advertentie begint en creeer een `AdObject` instantie gebruikend de advertentieinformatie.

   `AdObject` referentie:

   | Naam variabele | Beschrijving | Vereist |
   | --- | --- | :---: |
   | `name` | Vriendelijke naam van de advertentie. | Ja |
   | `adId` | De unieke id voor de advertentie. | Ja |
   | `position` | De numerieke positie van de advertentie binnen het advertentiespoor, beginnend met 1. | Ja |
   | `length` | Ad-lengte | Ja |

1. Voeg desgewenst standaard- en/of advertentiemetagegevens toe aan de volgende sessie via de variabelen van de contextgegevens.

   * **Standaard en metagegevens -** Voor standaard- en metagegevens maakt u een woordenboek van standaard- en metagegevenssleutelwaardeparen met de toetsen voor uw platform.
   * **Aangepast en metagegevens -** Voor aangepaste metagegevens maakt u een variabel object voor de aangepaste gegevensvariabelen en vult u de gegevens voor de huidige advertentie in.

1. Roep `trackEvent()` met de `AdStart` gebeurtenis in de `MediaHeartbeat` instantie aan om het afspelen van de advertentie te volgen.

   Neem een verwijzing naar de aangepaste metagegevensvariabele (of een leeg object) op als de derde parameter in de gebeurtenisaanroep.

1. Wanneer het afspelen van de advertentie het einde van de advertentie heeft bereikt, roept u `trackEvent()` de `AdComplete` gebeurtenis aan.

1. Als het afspelen van de advertentie niet is voltooid omdat de gebruiker de advertentie heeft overgeslagen, houdt u de `AdSkip` gebeurtenis bij.
1. Herhaal stap 3 tot en met 7 opnieuw als er extra advertenties binnen dezelfde `AdBreak`advertentie zijn.
1. Wanneer het advertentieeinde is voltooid, gebruikt u de `AdBreakComplete` gebeurtenis om het te volgen.

>[!IMPORTANT]
>
>Zorg ervoor dat u de afspeelkop van de inhoudsspeler (`l:event:playhead`) NIET verhoogt tijdens het afspelen van de advertentie (`s:asset:type=ad`). Als u dat wel doet, hebben de meetgegevens voor de Content Time Spent een negatief effect.

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
