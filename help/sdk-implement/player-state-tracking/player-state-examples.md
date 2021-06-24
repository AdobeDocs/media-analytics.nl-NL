---
title: Voorbeelden van statussen van speler bijhouden
description: Dit onderwerp omvat voorbeelden van de het Volgen eigenschap van de Staat van de Speler.
exl-id: a77bc882-ac03-40b4-ac64-87f26a09707b
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: 8a421ee4ee5d2e61126fc6ac8f10f326427e78a7
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# Voorbeelden van statussen van speler bijhouden


## Voorbeeld van lange pauze

Wanneer een videosessie een pauzeduur heeft die langer is dan 30 minuten, vereist de API een nieuwe sessie. Als dit gebeurt, moet de client een nieuwe sessie-id genereren. Voor beide videosessies moet de client alle statussen van een speler behouden en alle informatie als een `stateStart`-gebeurtenis direct na de `sessionStart`-aanroep verzenden.

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd`

Nadat `sessionEnd` is verzonden, moet een nieuwe videosessie worden gestart en de eerste API-gebeurtenissen zijn:

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

In het lange pauze-voorbeeld wordt getoond dat de speler ook de toestanden opslaat, zodat deze naar de nieuwe videosessie kunnen worden verzonden.
