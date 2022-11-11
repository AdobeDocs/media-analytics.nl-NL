---
title: Voorbeelden van statussen van speler bijhouden
description: Dit onderwerp omvat voorbeelden van de het Volgen eigenschap van de Staat van de Speler.
exl-id: a77bc882-ac03-40b4-ac64-87f26a09707b
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# Voorbeelden van statussen van speler bijhouden


## Voorbeeld van lange pauze

Wanneer een videosessie een pauzeduur heeft die langer is dan 30 minuten, vereist de API een nieuwe sessie. Als dit gebeurt, moet de client een nieuwe sessie-id genereren. Voor beide videosessies moet de client alle statussen van een speler behouden en alle informatie als een `stateStart` gebeurtenis net na de `sessionStart` vraag.

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd`

Na de `sessionEnd` wordt verzonden, moet een nieuwe videozitting beginnen en de eerste API gebeurtenissen zouden zijn:

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

In het lange pauze-voorbeeld wordt getoond dat de speler ook de toestanden opslaat, zodat deze naar de nieuwe videosessie kunnen worden verzonden.
