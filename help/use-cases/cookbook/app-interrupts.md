---
title: Toepassing onderbreekt tijdens afspelen
description: Leer hoe u onderbrekingen in het bijhouden van gegevens tijdens het afspelen van media kunt afhandelen.
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
exl-id: a84af6ad-dd4f-4f0d-93dd-66f2f84ddc0e
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 2ce09eafeb8def909ae2a8ae7cc09a88b2f663af
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---

# Toepassing onderbreekt tijdens afspelen{#handling-application-interrupts-during-playback}

Het afspelen in een mediatoepassing kan op verschillende manieren worden onderbroken. Een gebruiker kan bijvoorbeeld expliciet op pauzeren drukken of de toepassing op de achtergrond plaatsen. Ongeacht wat een onderbreking in media playback veroorzaakt, zijn de volgende instructies het zelfde.

1. Bellen **`trackPause`** wanneer de toepassing wordt onderbroken (gaat naar achtergrond, media pauzeert, enz.).
1. Bellen **`trackPlay`** wanneer de toepassing terugkeert naar de voorgrond en/of de media het afspelen hervat.

>[!NOTE]
>
>Aanroepen `trackSessionStart` wanneer de toepassing vanaf de achtergrond wordt afgespeeld, kan dit ertoe leiden dat het afspelen tot dat punt niet wordt meegeteld bij de totale afspeeltijd, en dat eerdere voortgangsmarkeringen, segmenten enzovoort verloren gaan. In plaats daarvan, vraag `trackPlay` wanneer de app terugkeert en/of de media het afspelen hervat.

## Veelgestelde vragen over het afhandelen van toepassingsonderbrekingen: {#faq-about-handling-application-interrupts}

* _Hoe lang moet een toepassing worden geachtergrondd voordat de sessie wordt gesloten?_

  Als de toepassing het afspelen op de achtergrond toestaat, kan het volgen door onze API&#39;s aan te roepen en sturen we al onze normale &#39;tracking pings&#39;-berichten. Niet veel video-apps staan afspelen op de achtergrond toe, behalve YouTube Red. Dit is echter wel mogelijk voor alle audio-apps. Als het afspelen op de achtergrond niet is toegestaan in de toepassing, is het aan te raden om gedurende één minuut in de pauzestatus te blijven en de volgende sessie te beëindigen. De toepassing kan niet blijven verzenden pingelt van de Pauze, omdat het in de meeste gevallen niet kan bepalen of de gebruiker zal terugkeren om de media te blijven bekijken, of zal bepalen wanneer het zal worden gedood. Het is ook een slechte ervaring om pingelt te blijven verzenden wanneer op de achtergrond.

* _Wat is de juiste manier om het opnieuw opstarten van tracering af te handelen nadat de app al lange tijd op de achtergrond wordt uitgevoerd?_

  De toepassing moet `trackSessionEnd` om de volgende sessie te beëindigen. Van Versie 2.1, verzendt SDK &quot;eind&quot;pingelt om het achterste eind mee te delen dat de volgende zitting wordt gesloten.

* _En hoe zit het met het opnieuw opstarten van dezelfde sessie?_

  Voor informatie over het hervatten van een volgende zitting, zie [Niet-actieve sessies hervatten](resuming-inactive.md).SDK verzendt hervat pingel om het achterste eind mee te delen dat de gebruiker manueel de zitting hervat.
