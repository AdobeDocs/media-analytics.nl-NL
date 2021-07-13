---
title: Hoofdafspelen tussen advertenties oplossen
description: '"Leer hoe u onverwachte hoofd-/afspeelaanroepen tussen advertenties kunt afhandelen."'
uuid: 228b4812-c23e-40c8-ae2b-e15ca69b0bc2
exl-id: f27ce2ba-7584-4601-8837-d8316c641708
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 1%

---

# Hoofdcontent omzetten:afspelen tussen advertenties{#resolving-main-play-appearing-between-ads}

## PROBLEEM

In sommige scenario&#39;s die van de advertentie volgen, kon u `main:play` vraag ontmoeten onverwacht tussen het eind van één advertentie en het begin van volgende advertentie voorkomen. Als de vertraging tussen de volledige vraag van de advertentie en de volgende vraag van het ad begin groter is dan 250 milliseconden, zal SDK van Media terug naar het verzenden van `main:play` vraag vallen. Als deze fallback naar `main:play` tijdens een pre-rol en onderbreking voorkomt, kan de metrisch van de inhoudbegin vroeg worden geplaatst.

Een tussenruimte tussen advertenties zoals hierboven beschreven, wordt door de Media SDK geïnterpreteerd als hoofdinhoud, omdat er geen overlapping met advertentie-inhoud is. Op de Media SDK is geen advertentie-informatie ingesteld en de speler bevindt zich in de afspeelstatus. Als er geen Advertentie-informatie is en de spelerstatus wordt afgespeeld, dan meldt de Media SDK de duur van het hiaat aan belangrijkste inhoud door gebrek. De duur van het afspelen kan niet naar null-advertentiegegevens worden gekopieerd.

## IDENTIFICATIE

Terwijl het gebruiken van Adobe zuivert of een sniffer van het netwerkpakket zoals Charles, als u de volgende Hartslagvraag in deze orde tijdens een pre-rol en onderbreking ziet:

* Begin sessie: `s:event:type=start` &amp; `s:asset:type=main`
* Begin van advertentie: `s:event:type=start` &amp; `s:asset:type=ad`
* Advertentiespel: `s:event:type=play` &amp; `s:asset:type=ad`
* Toevoegen voltooid: `s:event:type=complete` &amp; `s:asset:type=ad`
* Afspelen van hoofdinhoud: `s:event:type=play` &amp; `s:asset:type=main` **(onverwacht)**

* Begin van advertentie: `s:event:type=start` &amp; `s:asset:type=ad`
* Advertentiespel: `s:event:type=play` &amp; `s:asset:type=ad`
* Toevoegen voltooid: `s:event:type=complete` &amp; `s:asset:type=ad`
* Afspelen van hoofdinhoud: `s:event:type=play` &amp; `s:asset:type=main` **(verwacht)**

## RESOLUTIE

***Vertraging die de Ad Complete vraag teweegbrengt.***

Verwerk de tussenruimte vanuit de speler door `trackEvent:AdComplete` te laat aan te roepen voor de eerste advertentie, onmiddellijk gevolgd door `trackEvent:AdStart` voor de tweede advertentie. De toepassing moet het aanroepen van de gebeurtenis `AdComplete` blokkeren nadat de eerste bewerking is voltooid. Zorg ervoor dat u `trackEvent:AdComplete` voor de laatste advertentie in het ad-einde aanroept. Roep `trackEvent:AdComplete` onmiddellijk aan als de speler kan vaststellen dat het huidige ad-element het laatste element in het ad-einde is. Deze resolutie zal ertoe leiden dat minder dan één seconde van extra bestede tijd aan de voorafgaande advertentie-eenheid wordt toegeschreven.

**Bij starten ad-break, inclusief pre-roll:**

* Maak de `adBreak`-objectinstantie voor het advertentiepalk; bijvoorbeeld `adBreakObject`.

* Roep `trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);`.

**Bij elke advertentie-asset start:**

* **Bellen`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >Roep dit alleen aan als de vorige advertentie niet volledig was. Overweeg een Booleaanse waarde om de status &quot;`isinAd`&quot; voor de vorige advertentie te behouden.

* Maak de instantie van het advertentieobject voor het advertentie-element: bijvoorbeeld `adObject`.
* Vul de metagegevens van de advertentie in, `adCustomMetadata`.
* Roep `trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata);`.
* Roep `trackPlay()` aan als dit de eerste advertentie in een pre-rol en onderbreking is.

**Op elk advertentiemiddel voltooid:**

* **Geen vraag maken**

   >[!NOTE]
   >
   >Als de toepassing weet dat dit de laatste advertentie in het advertentiesonderbreking is, roept u `trackEvent:AdComplete` hier aan en slaat u de instelling `trackEvent:AdComplete` in `trackEvent:AdBreakComplete` over

**Op advertentie slaat u over:**

* Roep `trackEvent(MediaHeartbeat.Event.AdSkip);`.

**Bij ad-break voltooid:**

* **Bellen`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >Als deze stap reeds hierboven als deel van laatste `trackEvent:AdComplete` vraag wordt uitgevoerd, dan kan dit worden overgeslagen.

* Roep `trackEvent(MediaHeartbeat.Event.AdBreakComplete);`.
