---
title: Parameters voor advertenties
description: null
uuid: 92cd7f97-bb5a-4de6-8946-453d30271d0f
translation-type: tm+mt
source-git-commit: f59738f48eeb80d3aaead1757abd2ba3785c40da
workflow-type: tm+mt
source-wordcount: '1867'
ht-degree: 3%

---


# Parameters voor advertenties{#ad-parameters}

Dit onderwerp stelt een lijst van video en gegevens, met inbegrip van de waarden van contextgegevens voor, die Adobe via oplossingsvariabelen verzamelt.

Beschrijving van tabelgegevens:

* **Implementatie:** informatie over implementatiewaarden en -vereisten
   * *Sleutel*  - Variabele, plaats of manueel in uw app, of automatisch door Adobe Media SDK.
   * *Vereist*  - Geeft aan of de parameter is vereist voor het bijhouden van basisvideo.
   * *Type*  - Geeft het type op van de variabele die moet worden ingesteld, de tekenreeks of het getal.
   * *Verzonden met*  - Geeft aan wanneer de gegevens worden verzonden:  *Media* Startis de analytische aanroep die op het begin van de media wordt verzonden,  *Ad* Startis de analytische aanroep die op ad start wordt verzonden, enzovoort; de  ** Closecalls zijn de gecompileerde analytische vraag die rechtstreeks van de hartslagserver naar de analyseserver aan het eind van de media zitting, of het eind van de advertentie, het hoofdstuk, enz. wordt verzonden. De dichte vraag is niet beschikbaar in de vraag van het netwerkpakket.
   * *Min. SDK-versie* - Geeft aan welke SDK-versie u toegang tot de parameter nodig hebt.
   * *Samplewaarde* : geeft een voorbeeld van algemeen variabelengebruik.
