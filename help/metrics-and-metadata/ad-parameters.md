---
title: Parameters voor advertenties
description: "Leer over advertentieparameters met inbegrip van de implementatie, het netwerk, en het melden van variabelen voor ad videogegevens."
uuid: 92cd7f97-bb5a-4de6-8946-453d30271d0f
exl-id: 949e86cb-d265-4836-8825-a06b87203b15
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 7e5ce452a9c96c4e34150ae0e06d73b0cff98741
workflow-type: tm+mt
source-wordcount: '2100'
ht-degree: 3%

---

# Parameters voor advertenties{#ad-parameters}

Dit onderwerp stelt een lijst van video en gegevens, met inbegrip van de waarden van contextgegevens voor, die Adobe via oplossingsvariabelen verzamelt.

Beschrijving van tabelgegevens:

* **Implementatie:** Informatie over implementatiewaarden en -vereisten
   * *Sleutel* - Variabele, stelt u handmatig in in uw app of automatisch in door de SDK van Adobe Media.
   * *Vereist* - Geeft aan of de parameter vereist is voor het bijhouden van basisvideo.
   * *Type* - Geeft het type aan van de variabele die moet worden ingesteld, de tekenreeks of het getal.
   * *Verzonden met* - Geeft aan wanneer de gegevens worden verzonden: *Start media* de analytische oproep die bij het starten van de media wordt verzonden; *Ad Start* wordt de analytische oproep verzonden op ad start, enzovoort; de *Sluiten* de vraag is de gecompileerde analytische vraag die rechtstreeks van de hartslagserver naar de analyseserver aan het eind van de media zitting, of het eind van de advertentie, het hoofdstuk, enz. wordt verzonden. De dichte vraag is niet beschikbaar in de vraag van het netwerkpakket.
   * *Min. SDK-versie* - Geeft aan welke SDK-versie u toegang tot de parameter nodig hebt.
   * *Samplewaarde* - Verstrekt voorbeeld van gemeenschappelijk veranderlijk gebruik.
* **Netwerkparameters:** Hiermee geeft u de waarden weer die worden doorgegeven aan Adobe Analytics- of Hartslagservers. Deze kolom toont de namen van de parameters die in de netwerkvraag worden gezien die door Adobe Media SDKs wordt geproduceerd.
* **Rapportage:** Informatie over het weergeven en analyseren van videogegevens.
   * *Beschikbaar* - Geeft aan of de gegevens standaard beschikbaar zijn in de rapportage (*Ja*), of aangepaste instelling vereist (*Aangepast*)
   * *Gereserveerde variabele* - Geeft aan of de gegevens zijn vastgelegd als een gebeurtenis, eVar, eigenschap of classificatie in een gereserveerde variabele.
   * *Rapportnaam* - Naam van Adobe Analytics-rapport voor variabele
   * *Contextgegevens* - Naam van de Adobe Analytics-contextgegevens die aan de rapportserver worden doorgegeven en die in verwerkingsregels worden gebruikt.
   * *Gegevensfeed* - Kolomnaam voor variabele in Clickstream- of Live Stream-gegevensfeeds
   * *Audience Manager* - Trainingsnaam gevonden in Adobe Audience Manager

>[!IMPORTANT]
>
>Wijzig de classificatienamen niet voor onderstaande variabelen die
>beschreven onder Rapportage/Gereserveerde variabele als &quot;classificatie&quot;.
>De mediaclassificaties worden gedefinieerd wanneer een rapportsuite is ingeschakeld voor media
>bijhouden. Van tijd tot tijd voegt Adobe nieuwe eigenschappen toe, en, wanneer dit voorkomt,
>klanten moeten hun rapportsuites opnieuw toelaten om toegang tot de nieuwe media te krijgen
>eigenschappen. Tijdens het updateproces bepaalt Adobe of de
>classificaties worden ingeschakeld door de namen van de variabelen te controleren. Indien
>ze ontbreken , voegt Adobe de ontbrekende weer toe .

## Videogegevens toevoegen {#ad-video-data}

