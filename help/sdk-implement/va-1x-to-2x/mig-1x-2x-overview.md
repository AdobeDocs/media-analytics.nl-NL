---
title: Migratieoverzicht
description: Dit onderwerp verstrekt een overzicht van het migreren van 1.x aan 2.x versies van Media SDK.
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Migratieoverzicht{#migration-overview}

De migratie van VHL 1.x naar VHL 2.x is eenvoudig, met de nieuwe versie die vereenvoudigde APIs voor initialisering, configuratie, en spelerafgevaardigden kenmerkt.

Hier volgen de belangrijkste verschillen tussen 1.x en 2.x:

* **Plugins, Delegates -** U hoeft geen plug-ins en afgevaardigden meer te implementeren voor Analytics, VideoPlayer en Heartbone.
* **Configuratie -** U hoeft geen configuraties meer te instantiëren voor de 1.x plug-ins.

## Voordelen van 2.x {#benefits-of-two-x}

* Alle openbare methodes worden geconsolideerd in de `MediaHeartbeat` klasse om implementatie voor ontwikkelaars gemakkelijker te maken.
* Alle configuraties worden nu geconsolideerd in de `MediaHeartbeatConfig` klasse.
* U hoeft geen configuraties meer te instantiëren voor de plug-ins Analytics, VideoPlayer en Heartbone. U hoeft de `MediaHeartbeat` klasse alleen met `MediaHeartbeatDelegate` en `MediaHeartbeatConfig` instanties te instantiëren. Dit is de enige implementatie die nodig is om Media Analytics te initialiseren.

   Met initialisatie van `MediaHeartbeat`, kunt u alle implementatie voor Insteekmodule Analytics, Insteekmodule VideoPlayer, en Insteekmodule Heartbeat veilig schrappen. Verwijder ook alle bestaande implementatie voor initialisatie die een array van plug-ins als invoer nodig heeft. Hier kunt u vergelijkingen naast elkaar zien van de 1.x- en 2.x-implementaties: [Codevergelijking: 1.x tot 2.x.](./code-comparison-1x-2x.md)

De nieuwe API&#39;s in 2.x worden uitgebreid beschreven in: [Conversie van API 1.x naar 2.x](./1x-2x-api-change.md).
