---
title: De volgorde van gebeurtenissen bepalen
description: De volgorde van gebeurtenissen bepalen
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
translation-type: tm+mt
source-git-commit: e0da35f364dc057a241fbb05a718a731ffee1e94
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# De volgorde van gebeurtenissen bepalen{#controlling-the-order-of-events}

Het stromen video het volgen is een hoogst tijd-afhankelijke verrichting en soms komen de het volgen vraag van API van de Inzameling van Media bij het achtereind uit-van-orde aan. In deze situatie, probeert het achtereind om gebeurtenissen op verstrekte timestamp in het `playerTime` voorwerp op rij te plaatsen en opnieuw te rangschikken.  Dit gebeurt met enkele limieten. Momenteel, kan reorder ontbreken als de vertragingen tussen uit-van-orde vraag meer dan één seconde zijn. In toekomstige updates kan de &quot;aanvaardbare vertragingstijd&quot; geoptimaliseerd en configureerbaar zijn.

## Voorbeeld van een out-of-order-gebeurtenis
Gebeurtenissen buiten de volgorde treden op wanneer gebeurtenissen door het netwerk gaan, wat soms een vertraging veroorzaakt.

U kunt bijvoorbeeld een gebeurtenis `adBreakStart` verzenden, gevolgd door een gebeurtenis `adStart`. Dit is een gebruikscase, omdat een advertentie moet beginnen in een advertentie-einde.

Als de advertentie klaar is en geen buffer nodig is, komen beide gebeurtenissen bijna onmiddellijk voor en `playerTime.ts` voor beide gebeurtenissen zijn zeer dicht aan elkaar-maar zij zouden nooit gelijk moeten zijn.

> &#39;playerTime.ts&#39; van gebeurtenissen mag nooit gelijk zijn voor een gebeurtenis, omdat het sorteeralgoritme niet weet welke gebeurtenis het eerst heeft plaatsgevonden. Er moet een tijdstempelverschil van minstens 1 milliseconde zijn voor elke 2 opeenvolgende gebeurtenissen.

Omdat beide gebeurtenissen zeer dicht bij elkaar in tijd wanneer het ontsteken van netwerkvraag voorkomen, is het mogelijk dat zij uit orde aankomen. In dit voorbeeld komt de gebeurtenis `adStart` voor de gebeurtenis `adBreakStart`.


Er is een getimed venster met gebeurtenissen: 5 seconden of maximaal 10 gebeurtenissen. De gebeurtenissen zijn als buffer opgetreden voor alvorens hen naar de verwerkingspijpleiding te verzenden. Wanneer de voorwaarden worden voldaan-5 seconden overgegaan of meer dan 10 gebeurtenissen ontvangen zijn, worden de gebeurtenissen opnieuw geordend gebaseerd op `playerTime.ts` en dan verzonden in de nieuwe orde, naar de verwerkingspijpleiding.

>[!IMPORTANT]
>
>Er is een uitzonderingsgebeurtenis die onmiddellijk naar de verwerkingspijpleiding wordt verzonden en dat is de gebeurtenis `sessionStart`.