### ID advertentie

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-sleutel:**<br/> [adId](./ad-parameters.md#section_Related_APIs) </li> <li> **API-sleutel:**<br/> media.ad.id </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Advertentie starten, en sluiten </li> <li> **Min. SDK-versie:** Alle  </li> <li> **Samplewaarde:**<br/> &quot;2125&quot; </li><li> **Omschrijving:**<br/> ID van de advertentie. (Willekeurig geheel getal en/of lettercombinatie)  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>name) </li> <li> **Hartslag:**<br/> (s:asset:ad_id) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Bij BEZOEK </li> <li> **Rapportnaam:**<br/> Advertentie </li> <li> **Contextgegevens:**<br/> (a.media.ad.<br/>name) </li> <li> **Gegevensfeed:**<br/> video </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.na) </li> <li> **XDM-veldpad:**<br/> advertentie.adAssetReference.@id </li> <li> **XDM-veldpad voor verzameling:**<br/> mediaCollection.advertenceDetails.ID </li> <li> **XDM-veldpad rapporteren:**<br/> mediaReporting.advertenceDetails.ID </li> </ul> |



### Positie advertentie in pod

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-sleutel:**<br/> [position](./ad-parameters.md#section_Related_APIs) </li> <li> **API-sleutel:**<br/> media.ad.podPosition </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Advertentie starten, en sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> 1 </li><li> **Omschrijving:**<br/> De positie (index) van de advertentie binnen het bovenliggende element en het einde. De eerste advertentie heeft index 0, de tweede advertentie heeft index 1, enz.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>podPosition) </li> <li> **Hartslag:**<br/> (s:asset:pod_positie) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Positie advertentie in pod </li> <li> **Contextgegevens:**<br/> (a.media.ad.<br/>podPosition) </li> <li> **Gegevensfeed:**<br/> videoadinpod </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podPosition) </li> <li> **XDM-veldpad:**<br/> advertentie.addAssetViewDetails.index </li> <li> **XDM-veldpad voor verzameling:**<br/> mediaCollection.advertenceDetails.index </li> <li> **XDM-veldpad rapporteren:**<br/> mediaReporting.advertenceDetails.index </li> </ul> |



### Advertentieduur

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-sleutel:**<br/>  [length](./ad-parameters.md#section_Related_APIs) </li> <li> **API-sleutel:**<br/> media.ad.length </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Advertentie starten, en sluiten </li> <li> **Min. SDK-versie:** 1.5.1. </li> <li> **Samplewaarde:**<br/> &quot;15&quot;  </li><li> **Omschrijving:**<br/> Lengte van video en in seconden.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>length) </li> <li> **Hartslag:**<br/> l:asset:ad_length) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar en indeling </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Ad Length en Ad Length (variabele) </li> <li> **Contextgegevens:**<br/> (a.media.ad.<br/>lengte) </li> <li> **Gegevensfeed:**<br/> videoadlength </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.length) </li> <li> **XDM-veldpad:**<br/> advertentie.adAssetReference.<br/>xmpDM:duration </li> <li> **XDM-veldpad voor verzameling:**<br/> mediaCollection.advertenceDetails.length </li> <li> **XDM-veldpad rapporteren:**<br/> mediaReporting.advertenceDetails.length </li> </ul> |



### Naam van advertentiespeler

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-sleutel:**<br/>  [playerName](./ad-parameters.md#section_Related_APIs) </li> <li> **API-sleutel:**<br/> media.ad.playerName </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Advertentie starten, en sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> &quot;Bevriewiel&quot; </li><li> **Omschrijving:**<br/> De naam van de speler die verantwoordelijk is voor het renderen van de advertentie.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>playerName) </li> <li> **Hartslag:**<br/> (s:sp:player_name) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Naam van advertentiespeler </li> <li> **Contextgegevens:**<br/> (a.media.ad.<br/>playerName) </li> <li> **Gegevensfeed:**<br/> videoadplayernaam </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.playerName) </li> <li> **XDM-veldpad:**<br/> advertentie.adAssetViewDetails.playerName </li> <li> **XDM-veldpad voor verzameling:**<br/> mediaCollection.advertenceDetails.<br/>playerName </li> <li> **XDM-veldpad rapporteren:**<br/> mediaReporting.advertenceDetails.<br/>playerName </li> </ul> |



### Naam advertentie-einde

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-sleutel:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **API-sleutel:**<br/> media.ad.podFriendlyName </li> <li> **Vereist:**<br/> SDK: Ja; API: Nee. </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Advertentie starten, en sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> &quot;pre-roll&quot; </li><li> **Omschrijving:**<br/> De vriendelijke naam van het Advertentiepagina.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>podFriendlyName) </li> <li> **Hartslag:**<br/> (s:asset:pod_naam) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> Classificatie </li> <li> **Rapportnaam:**<br/> Podnaam </li> <li> **Contextgegevens:**<br/> (a.media.ad.<br/>podFriendlyName) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podFriendlyName) </li> <li> **XDM-veldpad:**<br/> advertentie.adAssetViewDetails.<br/>adBreak.dc:title </li> <li> **XDM-veldpad voor verzameling:**<br/> mediaCollection.advertentiePodDetails.<br/>kindName </li> <li> **XDM-veldpad rapporteren:**<br/> mediaReporting.advertentiePodDetails.<br/>kindName </li> </ul> |



### Index van advertentiepunten

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-sleutel:**<br/>  [positie](./ad-parameters.md#section_Related_APIs) </li> <li> **API-sleutel:**<br/> media.ad.podPosition </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> 1 </li><li> **Omschrijving:**<br/> De index van het advertentieeinde binnen de inhoud die begint bij 1. Deze eigenschap wordt gebruikt **alleen** door de SDK van Media om de pod-id te genereren.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **Hartslag:**<br/> </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Nee </li> <li> **Gereserveerde variabele:**<br/> N.v.t. </li> <li> **Rapportnaam:**<br/> N.v.t. </li> <li> **Contextdata:**<br/> </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> </li> <li> **XDM-veldpad:**<br/> advertentie.addAssetViewDetails.index </li> <li> **XDM-veldpad voor verzameling:**<br/> mediaCollection.advertencePodDetails.index </li> </ul> |



### Positie advertentie-einde

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-sleutel:**<br/>  [startTime](./ad-parameters.md#section_Related_APIs) </li> <li> **API-sleutel:**<br/> media.ad.podSecond </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Advertentie starten, en sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> 90 </li><li> **Omschrijving:**<br/> De verschuiving van het advertentieeinde binnen de inhoud, in seconden.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>podSecond) </li> <li> **Hartslag:**<br/> l:asset:pod_offset) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> Classificatie </li> <li> **Rapportnaam:**<br/> Podpositie </li> <li> **Contextgegevens:**<br/> (a.media.ad.<br/>podSecond) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podSecond) </li> <li> **XDM-veldpad:**<br/> advertentie.adAssetViewDetails.adBreak.<br/>offset </li> <li> **XDM-veldpad voor verzameling:**<br/> mediaCollection.advertentiePodDetails.<br/>offset </li> <li> **XDM-veldpad rapporteren:**<br/> mediaReporting.advertentiePodDetails.<br/>offset </li> </ul> |



### ID advertentie-einde

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Advertentie starten, en sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> c4a577424c84067899b807c76722d495_1  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>pod) </li> <li> **Hartslag:**<br/> (s:asset:pod_id) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Advertentiepod </li> <li> **Contextgegevens:**<br/> (a.media.ad.<br/>pod) </li> <li> **Gegevensfeed:**<br/> videoadpod </li> <li> **Audience Manager:**<br/> </li> <li> **XDM-veldpad:**<br/> advertentie.adAssetViewDetails.adBreak.@id </li> <li> **XDM-veldpad rapporteren:**<br/> mediaReporting.advertentiePodDetails.<br/>ID </li> </ul> |



### Advertentienaam

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-sleutel:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **API-sleutel:**<br/> media.ad.name </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Advertentie starten, en sluiten </li> <li> **Min. SDK-versie:** 1.5.1. </li> <li> **Samplewaarde:**<br/> &quot;Ford F-150&quot; </li><li> **Omschrijving:**<br/> Vriendelijke naam van de advertentie.  Bij de rapportage is &quot;Advertentienaam&quot; de classificatie en &quot;Advertentienaam (variabele)&quot; de eVar.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>vriendelijkeName) </li> <li> **Hartslag:**<br/> (s:asset:ad_name) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar en indeling </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Advertentienaam en Advertentienaam (variabele) </li> <li> **Contextgegevens:**<br/> (a.media.ad.<br/>vriendelijkeName) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.friendlyName) </li> <li> **XDM-veldpad:**<br/> advertentie.adAssetReference.dc:title </li> <li> **XDM-veldpad voor verzameling:**<br/> mediaCollection.advertenceDetails.name </li> <li> **XDM-veldpad rapporteren:**<br/> mediaReporting.advertenceDetails.name </li> </ul> |



## Standaard advertentiemetagegevens {#standard-ad-metadata}

### Adverteerder

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-sleutel:**<br/> ADVERTISER </li> <li> **API-sleutel:**<br/> media.ad.advertiser </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Advertentie starten, en sluiten </li> <li> **Min. SDK-versie:** 1.5.7. </li> <li> **Samplewaarde:**<br/> </li><li> **Omschrijving:**<br/> Bedrijf/merk waarvan het product in de advertentie wordt vermeld.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>adverteerder) </li> <li> **Hartslag:**<br/> (s:meta:<br/>a.media.ad.advertiser) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> <i>Adverteerder </i> </li> <li> **Contextgegevens:**<br/> (a.media.ad.<br/>adverteerder) </li> <li> **Gegevensfeed:**<br/> videoadverteerder </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.advertiser) </li> <li> **XDM-veldpad:**<br/> advertentie.adAssetReference.adverteerder </li> <li> **XDM-veldpad voor verzameling:**<br/> mediaCollection.advertenceDetails.adverteerder </li> <li> **XDM-veldpad rapporteren:**<br/> mediaReporting.advertenceDetails.adverteerder </li> </ul> |



