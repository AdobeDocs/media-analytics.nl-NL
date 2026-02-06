---
title: Toepassing onderbreekt tijdens afspelen
description: Leer hoe u onderbrekingen in het bijhouden van gegevens tijdens het afspelen van media kunt afhandelen.
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
exl-id: a84af6ad-dd4f-4f0d-93dd-66f2f84ddc0e
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---

# Toepassing onderbreekt tijdens afspelen{#handling-application-interrupts-during-playback}

Het afspelen in een mediatoepassing kan op verschillende manieren worden onderbroken. Een gebruiker kan bijvoorbeeld expliciet op pauzeren drukken of de toepassing op de achtergrond plaatsen. Ongeacht wat een onderbreking in media playback veroorzaakt, zijn de volgende instructies het zelfde.

1. Roep **`trackPause`** aan wanneer de toepassing wordt onderbroken (gaat naar de achtergrond, media pauzeert, enz.).
1. Roep **`trackPlay`** aan wanneer de toepassing terugkeert naar de voorgrond en/of de media het afspelen hervat.

>[!NOTE]
>
>Wanneer `trackSessionStart` wordt aangeroepen wanneer de toepassing vanaf de achtergrond wordt afgespeeld, kan dit ertoe leiden dat het afspelen tot dat punt niet wordt meegeteld in de totale afspeeltijd, en dat eerdere voortgangsmarkeringen, segmenten enzovoort verloren gaan. Roep in plaats daarvan `trackPlay` aan wanneer de app wordt geretourneerd en/of wanneer de media worden hervat.

## Veelgestelde vragen over het afhandelen van toepassingsonderbrekingen: {#faq-about-handling-application-interrupts}

* _hoe lang een toepassing zou moeten worden gesteund alvorens de zitting sluit?_

  Als de toepassing het afspelen op de achtergrond toestaat, kan het volgen door onze API&#39;s aan te roepen en sturen we al onze normale &#39;tracking pings&#39;-berichten. Niet veel video-apps staan afspelen op de achtergrond toe, behalve YouTube Red. Dit is echter wel mogelijk voor alle audio-apps. Als het afspelen op de achtergrond niet is toegestaan in de toepassing, is het aan te raden om gedurende één minuut in de pauzestatus te blijven en de volgende sessie te beëindigen. De toepassing kan niet blijven verzenden pingelt van de Pauze, omdat het in de meeste gevallen niet kan bepalen of de gebruiker zal terugkeren om de media te blijven bekijken, of zal bepalen wanneer het zal worden gedood. Het is ook een slechte ervaring om pingelt te blijven verzenden wanneer op de achtergrond.

* _wat is de correcte manier om het opnieuw beginnen volgen te behandelen nadat app in de achtergrond lange tijd is geweest?_

  De toepassing moet `trackSessionEnd` aanroepen om de volgende sessie te beëindigen. Van Versie 2.1, verzendt SDK &quot;eind&quot;pingelt om het achterste eind mee te delen dat de volgende zitting wordt gesloten.

* _wat over het opnieuw beginnen van de zelfde zitting?_

  Voor informatie over het hervatten van een volgende zitting, zie [ Hervatten inactieve zittingen ](resuming-inactive.md).SDK verzendt hervat pingel om het achterste eind mee te delen dat de gebruiker manueel de zitting hervat.
