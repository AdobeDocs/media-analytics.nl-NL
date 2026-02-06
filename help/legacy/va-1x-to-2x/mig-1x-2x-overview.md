---
title: Migratieoverzicht
description: Meer informatie over het migreren van 1.x- naar 2.x-versies van Media SDK.
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
exl-id: b3b8b9f8-a6e9-4ed1-85c1-80e61460e8a0
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 6%

---

# Overzicht van oudere migratie voor VHL 1.x naar VHL 2.x {#migration-overview}

De migratie van VHL 1.x naar VHL 2.x is eenvoudig, met de nieuwe versie die vereenvoudigde API&#39;s voor initialisatie, configuratie en spelerafgevaardigden.i bevat

Hier volgen de belangrijkste verschillen tussen 1.x en 2.x:

* **Insteekmodules, Afgevaardigden -** u te hoeven niet meer om insteekmodules en afgevaardigden voor Analytics, VideoPlayer, en Hartslag uit te voeren.
* **Configuratie -** u hoeft niet meer configuraties voor de 1.x plug-ins te concretiseren.

## Voordelen van 2.x {#benefits-of-two-x}

* Alle methoden van het type public worden geconsolideerd in de klasse `MediaHeartbeat` om de implementatie voor ontwikkelaars te vereenvoudigen.
* Alle configuraties worden nu geconsolideerd in de `MediaHeartbeatConfig` -klasse.
* U hoeft geen configuraties meer te instantiëren voor de plug-ins Analytics, VideoPlayer en Heartbone. U hoeft de `MediaHeartbeat` -klasse alleen te instantiëren met `MediaHeartbeatDelegate` - en `MediaHeartbeatConfig` -instanties. Dit is de enige implementatie die nodig is om Media Analytics te initialiseren.

  Met de initialisatie van `MediaHeartbeat` kunt u veilig alle implementatie voor Analytics Plugin, VideoPlayer Plugin, en de Insteekmodule van de Hartslag schrappen. Verwijder ook alle bestaande implementatie voor initialisatie die een array van plug-ins als invoer nodig heeft. U kunt zij aan zij vergelijkingen van de 1.x en 2.x implementaties hier zien: [&#x200B; vergelijking van de Code: 1.x aan 2.x.](./code-comparison-1x-2x.md)

De nieuwe API&#39;s in 2.x worden uitgebreid beschreven in: [Conversie van API 1.x naar 2.x](./1x-2x-api-change.md).