* **Netwerkparameters:** geeft de waarden weer die worden doorgegeven aan Adobe Analytics- of Hartslagservers. Deze kolom toont de namen van de parameters die in de netwerkvraag worden gezien die door Adobe Media SDKs wordt geproduceerd.
* **Rapportage:** informatie over het weergeven en analyseren van videogegevens.
   * *Beschikbaar*  - Geeft aan of de gegevens standaard beschikbaar zijn in rapportage (*Ja*) of dat aangepaste installatie vereist is (*Aangepast*)
   * *Gereserveerde variabele*  - Geeft aan of de gegevens zijn vastgelegd als een gebeurtenis, eVar, eigenschap of classificatie in een gereserveerde variabele.
   * *Rapportnaam*  - Naam van analyserapport van Adobe voor variabele
   * *Contextgegevens*  - Naam van de Adobe Analytics-contextgegevens die aan de rapportserver worden doorgegeven en in verwerkingsregels worden gebruikt.
   * *Gegevensfeed*  - Kolomnaam voor variabele gevonden in Clickstream- of Live Stream-gegevensfeeds
   * *Audience Manager*  - Naam van dienstreis aangetroffen in Adobe Audience Manager

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
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> [adId](./ad-parameters.md#section_Related_APIs) </li> <li> **API-sleutel:**<br/> media.ad.id </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Advertentie Begin, en Sluiten </li> <li> **Min. SDK-versie:** Willekeurige  </li> <li> **Samplewaarde:**<br/> &quot;2125&quot; </li><li> **Beschrijving:**<br/> id van de advertentie. (Willekeurig geheel getal en/of lettercombinatie)  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>name) </li> <li> **hartslag:**<br/> (s:asset:ad_id) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> BIJ BEZOEK </li> <li> **rapportnaam:**<br/> toevoegen </li> <li> **Contextgegevens:**<br/> (a.media.ad.<br/>name) </li> <li> **Gegevensfeed:**<br/> video </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.na) </li> </ul> |



### Positie advertentie in pod

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> [position](./ad-parameters.md#section_Related_APIs) </li> <li> **API-sleutel:**<br/> media.ad.podPosition </li> <li> **Vereist:**<br/> Ja </li> <li> **Tekst:**<br/> nummer </li> <li> **Verzonden met:**<br/> Advertentie Begin, en Sluiten </li> <li> **Min. SDK-versie:** Willekeurige </li> <li> **Samplewaarde:**<br/> 1 </li><li> **Beschrijving:**<br/> De positie (index) van de advertentie binnen het bovenliggende element en het einde. De eerste advertentie heeft index 0, de tweede advertentie heeft index 1, enz.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>podPosition) </li> <li> **hartslag:**<br/> (s:asset:pod_position) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **verlopen:**<br/> op HIT </li> <li> **rapportnaam:Pod**<br/> toevoegen </li> <li> **Contextgegevens:**<br/> (a.media.ad.<br/>podPosition) </li> <li> **Gegevensfeed:**<br/> videoinvoegpod </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podPosition) </li> </ul> |



### Advertentieduur

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>  [length](./ad-parameters.md#section_Related_APIs) </li> <li> **API-sleutel:**<br/> media.ad.length </li> <li> **Vereist:**<br/> Ja </li> <li> **Tekst:**<br/> nummer </li> <li> **Verzonden met:**<br/> Advertentie Begin, en Sluiten </li> <li> **Min. SDK-versie:** 1.5.1 </li> <li> **Samplewaarde:**<br/> &quot;15&quot;  </li><li> **Beschrijving:**<br/> duur van video en in seconden.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>length) </li> <li> **hartslag:**<br/> (l:asset:ad_length) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar en classificatie </li> <li> **verlopen:**<br/> op HIT </li> <li> **Rapportnaam:**<br/> Lengte toevoegen en Lengte toevoegen (variabele) </li> <li> **Contextgegevens:**<br/> (a.media.ad.<br/>lengte) </li> <li> **Gegevensfeed:**<br/> videolengte </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.length) </li> </ul> |



### Naam van advertentiespeler

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>  [playerName](./ad-parameters.md#section_Related_APIs) </li> <li> **API-sleutel:**<br/> media.ad.playerName </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Advertentie Begin, en Sluiten </li> <li> **Min. SDK-versie:** Willekeurige </li> <li> **Samplewaarde:**<br/> &quot;Bevriewiel&quot; </li><li> **Beschrijving:**<br/> De naam van de speler die verantwoordelijk is voor het renderen van de advertentie.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>playerName) </li> <li> **hartslag:**<br/> (s:sp:player_name) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **verlopen:**<br/> op HIT </li> <li> **Rapportnaam:naam**<br/> van advertentiespeler </li> <li> **Contextgegevens:**<br/> (a.media.ad.<br/>playerName) </li> <li> **Gegevensfeed:**<br/> videoadplayername </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.playerName) </li> </ul> |



### Naam advertentie-einde

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **API-sleutel:**<br/> media.ad.podFriendlyName </li> <li> **Vereist:**<br/> SDK: Ja; API: Nee. </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Advertentie Begin, en Sluiten </li> <li> **Min. SDK-versie:** Willekeurige </li> <li> **Samplewaarde:**<br/> &quot;pre-roll&quot; </li><li> **Omschrijving:**<br/> de vriendelijke naam van het advertentiepunt.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>podFriendlyName) </li> <li> **hartslag:**<br/> (s:element:pod_naam) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> classificatie </li> <li> **Rapportnaam:**<br/> podnaam </li> <li> **Contextgegevens:**<br/> (a.media.ad.<br/>podFriendlyName) </li> <li> **Gegevensfeed:**<br/> n.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podFriendlyName) </li> </ul> |



### Index van advertentiepunten

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>  [positie](./ad-parameters.md#section_Related_APIs) </li> <li> **API-sleutel:**<br/> media.ad.podPosition </li> <li> **Vereist:**<br/> Ja </li> <li> **Tekst:**<br/> nummer </li> <li> **Verzonden met:**<br/> </li> <li> **Min. SDK-versie:** Willekeurige </li> <li> **Samplewaarde:**<br/> 1 </li><li> **Beschrijving:**<br/> De index van het advertentie-einde binnen de inhoud die begint bij 1. Deze eigenschap wordt door de SDK van Media alleen **alleen** gebruikt om de pod-id te genereren.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **Hartslag:**<br/> </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Nee </li> <li> **Gereserveerde variabele:**<br/> n.v.t. </li> <li> **Rapportnaam:**<br/> n.v.t. </li> <li> **Contextdata:**<br/> </li> <li> **Gegevensfeed:**<br/> n.v.t. </li> <li> **Audience Manager:**<br/> </li> </ul> |



### Positie advertentie-einde

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>  [startTime](./ad-parameters.md#section_Related_APIs) </li> <li> **API-sleutel:**<br/> media.ad.podSecond </li> <li> **Vereist:**<br/> Ja </li> <li> **Tekst:**<br/> nummer </li> <li> **Verzonden met:**<br/> Advertentie Begin, en Sluiten </li> <li> **Min. SDK-versie:** Willekeurige </li> <li> **Samplewaarde:**<br/> 90 </li><li> **Beschrijving:**<br/> De verschuiving van het advertentieeinde binnen de inhoud, in seconden.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>podSecond) </li> <li> **Hartslag:**<br/> (l:element:pod_offset) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> classificatie </li> <li> **Rapportnaam:**<br/> Podpositie </li> <li> **Contextgegevens:**<br/> (a.media.ad.<br/>podSecond) </li> <li> **Gegevensfeed:**<br/> n.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podSecond) </li> </ul> |



### ID advertentie-einde

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Advertentie Begin, en Sluiten </li> <li> **Min. SDK-versie:** Willekeurige </li> <li> **Samplewaarde:**<br/> c4a577424c84067899b807c76722d495_1  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>pod) </li> <li> **hartslag:**<br/> (s:asset:pod_id) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **verlopen:**<br/> op HIT </li> <li> **Rapportnaam:**<br/> advertentiepod </li> <li> **Contextgegevens:**<br/> (a.media.ad.<br/>pod) </li> <li> **Gegevensfeed:**<br/> videopod </li> <li> **Audience Manager:**<br/> </li> </ul> |



### Advertentienaam

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **API-sleutel:**<br/> media.ad.name </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Advertentie Begin, en Sluiten </li> <li> **Min. SDK-versie:** 1.5.1 </li> <li> **Samplewaarde:**<br/> &quot;Ford F-150&quot; </li><li> **Beschrijving:**<br/> Vriendelijke naam van de advertentie.  Bij de rapportage is &quot;Advertentienaam&quot; de classificatie en &quot;Advertentienaam (variabele)&quot; de eVar.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>vriendelijkeName) </li> <li> **hartslag:**<br/> (s:asset:ad_name) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar en classificatie </li> <li> **verlopen:**<br/> op HIT </li> <li> **Rapportnaam:Naam en naam**<br/> toevoegen (variabele) </li> <li> **Contextgegevens:**<br/> (a.media.ad.<br/>vriendelijkeName) </li> <li> **Gegevensfeed:**<br/> n.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.friendlyName) </li> </ul> |



## Standaard Advertentiemetagegevens {#standard-ad-metadata}

### Adverteerder

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> ADVERTISER </li> <li> **API-sleutel:**<br/> media.ad.advertiser </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Advertentie Begin, en Sluiten </li> <li> **Min. SDK-versie:** 1.5.7 </li> <li> **Samplewaarde:**<br/> </li><li> **Omschrijving:**<br/> Bedrijf/Merk waarvan het product in de advertentie is vermeld.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>adverteerder) </li> <li> **Hartslag:**<br/> (s:meta:<br/>a.media.ad.advertiser) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **verlopen:**<br/> op HIT </li> <li> **Rapportnaam:**<br/> <i>Adverteerder  </i> </li> <li> **Contextgegevens:**<br/> (a.media.ad.<br/>adverteerder) </li> <li> **Gegevensfeed:**<br/> videoadverteerder </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.advertiser) </li> </ul> |