### Campagne-id

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-sleutel:**<br/> CAMPAIGN_ID </li> <li> **API-sleutel:**<br/> media.ad.campaignId </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Advertentie starten, en sluiten </li> <li> **Min. SDK-versie:** 1.5.7. </li> <li> **Samplewaarde:**<br/> Geheel getal of naam (tekenreeks).  </li><li> **Omschrijving:**<br/> Id van de advertentiecampagne.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>campaign) </li> <li> **Hartslag:**<br/> (s:meta:<br/>a.media.ad.campaign) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> <i>Campagne-id </i> </li> <li> **Contextgegevens:**<br/> (a.media.ad.<br/>campagne) </li> <li> **Gegevensfeed:**<br/> videocampagne </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.campaign) </li> <li> **XDM-veldpad:**<br/> advertentie.adAssetReference.campagne </li> <li> **XDM-veldpad voor verzameling:**<br/> mediaCollection.advertenceDetails.<br/>campagneID </li> <li> **XDM-veldpad rapporteren:**<br/> mediaReporting.advertenceDetails.<br/>campagneID </li> </ul> |



### Creative-id

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-sleutel:**<br/> CREATIVE_ID </li> <li> **API-sleutel:**<br/> media.ad.creativeId </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Advertentie starten, en sluiten </li> <li> **Min. SDK-versie:** 1.5.7. </li> <li> **Samplewaarde:**<br/> Geheel getal of naam (tekenreeks).  </li><li> **Omschrijving:**<br/> Id van de advertentie.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>creatief) </li> <li> **Hartslag:**<br/> (s:meta:<br/>a.media.ad.creative) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> <i>Creative-id </i> </li> <li> **Contextgegevens:**<br/> (a.media.ad.<br/>creatief) </li> <li> **Gegevensfeed:**<br/> adclassificatie creatief </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.creative) </li> <li> **XDM-veldpad:**<br/> advertentie.adAssetReference.creativeID </li> <li> **XDM-veldpad voor verzameling:**<br/> mediaCollection.advertenceDetails.creativeID </li> <li> **XDM-veldpad rapporteren:**<br/> mediaReporting.advertenceDetails.creativeID </li> </ul> |



