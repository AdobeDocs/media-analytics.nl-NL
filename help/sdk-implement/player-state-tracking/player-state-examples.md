---
title: Voorbeelden van statussen van speler bijhouden
description: Dit onderwerp omvat voorbeelden van de het Volgen eigenschap van de Staat van de Speler.
translation-type: tm+mt
source-git-commit: 1cf11a6b8971f5be490998bbd855a27bfe366e48
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# Voorbeelden van statussen van speler bijhouden

Voorbeelden toevoegen


## Voorbeeld van lange pauze

Wanneer een videosessie een pauzeduur heeft die langer is dan 30 minuten, vereist de API een nieuwe sessie. Als dit gebeurt, moet de client een nieuwe sessie-id genereren. Voor beide videosessies moet de client alle statussen van een speler behouden en alle informatie als een `stateStart` gebeurtenis direct na de `sessionStart` aanroep verzenden.

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd
`

Nadat de video `sessionEnd` is verzonden, moet een nieuwe videosessie worden gestart en moeten de eerste API-gebeurtenissen:

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

In het lange pauze-voorbeeld wordt getoond dat de speler ook de toestanden opslaat, zodat deze naar de nieuwe videosessie kunnen worden verzonden.
