---
title: Gebeurtenistypen en beschrijvingen voor streaming media
description: '"Wat zijn de gebeurtenistypen en de beschrijvingen van de Inzameling van Media? "'
uuid: bc4f75a7-ea22-47eb-a50d-5f41274c6d41
exl-id: f2919e69-8b03-45b4-b9cd-365222a061e0
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---

# Gebeurtenistypen en beschrijvingen{#event-types-and-descriptions}

## sessionStart

Verzonden met de `sessions` vraag. Wanneer de reactie terugkeert, haalt u identiteitskaart van de Zitting uit de kopbal van de Plaats en gebruikt het voor verdere gebeurtenisvraag aan de server van de Inzameling.

## play

Verzonden wanneer de status van de speler verandert in &#39;playing&#39; (de callback wordt dan geactiveerd door de speler). `on('Playing')` Andere toestanden waarvan de speler overgaat naar &#39;&#39;afspelen&#39;&#39; zijn &#39;&#39;bufferen&#39;&#39;, de gebruiker hervat van &#39;&#39;gepauzeerd&#39;&#39;, de speler hersteld van een fout, automatisch afspelen, enzovoort.

## pingelen

* **De belangrijkste Inhoud -** moet om de 10 seconden tijdens het spelen van de belangrijkste inhoud, ongeacht andere API gebeurtenissen worden verzonden die zijn verzonden. De eerste pingel gebeurtenis zou 10 seconden moeten in brand steken nadat de belangrijkste inhoud is begonnen te spelen.
* **Inhoud toevoegen -** moet elke seconde worden verzonden tijdens het bijhouden van advertenties.

Pingel gebeurtenissen *not* zou `params` kaart in het verzoeklichaam moeten omvatten.

## bitrateChange

Verzonden wanneer de bitrage verandert.

## bufferStart

Verzonden wanneer de buffering begint. Er is geen `bufferResume` gebeurtenistype. Een `bufferResume` wordt afgeleid wanneer u een `play` gebeurtenis na `bufferStart` verzendt.

## pauseStart

Verzonden wanneer de gebruiker op Pauzeren drukt. Er is geen `resume` gebeurtenistype. Een `resume` wordt afgeleid wanneer u een `play` gebeurtenis na `pauseStart` verzendt.

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

Als u geen `sessionEnd` verzendt, zal een verlaten zitting uit normaal (nadat geen gebeurtenissen 10 minuten worden ontvangen, of wanneer geen playhead beweging voor 30 minuten voorkomt), en de zitting wordt geschrapt door het achtereind.

## sessionComplete

Verzonden wanneer het einde van de hoofdinhoud is bereikt

>[!IMPORTANT]
>
>Raadpleeg de [JSON-validatieschema&#39;s](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) voor elk gebeurtenistype om de juiste typen en vereisten voor gebeurtenisparameters te controleren.