### Campagne-id

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> CAMPAIGN_ID </li> <li> **API-sleutel:**<br/> media.ad.campaignId </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Advertentie Begin, en Sluiten </li> <li> **Min. SDK-versie:** 1.5.7 </li> <li> **Samplewaarde:**<br/> Geheel getal of naam (tekenreeks).  </li><li> **Beschrijving:**<br/> id van de advertentiecampagne.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>campaign) </li> <li> **hartslag:**<br/> (s:meta:<br/>a.media.ad.campaign) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **verlopen:**<br/> op HIT </li> <li> **Rapportnaam:**<br/> <i>Campagne-id </i> </li> <li> **Contextgegevens:**<br/> (a.media.ad.<br/>campagne) </li> <li> **gegevensfeed:**<br/> videocampagne </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.campaign) </li> </ul> |



### Creative-id

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> CREATIVE_ID </li> <li> **API-sleutel:**<br/> media.ad.creativeId </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Advertentie Begin, en Sluiten </li> <li> **Min. SDK-versie:** 1.5.7 </li> <li> **Samplewaarde:**<br/> Geheel getal of naam (tekenreeks).  </li><li> **Beschrijving:**<br/> id van de advertentie.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>creatief) </li> <li> **Hartslag:**<br/> (s:meta:<br/>a.media.ad.creative) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **verlopen:**<br/> op HIT </li> <li> **Rapportnaam:**<br/> <i>Creative-id  </i> </li> <li> **Contextgegevens:**<br/> (a.media.ad.<br/>creatief) </li> <li> **gegevensfeed:**<br/> adclassificationcreative </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.creative) </li> </ul> |



### Site-id

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> SITE_ID </li> <li> **API-sleutel:**<br/> media.ad.siteId </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Advertentie Begin, en Sluiten </li> <li> **Min. SDK-versie:** 1.5.7 </li> <li> **Samplewaarde:**<br/> </li><li> **Beschrijving:**<br/> id van de advertentiesite.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>site) </li> <li> **Hartslag:**<br/> (s:meta:<br/>a.media.ad.site) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> <i>Aangepaste verwerkingsregel gebruiken  </i> </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **verlopen:**<br/> op HIT </li> <li> **Rapportnaam:**<br/> Aangepast* </li> <li> **Contextgegevens:**<br/> (a.media.ad.<br/>site) </li> <li> **Gegevensfeed:**<br/> n.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.site) </li> </ul> * Aangepaste verwerkingsregel gebruiken |



