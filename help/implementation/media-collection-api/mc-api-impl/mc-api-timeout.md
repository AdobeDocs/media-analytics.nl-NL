---
title: Tijdslimiet
description: Meer informatie over de time-outvoorwaarden van de Media Collection API.
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
exl-id: 0b494b27-a4a6-4af7-84c1-c44b33b6da8f
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# Tijdslimiet{#timeout-conditions}

**Voorwaarden van de Onderbreking van de Inzameling van Media API**

De Media Collection API, die stateless is, heeft niet het zelfde mechanisme als Media SDK voor het uitgeven van een nieuwe identiteitskaart van de Zitting wanneer onderbrekingsvoorwaarden voorkomen. Wanneer een onderbrekingsvoorwaarde voorkomt, zal het achtereind de zitting sluiten, en alle verdere vraag die met die identiteitskaart van de Zitting wordt gemaakt zal worden gelaten vallen. De logica die een Onderbreking van de Zitting behandelt moet in de cliënt worden behandeld. Dit betekent dat de speler de time-outvoorwaarden moet controleren en een nieuwe sessie-id moet verkrijgen als er een time-out optreedt.

* **10 notulen: Geen API Gebeurtenissen**

  Als het achterste einde geen API-gebeurtenissen ontvangt, wordt de sessie gesloten.
* **30 notulen: Geen Verandering Playhead**

  Als de afspeelkop gedurende 30 minuten niet beweegt (de gebruiker tikt bijvoorbeeld op Pauzeren en gaat weg), sluit het achterste einde de sessie.

>[!NOTE]
>
>U kunt het beëindigen van een sessie ook afdwingen door een `events` -aanvraag met het gebeurtenistype `sessionEnd` te verzenden.
