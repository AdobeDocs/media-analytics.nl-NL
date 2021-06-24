---
title: Toepassing onderbreekt tijdens afspelen
description: Leer hoe u onderbrekingen in het bijhouden van gegevens tijdens het afspelen van media kunt afhandelen.
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
exl-id: a84af6ad-dd4f-4f0d-93dd-66f2f84ddc0e
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 1%

---

# Handlingstoepassing onderbreekt tijdens afspelen{#handling-application-interrupts-during-playback}

Het afspelen in een mediatoepassing kan op verschillende manieren worden onderbroken: wanneer een gebruiker expliciet op pauze drukt of wanneer een gebruiker de toepassing op de achtergrond plaatst. Ongeacht wat een onderbreking in media playback veroorzaakt, zijn de volgende instructies het zelfde:

1. Roep **`trackPause`** aan wanneer de toepassing wordt onderbroken (gaat naar achtergrond, media pauzeert, enz.).
1. Roep **`trackPlay`** aan wanneer de toepassing op de voorgrond terugkeert en/of de media het spelen hervat.

>[!NOTE]
>
>Het Media Analytics-team heeft gevallen gezien waarin klanten `trackSessionStart` hebben gebeld toen hun app van de achtergrond werd teruggestuurd. Als u dit doet, wordt het afspelen tot dat moment niet meegeteld bij de totale afspeeltijd, en gaan er eerder voortgangsmarkeringen, segmenten enzovoort verloren. Roep in plaats daarvan `trackPlay` aan wanneer de app wordt geretourneerd en/of wanneer de media worden hervat.

## Veelgestelde vragen over het afhandelen van toepassingsonderbrekingen: {#faq-about-handling-application-interrupts}

* _Hoe lang moet een toepassing worden geachtergrondd voordat de sessie wordt gesloten?_

   Als de toepassing het afspelen op de achtergrond toestaat, kan het volgen door onze API&#39;s aan te roepen en sturen we al onze normale &#39;tracking pings&#39;-berichten. Niet veel video-apps staan afspelen op de achtergrond toe, behalve YouTube Red. Dit is echter wel mogelijk voor alle audio-apps. Als het afspelen op de achtergrond niet is toegestaan in de toepassing, is het aan te raden om gedurende één minuut in de pauzestatus te blijven en de volgende sessie te beëindigen. De toepassing kan niet blijven verzenden pingelt van de Pauze, omdat het in de meeste gevallen niet kan bepalen of de gebruiker zal terugkeren om de media te blijven bekijken, of zal bepalen wanneer het zal worden gedood. Het is ook een slechte ervaring om pingelt te blijven verzenden wanneer op de achtergrond.

* _Wat is de juiste manier om het opnieuw opstarten van tracering af te handelen nadat de app al lange tijd op de achtergrond wordt uitgevoerd?_

   De toepassing moet `trackSessionEnd` aanroepen om de volgende sessie te beëindigen. Van Versie 2.1, verzendt SDK &quot;eind&quot;pingelt om het achterste eind mee te delen dat de volgende zitting wordt gesloten.

* _En hoe zit het met het opnieuw opstarten van dezelfde sessie?_

   Zie deze pagina voor gedetailleerde instructies voor het opnieuw starten van een volgende sessie: [Een eerder gesloten sessie handmatig hervatten](/help/sdk-implement/cookbook/resuming-inactive.md). SDK verzendt hervat pingel om het achterste eind mee te delen dat de gebruiker manueel de zitting hervat.
