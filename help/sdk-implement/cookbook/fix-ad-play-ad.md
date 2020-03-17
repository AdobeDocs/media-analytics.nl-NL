---
title: Hoofdafspelen tussen advertenties oplossen
description: Onverwachte hoofd afhandelen:aanroepen afspelen tussen advertenties.
uuid: 228b4812-c23e-40c8-ae2b-e15ca69b0bc2
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Hoofdbestand omzetten:afspelen tussen advertenties{#resolving-main-play-appearing-between-ads}

## PROBLEEM

In sommige scenario&#39;s van de advertentie, kon u `main:play` vraag tegenkomen die onverwacht tussen het eind van één en het begin van de volgende advertentie voorkomt. Als de vertraging tussen de volledige vraag van de advertentie en de volgende vraag van het ad begin groter is dan 250 milliseconden, zal SDK van Media terug naar het verzenden van `main:play` vraag vallen. Als deze terugval tijdens een pre-rol en een onderbreking voorkomt, kan de metrisch van de inhoudsbegin vroeg worden geplaatst. `main:play`

Een tussenruimte tussen advertenties zoals hierboven beschreven, wordt door de Media SDK geïnterpreteerd als hoofdinhoud, omdat er geen overlapping met advertentie-inhoud is. Op de Media SDK is geen advertentie-informatie ingesteld en de speler bevindt zich in de afspeelstatus. Als er geen Advertentie-informatie is en de spelerstatus wordt afgespeeld, dan meldt de Media SDK de duur van het hiaat aan belangrijkste inhoud door gebrek. De duur van het afspelen kan niet naar null-advertentiegegevens worden gekopieerd.

## IDENTIFICATIE

Wanneer u Adobe Debug of een snuffelaar van een netwerkpakket zoals Charles gebruikt, als u de volgende hartslagvraag in deze orde tijdens een pre-rol en onderbreking ziet:

* Begin sessie: `s:event:type=start` &amp; `s:asset:type=main`
* Begin van advertentie: `s:event:type=start` &amp; `s:asset:type=ad`
* Advertentiespel: `s:event:type=play` &amp; `s:asset:type=ad`
* Toevoegen voltooid: `s:event:type=complete` &amp; `s:asset:type=ad`
* Afspelen van hoofdinhoud: `s:event:type=play` &amp; `s:asset:type=main`**(onverwacht)**

* Begin van advertentie: `s:event:type=start` &amp; `s:asset:type=ad`
* Advertentiespel: `s:event:type=play` &amp; `s:asset:type=ad`
* Toevoegen voltooid: `s:event:type=complete` &amp; `s:asset:type=ad`
* Afspelen van hoofdinhoud: `s:event:type=play` &amp; `s:asset:type=main`**(verwacht)**

## RESOLUTIE

***Vertraging die de Ad Complete vraag teweegbrengt.***

Behandel de tussenruimte vanuit de speler door `trackEvent:AdComplete` laat aan te roepen voor de eerste advertentie, onmiddellijk gevolgd door `trackEvent:AdStart` de tweede advertentie. De app moet het aanroepen van de `AdComplete` gebeurtenis blokkeren nadat de eerste bewerking is voltooid. Zorg ervoor dat u `trackEvent:AdComplete` voor de laatste advertentie in het advertentiesonderbreking belt. Als de speler kan vaststellen dat het huidige advertentie-element het laatste element in het ad-einde is, roept u dit `trackEvent:AdComplete` onmiddellijk aan. Deze resolutie zal ertoe leiden dat minder dan één seconde van extra bestede tijd aan de voorafgaande advertentie-eenheid wordt toegeschreven.

**Bij starten ad-break, inclusief pre-roll:**

* Maak de `adBreak` objectinstantie voor het advertentie-einde; bijvoorbeeld `adBreakObject`.

* Bel `trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);`.

**Bij elke advertentie-asset start:**

* **Bellen`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >Roep dit alleen aan als de vorige advertentie niet volledig was. Overweeg een Booleaanse waarde om de status &quot;`isinAd`&quot; voor de vorige advertentie te behouden.

* Maak de instantie van het advertentieobject voor het advertentie-element: bijvoorbeeld `adObject`.
* De metagegevens van de advertentie vullen, `adCustomMetadata`.
* Bel `trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata);`.
* Roep `trackPlay()` als dit de eerste advertentie is in een pre-rol en onderbreking.

**Op elk advertentiemiddel voltooid:**

* **Geen vraag maken**

   >[!NOTE]
   >
   >Als de toepassing weet dat dit de laatste advertentie in het advertentiespoor is, roept u `trackEvent:AdComplete` hier aan en slaat u de instelling `trackEvent:AdComplete` in het dialoogvenster `trackEvent:AdBreakComplete`

**Op advertentie slaat u over:**

* Bel `trackEvent(MediaHeartbeat.Event.AdSkip);`.

**Bij ad-break voltooid:**

* **Bellen`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >Als deze stap hierboven reeds als deel van de laatste `trackEvent:AdComplete` vraag wordt uitgevoerd, dan kan dit worden overgeslagen.

* Bel `trackEvent(MediaHeartbeat.Event.AdBreakComplete);`.