### Site-id

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-sleutel:**<br/> SITE_ID </li> <li> **API-sleutel:**<br/> media.ad.siteId </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Advertentie starten, en sluiten </li> <li> **Min. SDK-versie:** 1.5.7. </li> <li> **Samplewaarde:**<br/> </li><li> **Omschrijving:**<br/> ID van de advertentiesite.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>site) </li> <li> **Hartslag:**<br/> (s:meta:<br/>a.media.ad.site) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> <i>Aangepaste verwerkingsregel gebruiken </i> </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Aangepast </li> <li> **Contextgegevens:**<br/> (a.media.ad.<br/>site) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.site) </li> <li> **XDM-veldpad:**<br/> advertentie.adAssetReference.siteID </li> <li> **XDM-veldpad voor verzameling:**<br/> mediaCollection.advertenceDetails.siteID </li> <li> **XDM-veldpad rapporteren:**<br/> mediaReporting.advertenceDetails.siteID </li> </ul> |



### Creative URL

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-sleutel:**<br/> CREATIVE_URL </li> <li> **API-sleutel:**<br/> media.ad.creativeURL </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Advertentie starten, en sluiten </li> <li> **Min. SDK-versie:** 1.5.7. </li> <li> **Samplewaarde:**<br/> </li><li> **Omschrijving:**<br/> URL van de advertentie.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>creativeURL) </li> <li> **Hartslag:**<br/> (s:meta:<br/>a.media.ad.creativeURL) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> <i>Aangepaste verwerkingsregel gebruiken </i> </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Aangepast </li> <li> **Contextgegevens:**<br/> (a.media.ad.<br/>creativeURL) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.creativeURL) </li> <li> **XDM-veldpad:**<br/> advertentie.adAssetReference.creativeURL </li> <li> **XDM-veldpad voor verzameling:**<br/> mediaCollection.advertenceDetails.<br/>creativeURL </li> <li> **XDM-veldpad rapporteren:**<br/> mediaReporting.advertenceDetails.<br/>creativeURL </li> </ul> |



