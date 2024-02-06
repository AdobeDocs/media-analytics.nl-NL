---
title: Gebeurtenistypen en beschrijvingen voor streaming media
description: "Wat zijn de gebeurtenistypen en de beschrijvingen van de Inzameling van Media? "
uuid: bc4f75a7-ea22-47eb-a50d-5f41274c6d41
exl-id: f2919e69-8b03-45b4-b9cd-365222a061e0
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 06f24e828fb7795d55599ea1fa7913182dd357e6
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# Gebeurtenistypen en beschrijvingen{#event-types-and-descriptions}

## sessionStart

Verzonden met de `sessions` vraag. Wanneer de reactie terugkeert, haalt u identiteitskaart van de Zitting uit de kopbal van de Plaats en gebruikt het voor verdere gebeurtenisvraag aan de server van de Inzameling.

## play

Verzonden wanneer de status van de speler verandert in &quot;afspelen&quot; in een andere status (dus de `on('Playing')` callback wordt geactiveerd door de speler). Andere toestanden waarvan de speler overgaat naar &#39;&#39;afspelen&#39;&#39; zijn &#39;&#39;bufferen&#39;&#39;, de gebruiker hervat van &#39;&#39;gepauzeerd&#39;&#39;, de speler hersteld van een fout, automatisch afspelen, enzovoort.

## pingelen

* **Hoofdinhoud -** Moet om de 10 seconden worden verzonden tijdens het afspelen van de hoofdinhoud, ongeacht andere API-gebeurtenissen die zijn verzonden. De eerste pingel gebeurtenis zou 10 seconden moeten in brand steken nadat de belangrijkste inhoud is begonnen te spelen.
* **Inhoud advertentie -** Moet elke 1 seconde worden verzonden tijdens het bijhouden van advertenties.

Ping-gebeurtenissen moeten *niet* inclusief de `params` kaart in de aanvraaginstantie.

## bitrateChange

Verzonden wanneer de bitrage verandert.

## bufferStart

Verzonden wanneer de buffering begint. Er is `bufferResume` gebeurtenistype. A `bufferResume` wordt afgeleid wanneer u een `play` gebeurtenis na `bufferStart`.

## pauseStart

Verzonden wanneer de gebruiker op Pauzeren drukt. Er is `resume` gebeurtenistype. A `resume` wordt afgeleid wanneer u een `play` gebeurtenis na een `pauseStart`.

## adBreakStart

Geeft het begin van een advertentie-einde aan.

## adStart

Geeft het begin van een advertentie aan

## adComplete

Geeft aan dat een advertentie-einde is voltooid

## adSkip

Geeft een advertentie aan en slaat deze over

## adBreakComplete

Geeft aan dat een advertentie-einde is voltooid

## hoofdstukStart

Geeft het begin van een hoofdstuksegment aan.

## hoofdstukSkip

Geeft aan dat een hoofdstuk wordt overgeslagen

## hoofdstukComplete

Hiermee wordt de voltooiing van een hoofdstuk aangegeven

## fout

Geeft aan dat er een fout is opgetreden.

## sessionEnd

Dit wordt gebruikt om de achtergrond van de Analyse van Media op de hoogte te brengen om de zitting onmiddellijk te sluiten wanneer de gebruiker hun het bekijken van de inhoud heeft verlaten en zij waarschijnlijk niet zullen terugkeren.

Indien een `sessionEnd` wordt niet verzonden, wordt een verlaten zitting [time-out, normaal](../mc-api-impl/mc-api-timeout.md) (ofwel nadat er gedurende 10 minuten geen gebeurtenissen zijn ontvangen, of wanneer er gedurende 30 minuten geen beweging van de afspeelkop plaatsvindt). Bovendien, zullen alle verdere Vraag van Media die met die Zitting ID wordt gemaakt worden gelaten vallen.

## sessionComplete

Verzonden wanneer het einde van de hoofdinhoud is bereikt

>[!IMPORTANT]
>
>U moet de [JSON-validatieschema&#39;s](mc-api-json-validation.md) voor elk gebeurtenistype, om de correcte types en de vereisten van gebeurtenisparameters te verifiëren.
