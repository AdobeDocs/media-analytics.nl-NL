---
title: Toepassing onderbreekt tijdens afspelen
description: Onderbrekingen van het bijhouden van beelden tijdens het afspelen van media afhandelen.
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Toepassing onderbreekt tijdens afspelen{#handling-application-interrupts-during-playback}

Het afspelen in een mediatoepassing kan op verschillende manieren worden onderbroken: wanneer een gebruiker expliciet op pauze drukt of wanneer een gebruiker de toepassing op de achtergrond plaatst. Ongeacht wat een onderbreking in media playback veroorzaakt, zijn de volgende instructies het zelfde:

1. Roep aan **`trackPause`** wanneer de toepassing wordt onderbroken (gaat naar achtergrond, media pauzeert, enz.).
1. Roep aan **`trackPlay`** wanneer de toepassing terugkeert naar de voorgrond en/of de media het afspelen hervat.

>[!NOTE]
>
>Het Media Analytics-team heeft instanties gezien waarin klanten hebben gebeld `trackSessionStart` wanneer hun app van de achtergrond is teruggekeerd. Als u dit doet, wordt het afspelen tot dat moment niet meegeteld bij de totale afspeeltijd, en gaan er eerder voortgangsmarkeringen, segmenten enzovoort verloren. Roep in plaats daarvan aan `trackPlay` wanneer de app wordt geretourneerd en/of wanneer de media worden hervat.

## Veelgestelde vragen over het afhandelen van toepassingsonderbrekingen: {#faq-about-handling-application-interrupts}

* _Hoe lang moet een toepassing worden geachtergrondd voordat de sessie wordt gesloten?_

   Als de toepassing het afspelen op de achtergrond toestaat, kan het volgen door onze API&#39;s aan te roepen en sturen we al onze normale &#39;tracking pings&#39;-berichten. Niet veel video-apps staan afspelen op de achtergrond toe, behalve YouTube Red. Dit is echter wel mogelijk voor alle audio-apps. Als het afspelen op de achtergrond niet is toegestaan in de toepassing, is het aan te raden om gedurende één minuut in de pauzestatus te blijven en de volgende sessie te beëindigen. De toepassing kan niet blijven verzenden pingelt van de Pauze, omdat het in de meeste gevallen niet kan bepalen of de gebruiker zal terugkeren om de media te blijven bekijken, of zal bepalen wanneer het zal worden gedood. Het is ook een slechte ervaring om pingelt te blijven verzenden wanneer op de achtergrond.

* _Wat is de juiste manier om het opnieuw opstarten van tracering af te handelen nadat de app al lange tijd op de achtergrond wordt uitgevoerd?_

   De toepassing moet bellen `trackSessionEnd` om de volgende sessie te beëindigen. Van Versie 2.1, verzendt SDK &quot;eind&quot;pingelt om het achterste eind mee te delen dat de volgende zitting wordt gesloten.

* _En hoe zit het met het opnieuw opstarten van dezelfde sessie?_

   Zie deze pagina voor gedetailleerde instructies voor het opnieuw starten van een volgende sessie: Een eerder gesloten sessie [handmatig hervatten.](/help/sdk-implement/cookbook/resuming-inactive.md) SDK verzendt hervat pingel om het achterste eind mee te delen dat de gebruiker manueel de zitting hervat.

