---
title: Hoofdafspelen tussen advertenties oplossen
description: Leer hoe u onverwachte hoofd-elementen kunt afhandelen:aanroepen afspelen tussen advertenties.
uuid: 228b4812-c23e-40c8-ae2b-e15ca69b0bc2
exl-id: f27ce2ba-7584-4601-8837-d8316c641708
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---


# Tussenruimten tussen advertenties verwerken{#resolving-main-play-appearing-between-ads}

## PROBLEEM

In sommige scenario&#39;s kunt u `main:play` aanroepen tegenkomen die onverwacht plaatsvinden tussen het einde van de ene advertentie en het begin van de volgende advertentie. Als de vertraging tussen de volledige advertentie en de volgende aanroep van het ad-start meer dan 250 milliseconden bedraagt, zal Media SDK terugvallen op het verzenden van `main:play` aanroepen. Als deze fallback naar `main:play` optreedt tijdens een pre-roll en break, kan de metrische waarde voor het starten van de inhoud vroeg worden ingesteld.

Een tussenruimte tussen advertenties zoals hierboven beschreven, wordt door de Media SDK geïnterpreteerd als hoofdinhoud, omdat er geen overlapping met advertentie-inhoud is. Op de Media SDK is geen advertentie-informatie ingesteld en de speler bevindt zich in de afspeelstatus. Als er geen advertentie-informatie is en de spelerstatus wordt afgespeeld, geeft de Media SDK de duur van de tussenruimte standaard weer in hoofdinhoud. De duur van het afspelen kan niet naar null-advertentiegegevens worden gekopieerd.

## IDENTIFICATIE

Wanneer het gebruiken van Adobe zuivert of een sniffer van het netwerkpakket zoals Charles, als u de volgende Hartslagvraag in deze orde tijdens een pre-rol en onderbreking ziet:

* Begin sessie: `s:event:type=start` &amp; `s:asset:type=main`
* Begin toevoegen: `s:event:type=start` &amp; `s:asset:type=ad`
* Advertentiespel: `s:event:type=play` &amp; `s:asset:type=ad`
* Toevoegen voltooid: `s:event:type=complete` &amp; `s:asset:type=ad`
* Afspelen van hoofdinhoud: `s:event:type=play` &amp; `s:asset:type=main` **(onverwacht)**

* Begin toevoegen: `s:event:type=start` &amp; `s:asset:type=ad`
* Advertentiespel: `s:event:type=play` &amp; `s:asset:type=ad`
* Toevoegen voltooid: `s:event:type=complete` &amp; `s:asset:type=ad`
* Afspelen van hoofdinhoud: `s:event:type=play` &amp; `s:asset:type=main` **(verwacht)**

## RESOLUTIE

***Vertraging die de Ad Volledige vraag teweegbrengt.***

Verwerk de tussenruimte vanuit de speler door `trackEvent:AdComplete` laat aan te roepen voor de eerste advertentie, onmiddellijk gevolgd door `trackEvent:AdStart` voor de tweede advertentie. De toepassing moet het aanroepen van de gebeurtenis `AdComplete` blokkeren nadat het eerste bericht is voltooid. Roep `trackEvent:AdComplete` aan voor de laatste advertentie in het ad-einde. Roep `trackEvent:AdComplete` onmiddellijk aan als de speler kan zien dat het huidige advertentie-element het laatste element in het advertentiespoor is. Deze resolutie zal ertoe leiden dat minder dan één seconde van extra bestede tijd aan de voorafgaande advertentie-eenheid wordt toegeschreven.

**op en onderbrekingsbegin, met inbegrip van pre-rol:**

* Maak de objectinstantie `adBreak` voor het advertentie-einde, bijvoorbeeld `adBreakObject` .

* Roep `trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);` aan.

**op elk ad activabegin:**

* **Vraag`trackEvent(MediaHeartbeat.Event.AdComplete);`**

  >[!NOTE]
  >
  >Roep dit alleen aan als de vorige advertentie niet volledig was. Overweeg een waarde Van Boole om &quot;`isinAd`&quot;staat voor de vorige advertentie te handhaven.

* Maak de instantie van het advertentieobject voor het advertentie-element: bijvoorbeeld `adObject` .
* Vul de metagegevens van de advertentie in, `adCustomMetadata` .
* Roep `trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata);` aan.
* Roep `trackPlay()` aan als dit de eerste advertentie in een pre-rol en onderbreking is.

**op elk geëindigd advertentiemiddel:**

* **maak geen vraag**

  >[!NOTE]
  >
  >Als de toepassing weet dat dit de laatste advertentie in het advertentiespoor is, roept u `trackEvent:AdComplete` hier aan en slaat u de instelling `trackEvent:AdComplete` in het dialoogvenster `trackEvent:AdBreakComplete` over

**op ad overslaan:**

* Roep `trackEvent(MediaHeartbeat.Event.AdSkip);` aan.

**op en volledige onderbreking:**

* **Vraag`trackEvent(MediaHeartbeat.Event.AdComplete);`**

  >[!NOTE]
  >
  >Als deze stap al is uitgevoerd als onderdeel van de laatste aanroep van `trackEvent:AdComplete` , kan deze worden overgeslagen.

* Roep `trackEvent(MediaHeartbeat.Event.AdBreakComplete);` aan.
