---
title: Migratieoverzicht
description: Meer informatie over het migreren van 1.x- naar 2.x-versies van de Media SDK.
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
exl-id: b3b8b9f8-a6e9-4ed1-85c1-80e61460e8a0
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 7%

---

# Overzicht van oudere migratie voor VHL 1.x naar VHL 2.x {#migration-overview}

De migratie van VHL 1.x naar VHL 2.x is eenvoudig, met de nieuwe versie die vereenvoudigde API&#39;s voor initialisatie, configuratie en spelerafgevaardigden.i bevat

Hier volgen de belangrijkste verschillen tussen 1.x en 2.x:

* **Insteekmodules, delegaties -** U hoeft geen plug-ins en afgevaardigden meer te implementeren voor Analytics, VideoPlayer en Heartbone.
* **Configuratie -** U hoeft geen configuraties meer te instantiëren voor de 1.x-plug-ins.

## Voordelen van 2.x {#benefits-of-two-x}

* Alle overheidsmethoden worden geconsolideerd in de `MediaHeartbeat` -klasse om de implementatie voor ontwikkelaars eenvoudiger te maken.
* Alle configuraties zijn nu geconsolideerd in de `MediaHeartbeatConfig` klasse.
* U hoeft geen configuraties meer te instantiëren voor de plug-ins Analytics, VideoPlayer en Heartbone. U hoeft alleen het `MediaHeartbeat` klasse met `MediaHeartbeatDelegate` en `MediaHeartbeatConfig` instanties. Dit is de enige implementatie die nodig is om Media Analytics te initialiseren.

   Met de initialisatie van `MediaHeartbeat`, kunt u veilig alle implementatie voor de Insteekmodule Analytics, Insteekmodule VideoPlayer en insteekmodule Heartbone verwijderen. Verwijder ook alle bestaande implementatie voor initialisatie die een array van plug-ins als invoer nodig heeft. Hier kunt u vergelijkingen naast elkaar zien van de 1.x- en 2.x-implementaties: [Codevergelijking: 1.x tot 2.x.](./code-comparison-1x-2x.md)

De nieuwe API&#39;s in 2.x worden uitgebreid beschreven in: [Conversie van API 1.x naar 2.x](./1x-2x-api-change.md).