### Creative URL

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> CREATIVE_URL </li> <li> **API-sleutel:**<br/> media.ad.creativeURL </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Advertentie Begin, en Sluiten </li> <li> **Min. SDK-versie:** 1.5.7 </li> <li> **Samplewaarde:**<br/> </li><li> **Beschrijving:**<br/> URL van de advertentie.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>creativeURL) </li> <li> **Hartslag:**<br/> (s:meta:<br/>a.media.ad.creativeURL) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> <i>Aangepaste verwerkingsregel gebruiken  </i> </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **verlopen:**<br/> op HIT </li> <li> **Rapportnaam:**<br/> Aangepast* </li> <li> **Contextgegevens:**<br/> (a.media.ad.<br/>creativeURL) </li> <li> **Gegevensfeed:**<br/> n.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.creativeURL) </li> </ul> * Aangepaste verwerkingsregel gebruiken |



### Plaatsing-id

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> PLACEMENT_ID </li> <li> **API-sleutel:**<br/> media.ad.placementId </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Advertentie Begin, en Sluiten </li> <li> **Min. SDK-versie:** 1.5.7 </li> <li> **Samplewaarde:**<br/> </li><li> **Beschrijving:**<br/> Plaatsing-id van de advertentie.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>plaatsing) </li> <li> **Hartslag:**<br/> (s:meta:<br/>a.media.ad.placement) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> <i>Aangepaste verwerkingsregel gebruiken  </i> </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **verlopen:**<br/> op HIT </li> <li> **Rapportnaam:**<br/> Aangepast* </li> <li> **Contextgegevens:**<br/> (a.media.ad.<br/>plaatsing) </li> <li> **Gegevensfeed:**<br/> n.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.placement) </li> </ul>* Aangepaste verwerkingsregel gebruiken |




## Metrisch {#ad-metrics} toevoegen

### Ad Start

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Advertentie starten </li> <li> **Min. SDK-versie:** Willekeurige </li> <li> **Samplewaarde:**<br/> TRUE </li><li> **Beschrijving:**<br/> Aantal video&#39;s dat wordt gestart.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>weergave) </li> <li> **Hartslag:**<br/>  (s:event:type=start)<br/> (s:asset:type=ad) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> gebeurtenis </li> <li> **rapportnaam:**<br/> Advertentie starten </li> <li> **Gegevensfeed:**<br/> n.v.t. </li> <li> **Contextgegevens:**<br/> (a.media.ad.<br/>weergave) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.view) </li> </ul> |



### Toevoegen voltooid

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Advertentie sluiten </li> <li> **Min. SDK-versie:** Willekeurige </li> <li> **Samplewaarde:**<br/> TRUE </li><li> **Beschrijving:**<br/> Aantal video&#39;s dat is voltooid.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>complete) </li> <li> **Hartslag:**<br/> (s:event:type=complete)<br/> (s:asset:type=ad)  </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> gebeurtenis </li> <li> **rapportnaam:**<br/> Advertentievullen </li> <li> **Gegevensfeed:**<br/> n.v.t. </li> <li> **Contextgegevens:**<br/> (a.media.ad.<br/>complete) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.complete) </li> </ul> |



### Toegevoegde tijd

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Advertentie sluiten </li> <li> **Min. SDK-versie:** Willekeurige </li> <li> **Samplewaarde:**<br/> 15 </li><li> **Beschrijving:**<br/> De totale hoeveelheid tijd, in seconden, die wordt besteed aan het bekijken van de advertentie (d.w.z. het aantal seconden dat wordt afgespeeld).  De waarde wordt weergegeven in de tijdnotatie (HH:MM:SS) in Analysis Workspace en Reports &amp; Analytics. In de Diervoeders van Gegevens, Data Warehouse, en Rapporterende APIs zullen de waarden in seconden worden getoond.  <br/>**Releasedatum: 13-09-18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>timePlayed) </li> <li> **Hartslag:**<br/> </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> gebeurtenis </li> <li> **rapportnaam:**<br/> bestede tijd toevoegen </li> <li> **Gegevensfeed:**<br/> n.v.t. </li> <li> **Contextgegevens:**<br/> (a.media.ad.<br/>timePlayed) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.timePlayed) </li> </ul> |



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

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartboneConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html#toc0)
