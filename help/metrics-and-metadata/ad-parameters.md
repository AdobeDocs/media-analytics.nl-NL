---
title: Ad-parameters
description: null
uuid: 92cd7f97-bb5a-4de6-8946-453d30271d0f
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Ad-parameters{#ad-parameters}

Dit onderwerp bevat een lijst met video en gegevens, waaronder contextgegevens, die Adobe verzamelt via oplossingvariabelen.

Beschrijving van tabelgegevens:

* **Implementatie:** Informatie over implementatiewaarden en -vereisten
   * *Sleutel* - Variabel, stelt u deze handmatig in uw app in of automatisch in door de SDK van Adobe Media.
   * *Vereist* - Geeft aan of de parameter is vereist voor het bijhouden van basisvideo.
   * *Type* - Geeft het type op van de variabele die moet worden ingesteld, de tekenreeks of het getal.
   * *Verzonden met* - Geeft aan wanneer de gegevens worden verzonden: Het Begin *van* Media is de analytische vraag die op media begin wordt verzonden, het Begin *van* Ad is de analytische vraag die op ad start wordt verzonden, etc. de *Dichte* vraag is de gecompileerde analytische vraag die rechtstreeks van de hartslagserver naar de analyseserver aan het eind van de media zitting, of het eind van de advertentie, het hoofdstuk, enz. wordt verzonden. De dichte vraag is niet beschikbaar in de vraag van het netwerkpakket.
   * *Min. SDK-versie* - Geeft aan welke SDK-versie u toegang tot de parameter nodig hebt.
   * *Samplewaarde* - Geeft een voorbeeld van algemeen variabelengebruik.
* **Netwerkparameters:** Hiermee geeft u de waarden weer die aan Adobe Analytics of Heartmaatservers worden doorgegeven. Deze kolom toont de namen van de parameters die in de netwerkvraag worden gezien die door de Media SDKs van Adobe wordt geproduceerd.
* **Rapportage:** Informatie over het weergeven en analyseren van videogegevens.
   * *Beschikbaar* - Geeft aan of de gegevens standaard beschikbaar zijn in de rapportage (*Ja*) of dat aangepaste instellingen vereist zijn (*Aangepast*)
   * *Gereserveerde variabele* - Geeft aan of de gegevens zijn vastgelegd als een gebeurtenis, eVar, eigenschap of classificatie in een gereserveerde variabele.
   * *Rapportnaam* - Naam van Adobe Analytics-rapport voor variabele
   * *Contextgegevens* - Naam van de Adobe Analytics-contextgegevens die aan de rapportserver zijn doorgegeven en in verwerkingsregels worden gebruikt.
   * *Gegevensfeed* - Kolomnaam voor variabele gevonden in Clickstream- of Live Stream-gegevensfeeds
   * *Auditiebeheer* - Trait name found in Adobe Audience Manager

>[!IMPORTANT]
>
>Wijzig de classificatienamen niet voor onderstaande variabelen die
>beschreven onder Rapportage/Gereserveerde variabele als &quot;classificatie&quot;.
>De mediaclassificaties worden gedefinieerd wanneer een rapportsuite is ingeschakeld voor media
>bijhouden. Adobe voegt van tijd tot tijd nieuwe eigenschappen toe en wanneer dit gebeurt,
>klanten moeten hun rapportsuites opnieuw toelaten om toegang tot de nieuwe media te krijgen
>eigenschappen. Tijdens het updateproces bepaalt Adobe of de
>classificaties worden ingeschakeld door de namen van de variabelen te controleren. Indien
>deze ontbreken, voegt Adobe de ontbrekende opnieuw toe.

## Videogegevens toevoegen {#ad-video-data}

### ID advertentie

|   Implementatie | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> [adId](./ad-parameters.md#section_Related_APIs) </li> <li> **API-sleutel:**<br/>media.ad.id</li> <li> **Vereist:**<br/>Ja</li> <li> **Type:**<br/>string</li> <li> **Verzonden met:**<br/>Advertentie starten, en sluiten</li> <li> **Min. SDK-versie:** Alle  </li> <li> **Samplewaarde:**<br/>&quot;2125&quot;</li><li> **Beschrijving:**<br/>id van de advertentie. (Willekeurig geheel getal en/of lettercombinatie)</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.ad.<br/>name)</li> <li> **Hartslag:**<br/>(s:asset:ad_id)</li> </ul> | <ul> <li> **Beschikbaar:**<br/>Ja</li> <li> **Gereserveerde variabele:**<br/>eVar</li> <li> **Verlopen:**<br/>Bij BEZOEK</li> <li> **Rapportnaam:**<br/>Advertentie</li> <li> **Contextgegevens:**<br/>(a.media.ad.<br/>name)</li> <li> **Gegevensfeed:**<br/>video</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.ad.na)</li> </ul> |



### Positie advertentie in pod

|   Implementatie | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> [positie](./ad-parameters.md#section_Related_APIs) </li> <li> **API-sleutel:**<br/>media.ad.podPosition</li> <li> **Vereist:**<br/>Ja</li> <li> **Type:**<br/>getal</li> <li> **Verzonden met:**<br/>Advertentie starten, en sluiten</li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/>1</li><li> **Beschrijving:**<br/>De positie (index) van de advertentie binnen het bovenliggende element en het einde. De eerste advertentie heeft index 0, de tweede advertentie heeft index 1, enz.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.ad.<br/>podPosition)</li> <li> **Hartslag:**<br/>(s:asset:pod_position)</li> </ul> | <ul> <li> **Beschikbaar:**<br/>Ja</li> <li> **Gereserveerde variabele:**<br/>eVar</li> <li> **Verlopen:**<br/>Op HIT</li> <li> **Rapportnaam:**<br/>Positie advertentie in pod</li> <li> **Contextgegevens:**<br/>(a.media.ad.<br/>podPosition)</li> <li> **Gegevensfeed:**<br/>videoadinpod</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.ad.podPosition)</li> </ul> |



### Advertentieduur

|   Implementatie | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>  [length](./ad-parameters.md#section_Related_APIs) </li> <li> **API-sleutel:**<br/>media.ad.length</li> <li> **Vereist:**<br/>Ja</li> <li> **Type:**<br/>getal</li> <li> **Verzonden met:**<br/>Advertentie starten, en sluiten</li> <li> **Min. SDK-versie:** 1.5.1. </li> <li> **Samplewaarde:**<br/>&quot;15&quot;</li><li> **Beschrijving:**<br/>duur van video en in seconden.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.ad.<br/>lengte)</li> <li> **Hartslag:**<br/>(l:asset:ad_length)</li> </ul> | <ul> <li> **Beschikbaar:**<br/>Ja</li> <li> **Gereserveerde variabele:**<br/>Var en classificatie</li> <li> **Verlopen:**<br/>Op HIT</li> <li> **Rapportnaam:**<br/>Ad Length en Ad Length (variabele)</li> <li> **Contextgegevens:**<br/>(a.media.ad.<br/>lengte)</li> <li> **Gegevensfeed:**<br/>videoadlength</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.ad.length)</li> </ul> |



### Naam van advertentiespeler

|   Implementatie | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>  [playerName](./ad-parameters.md#section_Related_APIs) </li> <li> **API-sleutel:**<br/>media.ad.playerName</li> <li> **Vereist:**<br/>Ja</li> <li> **Type:**<br/>string</li> <li> **Verzonden met:**<br/>Advertentie starten, en sluiten</li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/>&quot;Bevriewiel&quot;</li><li> **Beschrijving:**<br/>De naam van de speler die verantwoordelijk is voor het renderen van de advertentie.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.ad.<br/>playerName)</li> <li> **Hartslag:**<br/>(s:sp:player_name)</li> </ul> | <ul> <li> **Beschikbaar:**<br/>Ja</li> <li> **Gereserveerde variabele:**<br/>eVar</li> <li> **Verlopen:**<br/>Op HIT</li> <li> **Rapportnaam:**<br/>Naam van advertentiespeler</li> <li> **Contextgegevens:**<br/>(a.media.ad.<br/>playerName)</li> <li> **Gegevensfeed:**<br/>videoadplayernaam</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.ad.playerName)</li> </ul> |



### Naam advertentie-einde

|   Implementatie | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **API-sleutel:**<br/>media.ad.podFriendlyName</li> <li> **Vereist:**<br/>SDK: Ja; API: Nee.</li> <li> **Type:**<br/>string</li> <li> **Verzonden met:**<br/>Advertentie starten, en sluiten</li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/>&quot;pre-roll&quot;</li><li> **Omschrijving:**<br/>de vriendelijke naam van het advertentiepunt.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.ad.<br/>podFriendlyName)</li> <li> **Hartslag:**<br/>(s:asset:pod_name)</li> </ul> | <ul> <li> **Beschikbaar:**<br/>Ja</li> <li> **Gereserveerde variabele:**<br/>Classificatie</li> <li> **Rapportnaam:**<br/>Podnaam</li> <li> **Contextgegevens:**<br/>(a.media.ad.<br/>podFriendlyName)</li> <li> **Gegevensfeed:**<br/>N.v.t.</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.ad.podFriendlyName)</li> </ul> |



### Index van advertentiepunten

|   Implementatie | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>  [positie](./ad-parameters.md#section_Related_APIs) </li> <li> **API-sleutel:**<br/>media.ad.podPosition</li> <li> **Vereist:**<br/>Ja</li> <li> **Type:**<br/>getal</li> <li> **Verzonden met:**<br/> </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/>1</li><li> **Beschrijving:**<br/>De index van het advertentie-einde binnen de inhoud die begint bij 1. Deze eigenschap wordt**alleen **door de Media SDK gebruikt om de pod-id te genereren.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **Hartslag:**<br/> </li> </ul> | <ul> <li> **Beschikbaar:**<br/>Nee</li> <li> **Gereserveerde variabele:**<br/>N.v.t.</li> <li> **Rapportnaam:**<br/>N.v.t.</li> <li> **Contextgegevens:**<br/> </li> <li> **Gegevensfeed:**<br/>N.v.t.</li> <li> **Audience Manager:**<br/> </li> </ul> |



### Positie advertentie-einde

|   Implementatie | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>  [startTime](./ad-parameters.md#section_Related_APIs) </li> <li> **API-sleutel:**<br/>media.ad.podSecond</li> <li> **Vereist:**<br/>Ja</li> <li> **Type:**<br/>getal</li> <li> **Verzonden met:**<br/>Advertentie starten, en sluiten</li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/>90</li><li> **Beschrijving:**<br/>De verschuiving van het advertentieeinde binnen de inhoud, in seconden.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.ad.<br/>podSecond)</li> <li> **Hartslag:**<br/>(l:element:pod_offset)</li> </ul> | <ul> <li> **Beschikbaar:**<br/>Ja</li> <li> **Gereserveerde variabele:**<br/>Classificatie</li> <li> **Rapportnaam:**<br/>Podpositie</li> <li> **Contextgegevens:**<br/>(a.media.ad.<br/>podSecond)</li> <li> **Gegevensfeed:**<br/>N.v.t.</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.ad.podSecond)</li> </ul> |



### ID advertentie-einde

|   Implementatie | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>Automatisch instellen</li> <li> **API-sleutel:**<br/>N.v.t.</li> <li> **Vereist:**<br/>Ja</li> <li> **Type:**<br/>string</li> <li> **Verzonden met:**<br/>Advertentie starten, en sluiten</li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/>c4a577424c84067899b807c76722d495_1</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.ad.<br/>pod)</li> <li> **Hartslag:**<br/>(s:asset:pod_id)</li> </ul> | <ul> <li> **Beschikbaar:**<br/>Ja</li> <li> **Gereserveerde variabele:**<br/>eVar</li> <li> **Verlopen:**<br/>Op HIT</li> <li> **Rapportnaam:**<br/>Advertentiepod</li> <li> **Contextgegevens:**<br/>(a.media.ad.<br/>pod)</li> <li> **Gegevensfeed:**<br/>videoadpod</li> <li> **Audience Manager:**<br/> </li> </ul> |



### Advertentienaam

|   Implementatie | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **API-sleutel:**<br/>media.ad.name</li> <li> **Vereist:**<br/>Nee</li> <li> **Type:**<br/>string</li> <li> **Verzonden met:**<br/>Advertentie starten, en sluiten</li> <li> **Min. SDK-versie:** 1.5.1. </li> <li> **Samplewaarde:**<br/>&quot;Ford F-150&quot;</li><li> **Beschrijving:**<br/>Vriendelijke naam van de advertentie.  Bij de rapportage is &quot;Advertentienaam&quot; de classificatie en &quot;Advertentienaam (variabele)&quot; de Var.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.ad.<br/>vriendelijkeName)</li> <li> **Hartslag:**<br/>(s:asset:ad_name)</li> </ul> | <ul> <li> **Beschikbaar:**<br/>Ja</li> <li> **Gereserveerde variabele:**<br/>Var en classificatie</li> <li> **Verlopen:**<br/>Op HIT</li> <li> **Rapportnaam:**<br/>Advertentienaam en Advertentienaam (variabele)</li> <li> **Contextgegevens:**<br/>(a.media.ad.<br/>vriendelijkeName)</li> <li> **Gegevensfeed:**<br/>N.v.t.</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.ad.friendlyName)</li> </ul> |



## Standaard advertentiemetagegevens {#standard-ad-metadata}

### Adverteerder

|   Implementatie | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>ADVERTISER</li> <li> **API-sleutel:**<br/>media.ad.advertiser</li> <li> **Vereist:**<br/>Nee</li> <li> **Type:**<br/>string</li> <li> **Verzonden met:**<br/>Advertentie starten, en sluiten</li> <li> **Min. SDK-versie:** 1.5.7. </li> <li> **Samplewaarde:**<br/> </li><li> **Omschrijving:**<br/>Bedrijf/Merk waarvan het product in de advertentie is vermeld.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.ad.<br/>adverteerder)</li> <li> **Hartslag:**<br/>(s:meta:<br/>a.media.ad.advertiser)</li> </ul> | <ul> <li> **Beschikbaar:**<br/>Ja</li> <li> **Gereserveerde variabele:**<br/>eVar</li> <li> **Verlopen:**<br/>Op HIT</li> <li> **Rapportnaam:**<br/> <i>Adverteerder </i> </li> <li> **Contextgegevens:**<br/>(a.media.ad.<br/>adverteerder)</li> <li> **Gegevensfeed:**<br/>videoadverteerder</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.ad.advertiser)</li> </ul> |



