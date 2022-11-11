---
title: Federated Analytics
description: De Federated Analytics-service biedt een systeem voor het delen van Adobe Analytics voor het streamen van mediagegevens tussen twee partners.
uuid: a82ace81-c2f6-4799-9a62-4c6a737a7dab
exl-id: 81970370-663c-49d5-b13c-628d294be178
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 92%

---

# Federated Analytics{#federated-analytics}

De Federated Analytics-service biedt een systeem voor het delen van Adobe Media Analytics-data (audio en video) tussen twee partners.
De gestandaardiseerde meetdata die door Media Analytics worden gemaakt, zijn het handelsmerk van Federated Analytics, waardoor dezelfde data vanuit meerdere bronnen kunnen worden opgenomen in één rapport.
Door middel van de regels en logica in Federated Analytics worden de data gemakkelijk beheerd en geïndividualiseerd om aan de behoeften van elk partnerschap te voldoen.
Federated Analytics maakt het meten van audio en video efficiënter, gestroomlijnder en uitvoerbaarder.

## Voordelen {#benefits}

* **Transparant:** haal de zwarte doos van datacreatie weg door dezelfde logica in verschillende bedrijven te gebruiken
* **Breed:** krijg inzicht in het volledige bereik en de impact van audio- en videogebruik in verschillende partnerschappen, platforms en apparaten
* **Veilig:** beheer server-side datasharing via regels en logica
* **Gestandaardiseerd:** spreek de zelfde datataal als uw partners
* **Uitvoerbaar:** kwantificeer audio- en videodata om spelers te benchmarken, trends bij te houden en anomalieën te detecteren via Adobe Analytics
* **Gecentraliseerd:** verzamel data voor audio- en videometingen op één Adobe-locatie
* **Contractueel:** voldoe met gemak aan de vereisten voor het delen van juridische data
* **Tijdig:** verzend en ontvang data bijna in real time
* **Eenvoudig:** markeer spelers eenmaal met Adobe SDK&#39;s, deel data met veel partners

## Definities {#definitions}

* **Afzender:** klant genereert audio- en videoanalysedata op eigen spelers
* **Ontvanger:** klant ontvangt audio- en videoanalysedata van afzender

## Vereisten {#requirements}

* **Contract voor mediastreams:** ontvanger en afzender moeten een contract voor Adobe Analytics voor Media Streams hebben voordat ze toegang krijgen tot audio- en videodata in Adobe Analytics. Neem contact op met uw accountteam voor meer informatie.
* **Federated addendum:** zowel afzender als ontvanger moet beschikken over een ondertekend addendum bij Adobe voordat data worden verzonden of ontvangen. Eén addendum per klant is vereist, niet één addendum per partnerschap. Neem contact op met uw accountteam voor meer informatie.

* **Media Analytics-implementatie:** de afzenden moet Media Analytics hebben geïmplementeerd op alle spelers die deel zullen uitmaken van de gefedereerde datareeks. Alleen de data van Media Analytics zijn beschikbaar voor federatie. Zie documentatie: [Streaming media meten in Adobe Analytics](/help/media-overview.md)

* **Adobe Consulting-contract:** voor de eerste instelling van gefedereerde regels tussen ontvanger en afzender is het waardevol om met adviesdiensten te werken voor het beoordelen van data en een datasharingovereenkomst te maken.

## Het Federated Analytics-formulier downloaden

Als u wilt deelnemen aan Federated Analytics, downloadt en voltooit u de [Overeenkomst betreffende federatieregels](assets/federated_analytics_form.pdf) formulier.

## Proces {#process}

1. De afzender en de ontvanger werken samen om het formulier Overeenkomst federatieregels in te vullen. Het formulier Overeenkomst federatieregels bevat speciale velden voor ons engineeringteam en mag ALLEEN worden bewerkt met Adobe Acrobat. [Download Acrobat gratis.](https://get.adobe.com/nl/reader/)
1. Adviesdiensten verstrekken een voorbeelddatabestand aan de ontvanger met daadwerkelijke data van spelers van de afzender om te bevestigen dat de juiste correcte datasharingregels zijn gedefinieerd, op voorwaarde dat er databestanden beschikbaar zijn.
1. Afzender en ontvanger zorgen ervoor dat de overeenkomst voor het delen van data voldoet aan alle contractuele vereisten tussen beide partijen.
1. Consultingservices stuurt het ingevulde formulier naar Adobe Engineering om regels voor het delen van data op te stellen.
1. Data worden opgenomen in de ontwikkelrapportsuite waarin de ontvanger data controleert en valideert.
1. Zodra de ontvanger bevestigt dat de data correct zijn, werkt Adobe Engineering de regels bij zodat deze naar een productierapportsuite verwijzen.
1. De ontvanger zal de data in de productierapportsuite controleren en valideren.
1. Als de veranderingen in de datareeks optreden in de toekomst, kan de afzender of de ontvanger een klantenserviceticket indienen voor ondersteuning.
