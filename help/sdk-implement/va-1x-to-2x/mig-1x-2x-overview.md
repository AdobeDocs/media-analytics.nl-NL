---
title: Migratieoverzicht
description: Meer informatie over het migreren van 1.x- naar 2.x-versies van de Media SDK.
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
exl-id: b3b8b9f8-a6e9-4ed1-85c1-80e61460e8a0
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 8%

---

# Migratieoverzicht{#migration-overview}

De migratie van VHL 1.x naar VHL 2.x is eenvoudig, met de nieuwe versie die vereenvoudigde APIs voor initialisering, configuratie, en spelerafgevaardigden kenmerkt.

Hier volgen de belangrijkste verschillen tussen 1.x en 2.x:

* **Plugins, Delegates -** u hoeft geen plug-ins en afgevaardigden meer te implementeren voor Analytics, VideoPlayer en Heartbone.
* **Configuratie -** u hoeft geen configuraties meer te instantiëren voor de 1.x plug-ins.

## Voordelen van 2.x {#benefits-of-two-x}

* Alle openbare methodes worden geconsolideerd in de `MediaHeartbeat` klasse om implementatie voor ontwikkelaars gemakkelijker te maken.
* Alle configuraties worden nu geconsolideerd in de klasse `MediaHeartbeatConfig`.
* U hoeft geen configuraties meer te instantiëren voor de plug-ins Analytics, VideoPlayer en Heartbone. U hoeft de klasse `MediaHeartbeat` alleen te instantiëren met instanties `MediaHeartbeatDelegate` en `MediaHeartbeatConfig`. Dit is de enige implementatie die nodig is om Media Analytics te initialiseren.

   Met de initialisatie van `MediaHeartbeat`, kunt u alle implementatie voor de Insteekmodule Analytics, Insteekmodule VideoPlayer, en de Insteekmodule van de Hartslag veilig schrappen. Verwijder ook alle bestaande implementatie voor initialisatie die een array van plug-ins als invoer nodig heeft. Hier kunt u vergelijkingen naast elkaar zien van de 1.x- en 2.x-implementaties: [Codevergelijking: 1.x tot 2.x.](./code-comparison-1x-2x.md)

De nieuwe API&#39;s in 2.x worden uitgebreid beschreven in: [Conversie van API 1.x naar 2.x](./1x-2x-api-change.md).