### Campagne-id

|   Implementatie | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>CAMPAIGN_ID</li> <li> **API-sleutel:**<br/>media.ad.campaignId</li> <li> **Vereist:**<br/>Nee</li> <li> **Type:**<br/>string</li> <li> **Verzonden met:**<br/>Advertentie starten, en sluiten</li> <li> **Min. SDK-versie:** 1.5.7. </li> <li> **Samplewaarde:**<br/>Geheel getal of naam (tekenreeks).</li><li> **Beschrijving:**<br/>id van de advertentiecampagne.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.ad.<br/>campagne)</li> <li> **Hartslag:**<br/>(s:meta:<br/>a.media.ad.campaign)</li> </ul> | <ul> <li> **Beschikbaar:**<br/>Ja</li> <li> **Gereserveerde variabele:**<br/>eVar</li> <li> **Verlopen:**<br/>Op HIT</li> <li> **Rapportnaam:**<br/> <i>Campagne-id </i> </li> <li> **Contextgegevens:**<br/>(a.media.ad.<br/>campagne)</li> <li> **Gegevensfeed:**<br/>videocampagne</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.ad.campaign)</li> </ul> |



### Creative-id

|   Implementatie | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>CREATIVE_ID</li> <li> **API-sleutel:**<br/>media.ad.creativeId</li> <li> **Vereist:**<br/>Nee</li> <li> **Type:**<br/>string</li> <li> **Verzonden met:**<br/>Advertentie starten, en sluiten</li> <li> **Min. SDK-versie:** 1.5.7. </li> <li> **Samplewaarde:**<br/>Geheel getal of naam (tekenreeks).</li><li> **Beschrijving:**<br/>id van de advertentie.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.ad.<br/>creatief)</li> <li> **Hartslag:**<br/>(s:meta:<br/>a.media.ad.creative)</li> </ul> | <ul> <li> **Beschikbaar:**<br/>Ja</li> <li> **Gereserveerde variabele:**<br/>eVar</li> <li> **Verlopen:**<br/>Op HIT</li> <li> **Rapportnaam:**<br/> <i>Creative-id </i> </li> <li> **Contextgegevens:**<br/>(a.media.ad.<br/>creatief)</li> <li> **Gegevensfeed:**<br/>adclassificatie creatief</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.ad.creative)</li> </ul> |



