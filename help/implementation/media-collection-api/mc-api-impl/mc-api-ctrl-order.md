---
title: De volgorde van gebeurtenissen bepalen
description: Leer hoe u de volgorde van gebeurtenissen regelt en hoe gebeurtenissen in sommige gevallen opnieuw worden geordend op basis van de opgegeven tijdstempel in het PlayerTime-object.
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 1%

---

# De volgorde van gebeurtenissen bepalen{#controlling-the-order-of-events}

Het stromen video het volgen is een hoogst tijd-afhankelijke verrichting en soms komen de het volgen vraag van API van de Inzameling van Media bij het achtereind uit-van-orde aan. In deze situatie probeert het back-end gebeurtenissen in de wachtrij te plaatsen en opnieuw te ordenen op basis van de opgegeven tijdstempel in het dialoogvenster `playerTime` object.  Dit gebeurt met enkele limieten. Momenteel, kan reorder ontbreken als de vertragingen tussen uit-van-orde vraag meer dan één seconde zijn. In toekomstige updates kan de &quot;aanvaardbare vertragingstijd&quot; geoptimaliseerd en configureerbaar zijn.

## Voorbeeld van een out-of-order-gebeurtenis

Gebeurtenissen buiten de volgorde treden op wanneer gebeurtenissen door het netwerk gaan, wat soms een vertraging veroorzaakt.

U kunt bijvoorbeeld een `adBreakStart` gebeurtenis gevolgd door een `adStart` gebeurtenis. Dit is een gebruikscase, omdat een advertentie moet beginnen in een advertentie-einde.

Als de advertentie gereed is en er geen buffer nodig is, vinden beide gebeurtenissen bijna onmiddellijk plaats en wordt de `playerTime.ts` voor beide gebeurtenissen zeer dicht bij elkaar zijn - maar zij zouden nooit gelijk moeten zijn.

> &#39;playerTime.ts&#39; van gebeurtenissen mag nooit gelijk zijn voor een gebeurtenis, omdat het sorteeralgoritme niet weet welke gebeurtenis het eerst heeft plaatsgevonden. Er moet een tijdstempelverschil van minstens 1 milliseconde zijn voor elke 2 opeenvolgende gebeurtenissen.

Omdat beide gebeurtenissen zeer dicht bij elkaar in tijd wanneer het ontsteken van netwerkvraag voorkomen, is het mogelijk dat zij uit orde aankomen. In dit voorbeeld wordt `adStart` gebeurtenis aankomt vóór de gebeurtenis `adBreakStart` gebeurtenis.


Er is een getimed venster met gebeurtenissen: 5 seconden of maximaal 10 gebeurtenissen. De gebeurtenissen zijn als buffer opgetreden voor alvorens hen naar de verwerkingspijpleiding te verzenden. Wanneer aan de voorwaarden voldaan is - 5 seconden zijn overgegaan of meer dan 10 gebeurtenissen worden ontvangen, worden de gebeurtenissen opnieuw geordend gebaseerd op `playerTime.ts` en dan verzonden in de nieuwe orde, naar de verwerkingspijpleiding.

>[!IMPORTANT]
>
>Er is een uitzonderingsgebeurtenis die onmiddellijk naar de verwerkingspijpleiding wordt verzonden en dat is `sessionStart` gebeurtenis.
