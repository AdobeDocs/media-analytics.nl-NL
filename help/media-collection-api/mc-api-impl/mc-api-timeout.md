---
title: Time-outvoorwaarden
description: Leer meer over de time-outvoorwaarden van de API voor streaming Media Collection.
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
exl-id: 0b494b27-a4a6-4af7-84c1-c44b33b6da8f
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 1%

---

# Tijdslimiet{#timeout-conditions}

**Tijdslimiet voor API voor mediaverzameling**

De API voor de verzameling van media heeft, aangezien deze geen status heeft, niet hetzelfde mechanisme als de SDK van Media voor het uitgeven van een nieuwe sessie-id wanneer time-outvoorwaarden zich voordoen. Wanneer een onderbrekingsvoorwaarde voorkomt, zal het achtereind de zitting sluiten, en alle verdere vraag die met die identiteitskaart van de Zitting wordt gemaakt zal worden gelaten vallen. De logica die een Onderbreking van de Zitting behandelt moet in de cliënt worden behandeld. Dit betekent dat de speler de time-outvoorwaarden moet controleren en een nieuwe sessie-id moet verkrijgen als er een time-out optreedt.

* **10 minuten: Geen API-gebeurtenissen**

   Als het achterste einde geen API-gebeurtenissen ontvangt, wordt de sessie gesloten.
* **30 minuten: Geen wijziging van afspeelkop**

   Als de afspeelkop gedurende 30 minuten niet beweegt (de gebruiker tikt bijvoorbeeld op Pauzeren en gaat weg), sluit het achterste einde de sessie.

>[!NOTE]
>
>U kunt een zittingseind ook dwingen door een `events` verzoek met het `sessionEnd` gebeurtenistype te verzenden.