### Site-id

|   Implementatie | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>SITE_ID</li> <li> **API-sleutel:**<br/>media.ad.siteId</li> <li> **Vereist:**<br/>Nee</li> <li> **Type:**<br/>string</li> <li> **Verzonden met:**<br/>Advertentie starten, en sluiten</li> <li> **Min. SDK-versie:** 1.5.7. </li> <li> **Samplewaarde:**<br/> </li><li> **Beschrijving:**<br/>id van de advertentiesite.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.ad.<br/>site)</li> <li> **Hartslag:**<br/>(s:meta:<br/>a.media.ad.site)</li> </ul> | <ul> <li> **Beschikbaar:**<br/> <i>Aangepaste verwerkingsregel gebruiken </i> </li> <li> **Gereserveerde variabele:**<br/>eVar</li> <li> **Verlopen:**<br/>Op HIT</li> <li> **Rapportnaam:**<br/> <i> </i> </li> <li> **Contextgegevens:**<br/>(a.media.ad.<br/>site)</li> <li> **Gegevensfeed:**<br/>N.v.t.</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.ad.site)</li> </ul> |



### Creative URL

|   Implementatie | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>CREATIVE_URL</li> <li> **API-sleutel:**<br/>media.ad.creativeURL</li> <li> **Vereist:**<br/>Nee</li> <li> **Type:**<br/>string</li> <li> **Verzonden met:**<br/>Advertentie starten, en sluiten</li> <li> **Min. SDK-versie:** 1.5.7. </li> <li> **Samplewaarde:**<br/> </li><li> **Beschrijving:**<br/>URL van de advertentie.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.ad.<br/>creativeURL)</li> <li> **Hartslag:**<br/>(s:meta:<br/>a.media.ad.creativeURL)</li> </ul> | <ul> <li> **Beschikbaar:**<br/> <i>Aangepaste verwerkingsregel gebruiken </i> </li> <li> **Gereserveerde variabele:**<br/>eVar</li> <li> **Verlopen:**<br/>Op HIT</li> <li> **Rapportnaam:**<br/> <i> </i> </li> <li> **Contextgegevens:**<br/>(a.media.ad.<br/>creativeURL)</li> <li> **Gegevensfeed:**<br/>N.v.t.</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.ad.creativeURL)</li> </ul> |



