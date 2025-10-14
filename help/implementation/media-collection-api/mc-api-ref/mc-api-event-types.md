---
title: Gebeurtenistypen en beschrijvingen voor streaming media
description: 'Wat zijn de gebeurtenistypen en beschrijvingen van de Inzameling van Media? '
uuid: bc4f75a7-ea22-47eb-a50d-5f41274c6d41
exl-id: f2919e69-8b03-45b4-b9cd-365222a061e0
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 0%

---

# Gebeurtenistypen en beschrijvingen{#event-types-and-descriptions}

## sessionStart

Verzonden met de aanroep van `sessions` . Wanneer de reactie terugkeert, haalt u identiteitskaart van de Zitting uit de kopbal van de Plaats en gebruikt het voor verdere gebeurtenisvraag aan de server van de Inzameling.

## play

Verzonden wanneer de status van de speler verandert in &#39;play&#39; (de callback van `on('Playing')` wordt dus geactiveerd door de speler). Andere toestanden waarvan de speler overgaat naar &#39;&#39;afspelen&#39;&#39; zijn &#39;&#39;bufferen&#39;&#39;, de gebruiker hervat van &#39;&#39;gepauzeerd&#39;&#39;, de speler hersteld van een fout, automatisch afspelen, enzovoort.

## pingelen

* **Belangrijkste Inhoud -** moet om de 10 seconden tijdens belangrijkste inhoudsplayback, ongeacht andere API gebeurtenissen worden verzonden die zijn verzonden. De eerste pingel gebeurtenis zou 10 seconden moeten in brand steken nadat de belangrijkste inhoud is begonnen te spelen.
* **Advertentie Inhoud -** moet om de 1 seconde tijdens het volgen van advertenties worden verzonden.

Pingel gebeurtenissen ** niet `params` kaart in het verzoeklichaam zouden moeten omvatten.

## bitrateChange

Verzonden wanneer de bitrage verandert.

## bufferStart

Verzonden wanneer de buffering begint. Er is geen gebeurtenistype `bufferResume` . Een `bufferResume` wordt afgeleid wanneer u een `play` gebeurtenis na `bufferStart` verzendt.

## pauseStart

Verzonden wanneer de gebruiker op Pauzeren drukt. Er is geen gebeurtenistype `resume` . Een `resume` wordt afgeleid wanneer u een `play` -gebeurtenis na een `pauseStart` -gebeurtenis verzendt.

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

Als a `sessionEnd` niet wordt verzonden, zal een verlaten zitting [&#x200B; tijd-uit normaal &#x200B;](../mc-api-impl/mc-api-timeout.md) (of nadat geen gebeurtenissen voor 10 minuten worden ontvangen, of wanneer geen playhead beweging voor 30 minuten voorkomt). Bovendien, zullen alle verdere Vraag van Media die met die Zitting ID wordt gemaakt worden gelaten vallen.

## sessionComplete

Verzonden wanneer het einde van de hoofdinhoud is bereikt

>[!IMPORTANT]
>
>U zou naar de [&#x200B; JSON bevestigingsschema&#39;s &#x200B;](mc-api-json-validation.md) voor elk gebeurtenistype moeten verwijzen, om de correcte types en de vereisten van de gebeurtenisparameter te verifiëren.

## stateStart

Geeft het begin van bijhouden van spelerstatus aan.

Voor meer informatie, zie [&#x200B; Implementatie en het melden &#x200B;](/help/use-cases/player-state-tracking/implementation-and-reporting.md).

## stateEnd

Geeft het einde van de status tracking van de speler aan.

Voor meer informatie, zie [&#x200B; Implementatie en het melden &#x200B;](/help/use-cases/player-state-tracking/implementation-and-reporting.md).
