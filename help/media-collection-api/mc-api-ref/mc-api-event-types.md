---
title: Gebeurtenistypen en beschrijvingen
description: null
uuid: bc4f75a7-ea22-47eb-a50d-5f41274c6d41
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Gebeurtenistypen en beschrijvingen{#event-types-and-descriptions}

## sessionStart

Verzonden met de `sessions` vraag. Wanneer de reactie terugkeert, haalt u identiteitskaart van de Zitting uit de kopbal van de Plaats en gebruikt het voor verdere gebeurtenisvraag aan de server van de Inzameling.

## play

Verzonden wanneer de status van de speler verandert in &quot;afspelen&quot; in een andere status (de `on('Playing')` callback wordt dus geactiveerd door de speler). Andere toestanden waarvan de speler overgaat naar &#39;&#39;afspelen&#39;&#39; zijn &#39;&#39;bufferen&#39;&#39;, de gebruiker hervat van &#39;&#39;gepauzeerd&#39;&#39;, de speler hersteld van een fout, automatisch afspelen, enzovoort.

## pingelen

* **Hoofdinhoud -** Moet elke 10 seconden worden verzonden tijdens het afspelen van de hoofdinhoud, ongeacht andere API-gebeurtenissen die zijn verzonden. De eerste pingel gebeurtenis zou 10 seconden moeten in brand steken nadat de belangrijkste inhoud is begonnen te spelen.
* **Advertentie -** Moet om de 1 seconde worden verzonden tijdens het bijhouden van advertenties.

Pingel gebeurtenissen zouden *niet* de `params` kaart in het verzoeklichaam moeten omvatten.

## bitrateChange

Verzonden wanneer de bitrage verandert.

## bufferStart

Verzonden wanneer de buffering begint. Er is geen `bufferResume` gebeurtenistype. Een `bufferResume` resultaat wordt afgeleid wanneer u een `play` gebeurtenis na verzendt `bufferStart`.

## pauseStart

Verzonden wanneer de gebruiker op Pauzeren drukt. Er is geen `resume` gebeurtenistype. Een `resume` resultaat wordt afgeleid wanneer u een `play` gebeurtenis na een `pauseStart`.

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

Als u geen `sessionEnd`verzendt, zal een verlaten zitting onderbreking normaal (nadat geen gebeurtenissen 10 minuten worden ontvangen, of wanneer geen playhead beweging voor 30 minuten voorkomt), en de zitting wordt geschrapt door het achtereind.

## sessionComplete

Verzonden wanneer het einde van de hoofdinhoud is bereikt

>[!IMPORTANT]
>
>Raadpleeg de [JSON-validatieschema&#39;s](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) voor elk gebeurtenistype om de juiste typen gebeurtenisparameters en vereisten te controleren.