### Plaatsing-id

|   Implementatie | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>PLACEMENT_ID</li> <li> **API-sleutel:**<br/>media.ad.placementId</li> <li> **Vereist:**<br/>Nee</li> <li> **Type:**<br/>string</li> <li> **Verzonden met:**<br/>Advertentie starten, en sluiten</li> <li> **Min. SDK-versie:** 1.5.7. </li> <li> **Samplewaarde:**<br/> </li><li> **Beschrijving:**<br/>Plaatsing-id van de advertentie.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.ad.<br/>plaatsing)</li> <li> **Hartslag:**<br/>(s:meta:<br/>a.media.ad.placement)</li> </ul> | <ul> <li> **Beschikbaar:**<br/> <i>Aangepaste verwerkingsregel gebruiken </i> </li> <li> **Gereserveerde variabele:**<br/>eVar</li> <li> **Verlopen:**<br/>Op HIT</li> <li> **Rapportnaam:**<br/> <i> </i> </li> <li> **Contextgegevens:**<br/>(a.media.ad.<br/>plaatsing)</li> <li> **Gegevensfeed:**<br/>N.v.t.</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.ad.placement)</li> </ul> |




## Metrische gegevens toevoegen {#ad-metrics}

### Ad Start

|   Implementatie | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>Automatisch instellen</li> <li> **API-sleutel:**<br/>N.v.t.</li> <li> **Vereist:**<br/>Ja</li> <li> **Type:**<br/>string</li> <li> **Verzonden met:**<br/>Ad Start</li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/>TRUE</li><li> **Beschrijving:**<br/>Aantal video&#39;s dat wordt gestart.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.ad.<br/>weergave)</li> <li> **Hartslag:**<br/>(s:event:type=start)<br/>(s:asset:type=ad)</li> </ul> | <ul> <li> **Beschikbaar:**<br/>Ja</li> <li> **Gereserveerde variabele:**<br/>event</li> <li> **Rapportnaam:**<br/>Advertentiestartpagina</li> <li> **Gegevensfeed:**<br/>N.v.t.</li> <li> **Contextgegevens:**<br/>(a.media.ad.<br/>weergave)</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.ad.view)</li> </ul> |



