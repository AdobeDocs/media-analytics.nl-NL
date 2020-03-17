---
title: Tijdslimiet
description: null
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

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

