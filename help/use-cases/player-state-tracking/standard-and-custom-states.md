---
title: Over Standaard- en Aangepaste statussen
description: Leer meer over de functie voor het bijhouden van spelerstatussen, zoals vereisten en richtlijnen voor het implementeren en rapporteren van standaard- en aangepaste spelerstatussen.
exl-id: 3c492055-d471-4147-aa78-b058d6b931f4
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Informatie over standaard- en aangepaste statussen

Er zijn vijf standaardspelerstatussen beschikbaar en u kunt uw eigen aangepaste statussen toevoegen.

| Standaardstatusnaam | Media SDK-constante | API-naam van mediagroep |
|-----------------------|------------------------------------------|-----------------------------|
| Volledig scherm | `ADB.Media.PlayerState.Fullscreen` | `fullScreen` |
| Ondertiteling | `ADB.Media.PlayerState.ClosedCaptioning` | `closedCaptioning` |
| Dempen | `ADB.Media.PlayerState.Mute` | `mute` |
| Foto in beeld | `ADB.Media.PlayerState.PictureInPicture` | `pictureInPicture` |
| In focus | `ADB.Media.PlayerState.InFocus` | `inFocus` |

De gegevens worden op dezelfde manier berekend voor standaard- en aangepaste statussen, maar de gegevens worden anders opgeslagen voor analytische rapportage.

**voor standaardstaten** - wanneer u het volgen van de spelerstaat van de console van het Beheer van Media in Analytics het melden (admin kant) toelaat, zijn 15 oplossingsvariabelen beschikbaar voor het melden en gegevensuitvoer.

**voor douanestaten** - u kunt uw eigen verwerkingsregels tot stand brengen om de gegevens verwerkte waarden in douanegebeurtenissen op te slaan en dan die regels voor het melden van en gegevensuitvoer te gebruiken.

## Richtsnoeren

* Eén videosessie is beperkt tot tien spelerstatussen.
* Elke combinatie van frames is toegestaan.
* Wanneer meerdere spelerstatussen slagen, worden alleen de eerste 10 behouden en naar de VA-verwerkingscomponent doorgestuurd.
* Het maximum van tien staten geldt voor alle staten, ongeacht of ze gesloten zijn of niet.
* Een status kan meerdere keren beginnen en eindigen en wordt als één status geteld. `closedCapationing` kan bijvoorbeeld vijf keer worden gestart en gestopt, maar het telt als één frame.
* Elke staat die het maximum van 10 toegestane staten overschrijdt wordt verworpen.

## Aangepaste statussen

Met de mogelijkheid om aangepaste statussen te maken, kunt u aangepaste handelingen vastleggen en aangepaste metagegevens bijwerken tijdens een afspeelsessie.

Voor informatie over het creëren van douanestaten, zie de [ gids van de Verwijzing van Media API: `createStateObject` ](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/)