### Toevoegen voltooid

|   Implementatie | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>Automatisch instellen</li> <li> **API-sleutel:**<br/>N.v.t.</li> <li> **Vereist:**<br/>Ja</li> <li> **Type:**<br/>string</li> <li> **Verzonden met:**<br/>Advertentie sluiten</li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/>TRUE</li><li> **Beschrijving:**<br/>Aantal video&#39;s dat is voltooid.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.ad.<br/>complete)</li> <li> **Hartslag:**<br/>(s:event:type=complete)<br/>(s:asset:type=ad)</li> </ul> | <ul> <li> **Beschikbaar:**<br/>Ja</li> <li> **Gereserveerde variabele:**<br/>event</li> <li> **Rapportnaam:**<br/>Voltooien toevoegen</li> <li> **Gegevensfeed:**<br/>N.v.t.</li> <li> **Contextgegevens:**<br/>(a.media.ad.<br/>complete)</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.ad.complete)</li> </ul> |



### Toegevoegde tijd

|   Implementatie | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>Automatisch instellen</li> <li> **API-sleutel:**<br/>N.v.t.</li> <li> **Vereist:**<br/>Ja</li> <li> **Type:**<br/>string</li> <li> **Verzonden met:**<br/>Advertentie sluiten</li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/>15</li><li> **Beschrijving:**<br/>De totale hoeveelheid tijd, in seconden, die wordt besteed aan het bekijken van de advertentie (d.w.z. het aantal seconden dat wordt afgespeeld).  De waarde zal in het tijdformaat (HH:MM.:SS) in de Werkruimte van de Analyse en Rapporten &amp; Analytics worden getoond. In de Eigen Gegevens, het Pakhuis van Gegevens, en het Melden APIs zullen de waarden in seconden worden getoond.<br/>**Releasedatum: 13-09-18**</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.ad.<br/>timePlayed)</li> <li> **Hartslag:**<br/> </li> </ul> | <ul> <li> **Beschikbaar:**<br/>Ja</li> <li> **Gereserveerde variabele:**<br/>event</li> <li> **Rapportnaam:**<br/>Toegevoegde tijd</li> <li> **Gegevensfeed:**<br/>N.v.t.</li> <li> **Contextgegevens:**<br/>(a.media.ad.<br/>timePlayed)</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.ad.timePlayed)</li> </ul> |



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

* Android - [MediaHeartConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartboneConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html#toc0)

