---
title: Gebeurtenistypen en beschrijvingen voor streaming media
description: "Wat zijn de gebeurtenistypen en de beschrijvingen van de Inzameling van Media? "
uuid: bc4f75a7-ea22-47eb-a50d-5f41274c6d41
exl-id: f2919e69-8b03-45b4-b9cd-365222a061e0
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: d89b2af2e2ae5a170ce98f62656cdeed6fe31f19
workflow-type: tm+mt
source-wordcount: '353'
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

Ping-gebeurtenissen moeten *niet* de `params` kaart in de aanvraaginstantie.

## bitrateChange

Verzonden wanneer de bitrage verandert.

## bufferStart

Verzonden wanneer de buffering begint. Er is geen `bufferResume` gebeurtenistype. A `bufferResume` wordt afgeleid wanneer u een `play` gebeurtenis na `bufferStart`.

## pauseStart

Verzonden wanneer de gebruiker op Pauzeren drukt. Er is geen `resume` gebeurtenistype. A `resume` wordt afgeleid wanneer u een `play` gebeurtenis na een `pauseStart`.

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

Geeft het begin van een hoofdstuksegment aan

## hoofdstukSkip

Geeft aan dat een hoofdstuk wordt overgeslagen

## hoofdstukComplete

Hiermee wordt de voltooiing van een hoofdstuk aangegeven

## fout

Geeft aan dat er een fout is opgetreden.

## sessionEnd

Dit wordt gebruikt om de achtergrond van de Analyse van Media op de hoogte te brengen om de zitting onmiddellijk te sluiten wanneer de gebruiker hun het bekijken van de inhoud heeft verlaten en zij waarschijnlijk niet zullen terugkeren.

Als u geen `sessionEnd`, zal een verlaten zitting tijd-uit normaal (nadat geen gebeurtenissen 10 minuten worden ontvangen, of wanneer geen playhead beweging voor 30 minuten voorkomt), en de zitting wordt geschrapt door het achtereind.

## sessionComplete

Verzonden wanneer het einde van de hoofdinhoud is bereikt

>[!IMPORTANT]
>
>Raadpleeg de [JSON-validatieschema&#39;s](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) voor elk gebeurtenistype, om de correcte types en de vereisten van gebeurtenisparameters te verifiëren.