### Plaatsing-id

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-sleutel:**<br/> PLACEMENT_ID </li> <li> **API-sleutel:**<br/> media.ad.placementId </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Advertentie starten, en sluiten </li> <li> **Min. SDK-versie:** 1.5.7. </li> <li> **Samplewaarde:**<br/> </li><li> **Omschrijving:**<br/> Plaatsing-id van de advertentie.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>plaatsing) </li> <li> **Hartslag:**<br/> (s:meta:<br/>a.media.ad.placement) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> <i>Aangepaste verwerkingsregel gebruiken </i> </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Aangepast </li> <li> **Contextgegevens:**<br/> (a.media.ad.<br/>plaatsing) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.placement) </li> <li> **XDM-veldpad:**<br/> advertentie.adAssetReference.placementID </li> <li> **XDM-veldpad voor verzameling:**<br/> mediaCollection.advertenceDetails.<br/>placementID </li> <li> **XDM-veldpad rapporteren:**<br/> mediaReporting.advertenceDetails.<br/>placementID </li> </ul> |




## Metrische gegevens toevoegen {#ad-metrics}

### Ad Start

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Ad Start </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> TRUE </li><li> **Omschrijving:**<br/> Aantal video&#39;s dat wordt toegevoegd.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>weergave) </li> <li> **Hartslag:**<br/>  (s:event:type=start)<br/> (s:asset:type=ad) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Advertentiestartpagina </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Contextgegevens:**<br/> (a.media.ad.<br/>weergave) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.view) </li> <li> **XDM-veldpad:**<br/> advertentie.start.value > 0 => &quot;TRUE&quot; </li> <li> **XDM-veldpad rapporteren:**<br/> mediaReporting.advertenceDetails.isStarted </li> </ul> |



### Toevoegen voltooid

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Advertentie sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> TRUE </li><li> **Omschrijving:**<br/> Aantal video&#39;s dat is voltooid.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>complete) </li> <li> **Hartslag:**<br/> (s:event:type=complete)<br/> (s:asset:type=ad)  </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Voltooien toevoegen </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Contextgegevens:**<br/> (a.media.ad.<br/>complete) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.complete) </li> <li> **XDM-veldpad:**<br/> advertentie.completes.value > 0 => &quot;TRUE&quot; </li> <li> **XDM-veldpad rapporteren:**<br/> mediaReporting.advertenceDetails.<br/>isCompleted </li> </ul> |



### Toegevoegde tijd

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Advertentie sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> 15 </li><li> **Omschrijving:**<br/> De totale hoeveelheid tijd, in seconden, die wordt besteed aan het bekijken van de advertentie (d.w.z. het aantal seconden dat wordt afgespeeld).  De waarde wordt weergegeven in de tijdnotatie (HH:MM:SS) in Analysis Workspace en Reports &amp; Analytics. In de Diervoeders van Gegevens, Data Warehouse, en Rapporterende APIs zullen de waarden in seconden worden getoond.  <br/>**Releasedatum: 13-09-18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>timePlayed) </li> <li> **Hartslag:**<br/> </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Toegevoegde tijd </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Contextgegevens:**<br/> (a.media.ad.<br/>timePlayed) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.timePlayed) </li> <li> **XDM-veldpad:**<br/> advertentie.timePlayed.value </li> <li> **XDM-veldpad rapporteren:**<br/> mediaReporting.advertenceDetails.<br/>timePlayed </li> </ul> |



## Verwante API&#39;s {#section_Related_APIs}

### createAdObject-API&#39;s:

* Android - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdObject-java.lang.String-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdObjectWithName:adId:position:length:)
* JavaScript - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdObject)

### createAdBreakObject-API&#39;s:

* Android - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdBreakObject-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdBreakObjectWithName:position:startTime:)
* JavaScript - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdBreakObject)

### MediaHeartboneConfig-API&#39;s:

* Android - [MediaHeartboneConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartboneConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html#toc0)
