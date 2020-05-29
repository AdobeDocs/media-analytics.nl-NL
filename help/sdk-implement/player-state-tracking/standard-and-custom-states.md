---
title: Over Standaard- en Aangepaste statussen
description: In dit onderwerp wordt de functie voor het bijhouden van de spelerstatus beschreven, inclusief vereisten en richtlijnen voor het implementeren en rapporteren van standaard- en aangepaste spelerstatussen.
translation-type: tm+mt
source-git-commit: f7a45dfbabe71fa9e1de7a4f4b2a7e64849e4ef4
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---


# Informatie over standaard- en aangepaste frames

Er zijn vijf standaardspelerstatussen beschikbaar en u kunt uw eigen aangepaste statussen toevoegen.

| Standaardstatusnaam | Media SDK-constante | API-naam van mediagroep |
|-----------------------|------------------------------------------|-----------------------------|
| Volledig scherm | `ADB.Media.PlayerState.Fullscreen` | `fullScreen` |
| Ondertiteling | `ADB.Media.PlayerState.ClosedCaptioning` | `closedCaptioning` |
| Dempen | `ADB.Media.PlayerState.Mute` | `mute` |
| Beeld-in-beeld | `ADB.Media.PlayerState.PictureInPicture` | `pictureInPicture` |
| In focus | `ADB.Media.PlayerState.InFocus` | `inFocus` |

De gegevens worden op dezelfde manier berekend voor standaard- en aangepaste statussen, maar de gegevens worden anders opgeslagen voor analytische rapportage.

**Voor standaard status**-wanneer u het volgen van de spelerstaat van de console van het Beheer van Media in Analytics rapportering (admin kant) toelaat, zijn 15 oplossingsvariabelen beschikbaar voor rapportering en gegevensuitvoer.

**Voor douanestatus**-u kunt uw eigen verwerkingsregels tot stand brengen om de gegevens verwerkte waarden in douanegebeurtenissen op te slaan en dan die regels voor rapportering en gegevensuitvoer te gebruiken.

## Richtsnoeren

* Eén videosessie is beperkt tot tien spelerstatussen.
* Elke combinatie van frames is toegestaan.
* Wanneer meerdere spelerstatussen slagen, worden alleen de eerste 10 behouden en naar de VA-verwerkingscomponent doorgestuurd.
* Het maximum van tien staten geldt voor alle staten, ongeacht of ze gesloten zijn of niet.
* Een status kan meerdere keren beginnen en eindigen en wordt als één status geteld. U kunt bijvoorbeeld `closedCapationing` vijf keer beginnen en stoppen, maar het telt als één frame.
* Elke staat die het maximum van 10 toegestane staten overschrijdt wordt verworpen.

## Aangepaste statussen

Met de mogelijkheid om aangepaste statussen te maken, kunt u aangepaste handelingen vastleggen en aangepaste metagegevens bijwerken tijdens een afspeelsessie.

Zie de handleiding [Media API Reference voor informatie over het maken van aangepaste statussen: `createStateObject`](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
