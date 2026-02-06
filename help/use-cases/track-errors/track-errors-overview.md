---
title: Er zijn fouten bijgehouden
description: Dig dieper in fout het volgen gebruikend Media SDK.
uuid: d71429e6-ef8b-4ea2-8491-ff3cdbf4357f
exl-id: 61c5f835-d66c-4621-a0af-2e4f47a922ac
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 1%

---

# Overzicht{#overview}

De volgende instructies bieden richtlijnen voor implementatie voor alle 2.x SDK&#39;s.

>[!IMPORTANT]
>
>Als u een 1.x versie van SDK uitvoert, kunt u de 1.x Gidsen van Ontwikkelaars hier downloaden: [ Download SDKs.](/help/getting-started/download-sdks.md)

## Foutopsporing implementeren

1. Fouten met mediaspeler bijhouden.

   Bij foutgebeurtenissen roept u `trackError` aan met de foutinformatie.

>[!NOTE]
>
>Fouten bij het bijhouden van mediaspeler stoppen de mediatrackingsessie niet. Als de fout in de mediaspeler voorkomt dat het afspelen wordt voortgezet, controleert u of de mediatrackingsessie is gesloten door `trackSessionEnd` aan te roepen na het aanroepen van `trackError` .
