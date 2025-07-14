---
title: Extra's bijhouden beschreven
description: Overzicht van het implementeren en volgen van de Media SDK.
uuid: 1607798b-c6ef-4d60-8e40-e958c345b09c
exl-id: c714d31f-3d08-4ded-a413-2762d53bec75
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 1%

---

# Overzicht{#overview}

De volgende instructies bieden richtlijnen voor implementatie met behulp van de 2.x SDK&#39;s.

>[!IMPORTANT]
>
>Als u een 1.x versie van SDK uitvoert, kunt u 1.x de Gidsen van Ontwikkelaars hier downloaden: [ Download SDKs.](/help/getting-started/download-sdks.md)

Het afspelen van advertenties omvat het bijhouden en afbreken, het starten, voltooien en het overslaan van advertenties. Gebruik de API van de mediaspeler om toetsspelergebeurtenissen te identificeren en de vereiste en optionele advertentievariabelen te vullen. Zie de uitvoerige lijst van meta-gegevens hier: [ Advertentieparameters.](../../implementation/variables/ad-parameters.md)

## Gebeurtenissen van Player {#player-events}


### Bij starten van advertentie-einde

>[!NOTE]
>Met inbegrip van voorrol

* Maak een `adBreak` -objectinstantie voor het ad-einde. Bijvoorbeeld `adBreakObject` .

* Roep `trackEvent` aan voor het begin van het advertentieeinde met uw `adBreakObject` .

### Bij elke advertentie-asset start

* Maak een instantie van een advertentieobject voor het advertentie-element. Bijvoorbeeld `adObject` .
* Vul de metagegevens van de advertentie in, `adCustomMetadata` .
* Roep `trackEvent` aan voor het starten van de advertentie.

### Op elke advertentie compleet

* Roep `trackEvent` aan voor de advertentie is voltooid.

### Op advertentie slaan

* Roep `trackEvent` aan voor de advertentie.

### Bij voltooiing van advertentie

* Roep `trackEvent` aan voor het advertentieeinde is voltooid.

## Toevoegen en bijhouden {#implement-ad-tracking}

### Constanten voor bijhouden van advertenties

| Naam van constante | Beschrijving   |
|---|---|
| `AdBreakStart` | Constante voor het bijhouden van de gebeurtenis AdBreak Start |
| `AdBreakComplete` | Constante voor het bijhouden van de gebeurtenis AdBreak Complete |
| `AdStart` | Constante voor het bijhouden van de gebeurtenis Ad Start |
| `AdComplete` | Constante voor het bijhouden van de gebeurtenis Advertentie voltooid |
| `AdSkip` | Constante voor het bijhouden van de gebeurtenis Advertentie overslaan |

### Implementatiestappen

1. Bepaal wanneer de grens van de advertentieruimte begint, met inbegrip van pre-rol, en creeer `AdBreakObject` door de informatie van de advertentierak te gebruiken.

   `AdBreakObject` reference:

   | Naam variabele | Beschrijving | Vereist |
   | --- | --- | :---: |
   | `name` | De naam van het invoegpunt, zoals pre-roll, mid-roll en post-roll. | Ja |
   | `position` | De getalpositie van het advertentierak binnen de inhoud, beginnend met 1. | Ja |
   | `startTime` | Waarde van afspeelkop aan het begin van het advertentieeinde. | Ja |

1. Roep `trackEvent()` aan met `AdBreakStart` in de `MediaHeartbeat` -instantie om het ad-einde te volgen.

1. Bepaal wanneer de advertentie begint en creeer een `AdObject` instantie gebruikend de advertentieinformatie.

   `AdObject` reference:

   | Naam variabele | Beschrijving | Vereist |
   | --- | --- | :---: |
   | `name` | Vriendelijke naam van de advertentie. | Ja |
   | `adId` | De unieke id voor de advertentie. | Ja |
   | `position` | De numerieke positie van de advertentie binnen het advertentiespoor, beginnend met 1. | Ja |
   | `length` | Ad-lengte | Ja |

1. Voeg desgewenst standaard- en/of advertentiemetagegevens toe aan de volgende sessie via de variabelen van de contextgegevens.

   * **Standaard en meta-gegevens -** voor norm en meta-gegevens, creeer een woordenboek van standaard en de waardeparen van de meta-gegevens zeer belangrijke gebruikend de sleutels voor uw platform.
   * **Douane en meta-gegevens -** voor douanemetagegevens, creeer een veranderlijk voorwerp voor de variabelen van douanegegevens en bevolk met de gegevens voor de huidige advertentie.

1. Roep `trackEvent()` aan met de gebeurtenis `AdStart` in de instantie `MediaHeartbeat` om het afspelen van de advertentie te volgen.

   Neem een verwijzing naar de aangepaste metagegevensvariabele (of een leeg object) op als de derde parameter in de gebeurtenisaanroep.

1. Wanneer het afspelen van de advertentie het einde van de advertentie heeft bereikt, roept u `trackEvent()` aan met de gebeurtenis `AdComplete` .

1. Als het afspelen van de advertentie niet is voltooid omdat de gebruiker de advertentie heeft overgeslagen, houdt u de gebeurtenis `AdSkip` bij.
1. Herhaal stap 3 tot en met 7 opnieuw als er extra advertenties binnen dezelfde `AdBreak` zijn.
1. Wanneer het ad-einde is voltooid, gebruikt u de gebeurtenis `AdBreakComplete` om het bij te houden.

>[!IMPORTANT]
>
>Zorg ervoor dat u de afspeelkop van de inhoudsspeler (`l:event:playhead`) NIET verhoogt tijdens het afspelen van de advertentie (`s:asset:type=ad`). Als u dat wel doet, hebben de meetgegevens voor Tijd van inhoud een negatief effect.

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
