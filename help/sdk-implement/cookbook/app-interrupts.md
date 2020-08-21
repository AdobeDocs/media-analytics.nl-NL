---
title: Handlingstoepassing onderbreekt tijdens afspelen
description: Hoe te om onderbrekingen aan het volgen tijdens playback van media te behandelen.
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
translation-type: tm+mt
source-git-commit: 29b0d38e904a561d467ba0432b255fdb17d6b829
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 2%

---


# Handlingstoepassing onderbreekt tijdens afspelen{#handling-application-interrupts-during-playback}

De playback in een media toepassing kan op een verscheidenheid van manieren worden onderbroken: een gebruiker drukt uitdrukkelijk pauze, of wanneer een gebruiker de toepassing in de achtergrond zet. Ongeacht wat een onderbreking in media playback veroorzaakt, zijn de volgende instructies het zelfde:

1. Oproep **`trackPause`** wanneer de toepassing wordt onderbroken (gaat naar achtergrond, media pauzeren, enz.).
1. Oproep **`trackPlay`** wanneer de toepassing op de voorgrond en/of de media het spelen hervat.

>[!NOTE]
>
>Het team van de Analyse van Media heeft instanties gezien waar de klanten riepen `trackSessionStart` wanneer hun app van de achtergrond is teruggekeerd. Het doen dit resulteert in de playback tot dat punt niet telend naar de totale playbacktijd, samen met het verliezen van vroegere vooruitgangstellers, segmenten, etc. In plaats daarvan, vraag `trackPlay` wanneer app terugkeert en/of de media het spelen hervat.

## Veelgestelde vragen over de verwerking van toepassingsonderbrekingen: {#faq-about-handling-application-interrupts}

* _Hoe lang zou een app moeten worden achteraan alvorens de zitting sluit?_

   Als de toepassing achtergrondplayback toestaat, kan het blijven volgen door onze APIs te roepen en wij zullen al onze regelmatige het volgen pingelt verzenden. Niet veel videoapps staan achtergrondplayback behalve YouTube Red toe, nochtans, alle audioapps staan dit toe. Als de toepassing achtergrondplayback niet toestaat, dan is het raadzaam om in de Staat van de Pauze één minuut te blijven, en dan de volgende zitting te beëindigen. De toepassing kan niet blijven verzendend pingelt van de Pauze, omdat in de meeste gevallen het niet kan bepalen als de gebruiker zal terugkeren om het bekijken van de media voort te zetten, of bepalen wanneer het zal worden gedood. Het is ook een slechte ervaring blijven verzenden pingelt wanneer op de achtergrond.

* _Wat is de correcte manier om het opnieuw beginnen volgen te behandelen nadat app lang op de achtergrond is geweest?_

   De aanvraag moet `trackSessionEnd` om de volgende sessie te beëindigen. Van Versie 2.1, verzendt SDK een &quot;eind&quot;pingelt om het achterste eind mee te delen dat de volgende zitting gesloten is.

* _Hoe zit het met het opnieuw starten van dezelfde sessie?_

   Voor gedetailleerde instructies bij het opnieuw beginnen van een volgende zitting, zie deze pagina: [Een eerder gesloten sessie handmatig hervatten](/help/sdk-implement/cookbook/resuming-inactive.md). SDK verzendt een hervat pingelt om het achterste eind mee te delen dat de gebruiker manueel de zitting hervat.

