---
title: Hoofdafspelen tussen advertenties oplossen
description: "Leer hoe u onverwachte hoofd-/afspeelaanroepen tussen advertenties kunt afhandelen."
uuid: 228b4812-c23e-40c8-ae2b-e15ca69b0bc2
exl-id: f27ce2ba-7584-4601-8837-d8316c641708
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---


# Tussenruimten tussen advertenties verwerken{#resolving-main-play-appearing-between-ads}

## PROBLEEM

In sommige scenario&#39;s voor het bijhouden van een advertentie kunt u `main:play` oproepen die onverwacht tussen het eind van één en het begin van volgende advertentie voorkwamen. Als de vertraging tussen de volledige vraag van de advertentie en de volgende vraag van het ad begin groter is dan 250 milliseconden, zal SDK van Media terug naar het verzenden vallen `main:play` oproepen. Als dit terugvalt op `main:play` komt tijdens een pre-rol en onderbreking voor, kan de metrisch van de inhoudstart vroeg worden geplaatst.

Een tussenruimte tussen advertenties zoals hierboven beschreven, wordt door de Media SDK geïnterpreteerd als hoofdinhoud, omdat er geen overlapping met advertentie-inhoud is. Op de Media SDK is geen advertentie-informatie ingesteld en de speler bevindt zich in de afspeelstatus. Als er geen Advertentie-informatie is en de spelerstatus wordt afgespeeld, dan meldt de Media SDK de duur van het hiaat aan belangrijkste inhoud door gebrek. De duur van het afspelen kan niet naar null-advertentiegegevens worden gekopieerd.

## IDENTIFICATIE

Terwijl het gebruiken van Adobe zuivert of een sniffer van het netwerkpakket zoals Charles, als u de volgende Hartslagvraag in deze orde tijdens een pre-rol en onderbreking ziet:

* Begin sessie: `s:event:type=start` &amp; `s:asset:type=main`
* Begin van advertentie: `s:event:type=start` &amp; `s:asset:type=ad`
* Advertentiespel: `s:event:type=play` &amp; `s:asset:type=ad`
* Toevoegen voltooid: `s:event:type=complete` &amp; `s:asset:type=ad`
* Afspelen van hoofdinhoud: `s:event:type=play` &amp; `s:asset:type=main` **(onverwacht)**

* Begin van advertentie: `s:event:type=start` &amp; `s:asset:type=ad`
* Advertentiespel: `s:event:type=play` &amp; `s:asset:type=ad`
* Toevoegen voltooid: `s:event:type=complete` &amp; `s:asset:type=ad`
* Afspelen van hoofdinhoud: `s:event:type=play` &amp; `s:asset:type=main` **(verwacht)**

## RESOLUTIE

***Vertraging die de Ad Complete vraag teweegbrengt.***

Handel de tussenruimte vanuit de speler af door `trackEvent:AdComplete` laat voor de eerste advertentie, onmiddellijk gevolgd door `trackEvent:AdStart` voor de tweede advertentie. De app moet het oproepen van de `AdComplete` gebeurtenis nadat de eerste bewerking is voltooid. Zorg ervoor dat u belt `trackEvent:AdComplete` voor de laatste advertentie in het advertentieeinde. Als de speler kan vaststellen dat het huidige advertentie-element het laatste element in het advertentiespoor is, roept u `trackEvent:AdComplete` onmiddellijk. Deze resolutie zal ertoe leiden dat minder dan één seconde van extra bestede tijd aan de voorafgaande advertentie-eenheid wordt toegeschreven.

**Bij starten ad-break, inclusief pre-roll:**

* Maak de `adBreak` objectinstantie voor het ad-einde; bijvoorbeeld: `adBreakObject`.

* Bellen `trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);`.

**Bij elke advertentie-asset start:**

* **Bellen`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >Roep dit alleen aan als de vorige advertentie niet volledig was. Neem bijvoorbeeld een Booleaanse waarde om een &quot;`isinAd`&quot; staat voor de vorige advertentie.

* Maak de instantie van het advertentieobject voor het advertentie-element: bijvoorbeeld: `adObject`.
* De metagegevens van de advertentie invullen, `adCustomMetadata`.
* Bellen `trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata);`.
* Bellen `trackPlay()` als dit de eerste advertentie in een pre-rol en onderbreking is.

**Op elk advertentiemiddel voltooid:**

* **Geen vraag maken**

   >[!NOTE]
   >
   >Als de toepassing weet dat dit de laatste advertentie in het advertentiesonderbreking is, roept u `trackEvent:AdComplete` hier en slaat instelling over `trackEvent:AdComplete` in de `trackEvent:AdBreakComplete`

**Op advertentie slaat u over:**

* Bellen `trackEvent(MediaHeartbeat.Event.AdSkip);`.

**Bij ad-break voltooid:**

* **Bellen`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >Als deze stap al is uitgevoerd als onderdeel van de laatste `trackEvent:AdComplete` Deze aanroep kan worden overgeslagen.

* Bellen `trackEvent(MediaHeartbeat.Event.AdBreakComplete);`.
