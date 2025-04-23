---
title: Ad-parameters
description: Leer over advertentieparameters met inbegrip van de implementatie, het netwerk, en het melden van variabelen voor ad videogegevens.
uuid: 92cd7f97-bb5a-4de6-8946-453d30271d0f
exl-id: 949e86cb-d265-4836-8825-a06b87203b15
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: ebabbe52fe673e3fb6f13da40bbc3c87aef1c7bd
workflow-type: tm+mt
source-wordcount: '2038'
ht-degree: 0%

---

# Ad-parameters{#ad-parameters}

Dit onderwerp stelt een lijst van video en gegevens, met inbegrip van contextgegevenswaarden voor, die Adobe via oplossingsvariabelen verzamelt.

Beschrijving van tabelgegevens:

* **Implementatie:** Informatie over implementatiewaarden en vereisten
   * *Sleutel* - Veranderlijk, plaats of manueel in uw app, of automatisch door de Media SDK van Adobe.
   * *Vereist* - wijst erop of de parameter voor basisvideo het volgen wordt vereist.
   * *Type* - specificeert het type van de te plaatsen variabele, koord of aantal.
   * *Verzonden met* - wijst erop wanneer het gegeven wordt verzonden: *het Begin van Media* is de analysevraag die op media begin wordt verzonden, *en Begin* is de analytische vraag die op ad begin wordt verzonden, etc.; *dicht* vraag is de gecompileerde analytische vraag die rechtstreeks van de hartslagserver naar de analyseserver aan het eind van de media zitting, of het eind van de ad wordt verzonden , hoofdstuk, enz. De dichte vraag is niet beschikbaar in de vraag van het netwerkpakket.
   * *Min. SDK Versie* - wijst op welke versie van SDK u tot de parameter zou moeten toegang hebben.
   * *Waarde van de Steekproef* - verstrekt voorbeeld van gemeenschappelijk veranderlijk gebruik.
* **de Parameters van het Netwerk:** toont de waarden die tot Adobe Analytics of de servers van de Hartslag worden overgegaan. Deze kolom toont de namen van de parameters die in de netwerkvraag worden gezien die door de Media SDKs van Adobe wordt geproduceerd.
* **Meldend:** Informatie over hoe te om de videogegevens te bekijken en te analyseren.
   * *Beschikbaar* - Wijst erop of het gegeven in rapportering door gebrek (*ja*) beschikbaar is, of douane opstelling (*Douane* vereist)
   * *Gereserveerde Variabele* - wijst erop of het gegeven als gebeurtenis, eVar, pro, of classificatie in een gereserveerde variabele wordt gevangen.
   * *Naam van het Rapport* - Naam van het Analytische rapport van Adobe voor variabele
   * *Gegevens van de Context* - Naam van de de contextgegevens van Adobe Analytics die tot de rapporterende server worden overgegaan en in verwerkingsregels worden gebruikt.
   * *het Gegeven van Gegevens* - de naam van de Kolom voor variabele die in Clickstream of Levende de gegevensvoer van de Stream wordt gevonden
   * *Audience Manager* - De naam van het spoor die in Adobe Audience Manager wordt gevonden

>[!IMPORTANT]
>
>Wijzig de classificatienamen niet voor onderstaande variabelen die
>beschreven onder Rapportage/Gereserveerde variabele als &quot;classificatie&quot;.
>De mediaclassificaties worden gedefinieerd wanneer een rapportsuite is ingeschakeld voor media
>bijhouden. Van tijd tot tijd voegt Adobe nieuwe eigenschappen toe, en, wanneer dit voorkomt,
>klanten moeten hun rapportsuites opnieuw toelaten om toegang tot de nieuwe media te krijgen
>eigenschappen. Tijdens het updateproces bepaalt Adobe of de
>classificaties worden ingeschakeld door de namen van de variabelen te controleren. Indien een van de
>ze ontbreken, voegt Adobe de ontbrekende weer toe.

## Videogegevens toevoegen {#ad-video-data}

### ID advertentie

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Sleutel van SDK:**<br/> [ adId ](./ad-parameters.md#section_Related_APIs) </li> <li> **Sleutel API:**<br/> media.ad.id </li> <li> **Vereist:**<br/> ja </li> <li> **Type:**<br/> koord </li> <li> **verzonden met:**<br/> het Begin van de Advertentie, en sluit </li> <li> **Min. SDK-versie:** alle  </li> <li> **de Waarde van de Steekproef:**<br/> &quot;2125&quot; </li><li> **Beschrijving:**<br/> identiteitskaart van de advertentie. (Willekeurig geheel getal en/of lettercombinatie)  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/> naam) </li> <li> **Hartslag:**<br/> (<code> s :asset: ad_id</code>) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> ja </li> <li> **Gereserveerde Variabele:**<br/> eVar </li> <li> **Vervaldatum:**<br/> op VISIT </li> <li> **Naam van het Rapport:**<br/> Advertentie </li> <li> **Gegevens van de Context:**<br/> (a.media.ad.<br/> naam) </li> <li> **Diervoer van Gegevens:**<br/> videoad </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/> a.media.ad.name) </li> <li> **Weg van het Gebied XDM:** (Vervangen) <br/> advertentie.adAssetReference._id </li> <li> **Pad van het Gebied XDM van de Inzameling XDM:**<br/> mediaCollection.advertentieDetails.name </li> <li> **Meldend Pad van het Gebied XDM:**<br/> mediaReporting.advertentieDetails.name </li> </ul> |



### Positie advertentie in pod

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Sleutel van SDK:**<br/> [ positie ](./ad-parameters.md#section_Related_APIs) </li> <li> **Sleutel API:**<br/> media.ad.podPosition </li> <li> **Vereist:**<br/> ja </li> <li> **Type:**<br/> aantal </li> <li> **verzonden met:**<br/> het Begin van de Advertentie, en sluit </li> <li> **Min. SDK-versie:** alle </li> <li> **de Waarde van de Steekproef:**<br/> 1 </li><li> **Beschrijving:**<br/> de positie (index) van de advertentie binnen de ouder en onderbreking. De eerste advertentie heeft index 0, de tweede advertentie heeft index 1, enz.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/> podPosition) </li> <li> **Hartslag:**<br/> (<code> s :asset: pod_position</code>) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> ja </li> <li> **Gereserveerde Variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> op HIT </li> <li> **Naam van het Rapport:**<br/> Advertentie in Pod Pod </li> <li> **Gegevens van de Context:**<br/> (a.media.ad.<br/> podPosition) </li> <li> **Diervoer van Gegevens:**<br/> videoadinpod </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/> a.media.ad.po) </li> <li> **Pad van het Gebied XDM:** (Vervangen) <br/> advertentie.adAssetViewDetails.index </li> <li> **Pad van het Gebied XDM van de Inzameling:**<br/> mediaCollection.advertentieDetails.podPosition </li> <li> **Meldend Pad van het Gebied XDM:**<br/> mediaReporting.advertentieDetails.podPosition </li> </ul> |



### Advertentieduur

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Sleutel van SDK:**<br/>  [ lengte ](./ad-parameters.md#section_Related_APIs) </li> <li> **Sleutel API:**<br/> media.ad.length </li> <li> **Vereist:**<br/> ja </li> <li> **Type:**<br/> aantal </li> <li> **verzonden met:**<br/> het Begin van de Advertentie, en sluit </li> <li> **Min. SDK-versie:** 1.5.1 </li> <li> **de Waarde van de Steekproef:**<br/> &quot;15&quot;  </li><li> **Beschrijving:**<br/> Lengte van video en in seconden.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/> lengte) </li> <li> **Hartslag:**<br/> (<code> l :asset: ad_length</code>) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> ja </li> <li> **Gereserveerde Variabele:**<br/> eVar en classificatie </li> <li> **Verlopen:**<br/> op HIT </li> <li> **Naam van het Rapport:**<br/> de Lengte van de Advertentie en de Lengte van de Advertentie (veranderlijk) </li> <li> **Gegevens van de Context:**<br/> (a.media.ad.<br/> lengte) </li> <li> **Diervoer van Gegevens:**<br/> videoadlength </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/> a.media.ad.le) </li> <li> **Weg van het Gebied XDM:** (Vervangen) <br/> advertentie.adAssetReference.<br/>_xmpDM.duration </li> <li> **Pad van het Gebied XDM van de Inzameling XDM:**<br/> mediaCollection.advertentieDetails.length </li> <li> **die de Weg van het Gebied XDM melden:**<br/> mediaReporting.advertentieDetails.length </li> </ul> |



### Naam van advertentiespeler

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Sleutel van SDK:**<br/>  [ playerName ](./ad-parameters.md#section_Related_APIs) </li> <li> **Sleutel API:**<br/> media.ad.playerName </li> <li> **Vereist:**<br/> ja </li> <li> **Type:**<br/> koord </li> <li> **verzonden met:**<br/> het Begin van de Advertentie, en sluit </li> <li> **Min. SDK-versie:** alle </li> <li> **de Waarde van de Steekproef:**<br/> &quot;Bevel&quot; </li><li> **Beschrijving:**<br/> de naam van de speler verantwoordelijk voor het teruggeven van de advertentie.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/> playerName) </li> <li> **Hartslag:**<br/> (<code> s :sp: player_name</code>) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> ja </li> <li> **Gereserveerde Variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> op HIT </li> <li> **Naam van het Rapport:**<br/> de Naam van de Speler van de Advertentie </li> <li> **Gegevens van de Context:**<br/> (a.media.ad.<br/> playerName) </li> <li> **Diervoer van Gegevens:**<br/> videoadplayername </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/> a.media.ad.playerName) </li> <li> **Pad van het Gebied XDM:** (Vervangen) <br/> advertentie.adAssetViewDetails.playerName </li> <li> **Pad van het Gebied XDM van de Inzameling:**<br/> mediaCollection.advertentieDetails.<br/> playerName </li> <li> **Meldend Pad van het Gebied XDM:**<br/> mediaReporting.advertentieDetails.<br/> playerName </li> </ul> |



### Naam advertentie-einde

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Sleutel van SDK:**<br/>  [ naam ](./ad-parameters.md#section_Related_APIs) </li> <li> **Sleutel API:**<br/> media.ad.podFriendlyName </li> <li> **Vereist:**<br/> SDK: Ja; API: Nr. </li> <li> **Type:**<br/> koord </li> <li> **verzonden met:**<br/> het Begin van de Advertentie, en sluit </li> <li> **Min. SDK-versie:** alle </li> <li> **de Waarde van de Steekproef:**<br/> &quot;pre-rol&quot; </li><li> **Beschrijving:**<br/> de vriendschappelijke naam van het Ad Break.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/> podFriendlyName) </li> <li> **Hartslag:**<br/> (<code> s :asset: pod_name</code>) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> ja </li> <li> **Gereserveerde Variabele:**<br/> Classificatie </li> <li> **Naam van het Rapport:**<br/> Naam van de peul </li> <li> **Gegevens van de Context:**<br/> (a.media.ad.<br/> podFriendlyName) </li> <li> **Diervoer van Gegevens:**<br/> n.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/> a.media.ad.podFriendlyName) </li> <li> **Weg van het Gebied XDM:** (Vervangen) <br/> advertentie.adAssetViewDetails.<br/> adBreak._dc.title </li> <li> **Pad van het Gebied XDM van de Inzameling:**<br/> mediaCollection.advertentiePodDetails.<br/> Vriendnaam </li> <li> **Meldend Pad van het Gebied XDM:**<br/> mediaReporting.advertentiePodDetails.<br/> Vriendnaam </li> </ul> |



### Index van advertentiepunten

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Sleutel van SDK:**<br/>  [ positie ](./ad-parameters.md#section_Related_APIs) </li> <li> **Sleutel API:**<br/> media.ad.podIndex </li> <li> **Vereist:**<br/> ja </li> <li> **Type:**<br/> aantal </li> <li> **Verzonden met:**<br/> </li> <li> **Min. SDK-versie:** alle </li> <li> **de Waarde van de Steekproef:**<br/> 1 </li><li> **Beschrijving:**<br/> de index van de advertentierak binnen de inhoud die bij 1 begint. Dit bezit wordt gebruikt **slechts** door Media SDK om identiteitskaart van de Pod te produceren.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **Hartslag:**<br/> </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Nr </li> <li> **Gereserveerde Variabele:**<br/> n.v.t. </li> <li> **Naam van het Rapport:**<br/> n.v.t. </li> <li> **Contextgegevens:**<br/> </li> <li> **Diervoer van Gegevens:**<br/> n.v.t. </li> <li> **Audience Manager:**<br/> </li> <li> **Pad van het Gebied XDM:** (Vervangen) <br/> advertentie.adAssetViewDetails.index </li> <li> **Pad van het Gebied XDM van de Inzameling XDM:**<br/> mediaCollection.advertentiePodDetails.index </li> </ul> |



### Positie advertentie-einde

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Sleutel van SDK:**<br/>  [ startTime ](./ad-parameters.md#section_Related_APIs) </li> <li> **Sleutel API:**<br/> media.ad.podSecond </li> <li> **Vereist:**<br/> ja </li> <li> **Type:**<br/> aantal </li> <li> **verzonden met:**<br/> het Begin van de Advertentie, en sluit </li> <li> **Min. SDK-versie:** alle </li> <li> **Waarde van de Steekproef:**<br/> 90 </li><li> **Beschrijving:**<br/> de compensatie van de advertentieonderbreking binnen de inhoud, in seconden.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/> podSecond) </li> <li> **Hartslag:**<br/> (<code> l :asset: pod_offset</code>) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> ja </li> <li> **Gereserveerde Variabele:**<br/> Classificatie </li> <li> **de Naam van het Rapport:**<br/> PodPositie </li> <li> **Gegevens van de Context:**<br/> (a.media.ad.<br/> podSecond) </li> <li> **Diervoer van Gegevens:**<br/> n.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/> a.media.ad.podSecond) </li> <li> **Pad van het Gebied XDM:** (Vervangen) <br/> advertentie.adAssetViewDetails.adBreak.<br/> verschuiving </li> <li> **Pad van het Gebied XDM van de Inzameling:**<br/> mediaCollection.advertentiePodDetails.<br/> verschuiving </li> <li> **Meldend Pad van het Gebied XDM:**<br/> mediaReporting.advertentiePodDetails.<br/> verschuiving </li> </ul> |



### ID Advertentie-einde

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Sleutel van SDK:**<br/> automatisch plaatsen </li> <li> **API Sleutel:**<br/> n.v.t. </li> <li> **Vereist:**<br/> ja </li> <li> **Type:**<br/> koord </li> <li> **verzonden met:**<br/> het Begin van de Advertentie, en sluit </li> <li> **Min. SDK-versie:** alle </li> <li> **de Waarde van de Steekproef:**<br/> c4a577424c84067899b807c76722d495_1  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/> pod) </li> <li> **Hartslag:**<br/> (<code> s :asset: pod_id</code>) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> ja </li> <li> **Gereserveerde Variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> op HIT </li> <li> **Naam van het Rapport:**<br/> Advertentiepod </li> <li> **Gegevens van de Context:**<br/> (a.media.ad.<br/> pod) </li> <li> **Diervoer van Gegevens:**<br/> videoadpod </li> <li> **Audience Manager:**<br/> </li> <li> **Pad van het Gebied XDM:** (Vervangen) <br/> advertentie.adAssetViewDetails.adBreak._id </li> <li> **Meldend Pad van het Gebied XDM:**<br/> mediaReporting.advertentiePodDetails.<br/> ID </li> </ul> |



### Advertentienaam

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Sleutel van SDK:**<br/>  [ naam ](./ad-parameters.md#section_Related_APIs) </li> <li> **Sleutel API:**<br/> media.ad.name </li> <li> **Vereist:**<br/> Nr </li> <li> **Type:**<br/> koord </li> <li> **verzonden met:**<br/> het Begin van de Advertentie, en sluit </li> <li> **Min. SDK-versie:** 1.5.1 </li> <li> **de Waarde van de Steekproef:**<br/> &quot;Ford F-150&quot; </li><li> **Beschrijving:**<br/> vriendschappelijke naam van de advertentie.  In de rapportage is &quot;Advertentienaam&quot; de classificatie en &quot;Advertentienaam (variabele)&quot; de eVar.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/> vriendschappelijkeNaam) </li> <li> **Hartslag:**<br/> (<code> s :asset: ad_name</code>) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> ja </li> <li> **Gereserveerde Variabele:**<br/> eVar en classificatie </li> <li> **Verlopen:**<br/> op HIT </li> <li> **Naam van het Rapport:**<br/> Advertentienaam en Advertentienaam (veranderlijk) </li> <li> **Gegevens van de Context:**<br/> (a.media.ad.<br/> vriendschappelijkeNaam) </li> <li> **Diervoer van Gegevens:**<br/> videoadname </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/> a.media.ad.friendlyName) </li> <li> **Weg van het Gebied XDM:** (Vervangen) <br/> advertentie.adAssetReference._dc.title </li> <li> **Pad van het Gebied XDM van de Inzameling XDM:**<br/> mediaCollection.advertentieDetails.prettyName </li> <li> **Meldend Pad van het Gebied XDM:**<br/> mediaReporting.advertentieDetails.Friedname </li> </ul> |



## Standaard advertentiemetagegevens {#standard-ad-metadata}

### Adverteerder

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Sleutel van SDK:**<br/> ADVERTISER </li> <li> **Sleutel API:**<br/> media.ad.advertiser </li> <li> **Vereist:**<br/> Nr </li> <li> **Type:**<br/> koord </li> <li> **verzonden met:**<br/> het Begin van de Advertentie, en sluit </li> <li> **Min. SDK-versie:** 1.5.7 </li> <li> **de Waarde van de Steekproef:**<br/> </li><li> **Beschrijving:**<br/> Bedrijf/Merk het waarvan product in de advertentie wordt vermeld.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/> adverteerder) </li> <li> **Hartslag:**<br/> (<code> s :meta:</code><br/> a.media.ad.advertiser) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> ja </li> <li> **Gereserveerde Variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> op HIT </li> <li> **Naam van het Rapport:**<br/> <i> Advertiser </i> </li> <li> **Gegevens van de Context:**<br/> (a.media.ad.<br/> adverteerder) </li> <li> **Diervoer van Gegevens:**<br/> videoadadverteerder </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/> a.media.ad.advertiser) </li> <li> **Pad van het Gebied XDM:** (Vervangen) <br/> advertentie.adAssetReference.adverteerder </li> <li> **Pad van het Gebied XDM van de Inzameling XDM:**<br/> mediaCollection.advertentieDetails.adverteerder </li> <li> **Meldend Pad van het Gebied XDM:**<br/> mediaReporting.advertentieDetails.adverteerder </li> </ul> |



### Campagne-id

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Sleutel van SDK:**<br/> CAMPAIGN_ID </li> <li> **API Sleutel:**<br/> media.ad.campaignId </li> <li> **Vereist:**<br/> Nr </li> <li> **Type:**<br/> koord </li> <li> **verzonden met:**<br/> het Begin van de Advertentie, en sluit </li> <li> **Min. SDK-versie:** 1.5.7 </li> <li> **Waarde van de Steekproef:**<br/> Geheel, of naam (koord).  </li><li> **Beschrijving:**<br/> identiteitskaart van de advertentie campagne.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/> campagne) </li> <li> **Hartslag:**<br/> (<code> s :meta:</code><br/> a.media.ad.campaign) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> ja </li> <li> **Gereserveerde Variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> op HIT </li> <li> **Naam van het Rapport:**<br/> <i> Campagne-id </i> </li> <li> **Gegevens van de Context:**<br/> (a.media.ad.<br/> campagne) </li> <li> **Diervoer van Gegevens:**<br/> videoadcampagne </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/> a.media.ad.campaign) </li> <li> **Pad van het Gebied XDM:** (Vervangen) <br/> advertentie.adAssetReference.campagne </li> <li> **Pad van het Gebied XDM van de Inzameling:**<br/> mediaCollection.advertentieDetails.<br/> campagneID </li> <li> **Meldend Pad van het Gebied XDM:**<br/> mediaReporting.advertentieDetails.<br/> campagneID </li> </ul> |



### Creative-id

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Sleutel van SDK:**<br/> CREATIVE_ID </li> <li> **Sleutel API:**<br/> media.ad.creativeId </li> <li> **Vereist:**<br/> Nr </li> <li> **Type:**<br/> koord </li> <li> **verzonden met:**<br/> het Begin van de Advertentie, en sluit </li> <li> **Min. SDK-versie:** 1.5.7 </li> <li> **Waarde van de Steekproef:**<br/> Geheel, of naam (koord).  </li><li> **Beschrijving:**<br/> identiteitskaart van de advertentie creatief.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/> creatief) </li> <li> **Hartslag:**<br/> (<code> s :meta:</code><br/> a.media.ad.creative) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> ja </li> <li> **Gereserveerde Variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> op HIT </li> <li> **Naam van het Rapport:**<br/> <i> Creative-id </i> </li> <li> **Gegevens van de Context:**<br/> (a.media.ad.<br/> creatief) </li> <li> **Diervoer van Gegevens:**<br/> adclassificationcreative </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/> a.media.ad.creative) </li> <li> **Pad van het Gebied XDM:** (Vervangen) <br/> advertentie.adAssetReference.creativeID </li> <li> **Pad van het Gebied XDM van de Inzameling:**<br/> mediaCollection.advertentieDetails.creativeID </li> <li> **Meldend Pad van het Gebied XDM:**<br/> mediaReporting.advertentieDetails.creativeID </li> </ul> |



### Site-id

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Sleutel van SDK:**<br/> SITE_ID </li> <li> **Sleutel API:**<br/> media.ad.siteId </li> <li> **Vereist:**<br/> Nr </li> <li> **Type:**<br/> koord </li> <li> **verzonden met:**<br/> het Begin van de Advertentie, en sluit </li> <li> **Min. SDK-versie:** 1.5.7 </li> <li> **de Waarde van de Steekproef:**<br/> </li><li> **Beschrijving:**<br/> identiteitskaart van de advertentiesite.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/> site) </li> <li> **Hartslag:**<br/> (<code> s :meta:</code><br/> a.media.ad.site) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> <i> Aangepaste verwerkingsregel gebruiken </i> </li> <li> **Gereserveerde Variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> op HIT </li> <li> **Naam van het Rapport:**<br/> Douane </li> <li> **Gegevens van de Context:**<br/> (a.media.ad.<br/> site) </li> <li> **Diervoer van Gegevens:**<br/> n.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/> a.media.ad.site) </li> <li> **Pad van het Gebied XDM:** (Vervangen) <br/> advertentie.adAssetReference.siteID </li> <li> **Pad van het Gebied XDM van de Inzameling:**<br/> mediaCollection.advertentieDetails.siteID </li> <li> **Meldend Pad van het Gebied XDM:**<br/> mediaReporting.advertentieDetails.siteID </li> </ul> |



### CREATIVE URL

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Sleutel van SDK:**<br/> CREATIVE_URL </li> <li> **Sleutel API:**<br/> media.ad.creativeURL </li> <li> **Vereist:**<br/> Nr </li> <li> **Type:**<br/> koord </li> <li> **verzonden met:**<br/> het Begin van de Advertentie, en sluit </li> <li> **Min. SDK-versie:** 1.5.7 </li> <li> **de Waarde van de Steekproef:**<br/> </li><li> **Beschrijving:**<br/> URL van de advertentie creatief.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/> creativeURL) </li> <li> **Hartslag:**<br/> (<code> s :meta: &lt;c/ode> <br/> a.media.ad.creativeURL) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> <i> Aangepaste verwerkingsregel gebruiken </i> </li> <li> **Gereserveerde Variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> op HIT </li> <li> **Naam van het Rapport:**<br/> Douane </li> <li> **Gegevens van de Context:**<br/> (a.media.ad.<br/> creativeURL) </li> <li> **Diervoer van Gegevens:**<br/> n.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/> a.media.ad.creativeURL) </li> <li> **Pad van het Gebied XDM:** (Vervangen) <br/> advertentie.adAssetReference.creativeURL </li> <li> **Pad van het Gebied XDM van de Inzameling:**<br/> mediaCollection.advertentieDetails.<br/> creativeURL </li> <li> **Meldend Pad van het Gebied XDM:**<br/> mediaReporting.advertentieDetails.<br/> creativeURL </li> </ul> |



### Plaatsing-id

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Sleutel van SDK:**<br/> PLACEMENT_ID </li> <li> **API Sleutel:**<br/> media.ad.placementId </li> <li> **Vereist:**<br/> Nr </li> <li> **Type:**<br/> koord </li> <li> **verzonden met:**<br/> het Begin van de Advertentie, en sluit </li> <li> **Min. SDK-versie:** 1.5.7 </li> <li> **de Waarde van de Steekproef:**<br/> </li><li> **Beschrijving:**<br/> identiteitskaart van de Plaatsing van de advertentie.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/> plaatsing) </li> <li> **Hartslag:**<br/> (<code> s :meta:</code><br/> a.media.ad.placement) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> <i> Aangepaste verwerkingsregel gebruiken </i> </li> <li> **Gereserveerde Variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> op HIT </li> <li> **Naam van het Rapport:**<br/> Douane </li> <li> **Gegevens van de Context:**<br/> (a.media.ad.<br/> plaatsing) </li> <li> **Diervoer van Gegevens:**<br/> n.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/> a.media.ad.placement) </li> <li> **Pad van het Gebied XDM:** (Vervangen) <br/> advertentie.adAssetReference.placementID </li> <li> **Pad van het Gebied XDM van de Inzameling:**<br/> mediaCollection.advertentieDetails.<br/> placementID </li> <li> **Meldend Pad van het Gebied XDM:**<br/> mediaReporting.advertentieDetails.<br/> placementID </li> </ul> |




## Metrische gegevens toevoegen {#ad-metrics}

### Ad Start

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Sleutel van SDK:**<br/> automatisch plaatsen </li> <li> **API Sleutel:**<br/> n.v.t. </li> <li> **Vereist:**<br/> ja </li> <li> **Type:**<br/> koord </li> <li> **Verzonden met:**<br/> Advertentie Begin </li> <li> **Min. SDK-versie:** alle </li> <li> **de Waarde van de Steekproef:**<br/> WAAR </li><li> **Beschrijving:**<br/> Aantal video en begint.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/> weergave) </li> <li> **Hartslag:**<br/> (<code> s :event: type=start</code>) <br/> (<code> s :asset: type=ad <code>) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> ja </li> <li> **Gereserveerde Variabele:**<br/> gebeurtenis </li> <li> **de Naam van het Rapport:**<br/> Adt begint </li> <li> **Diervoer van Gegevens:**<br/> n.v.t. </li> <li> **Gegevens van de Context:**<br/> (a.media.ad.<br/> weergave) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/> a.media.ad.vinew) </li> <li> **Pad van het Gebied XDM:** (Vervangen) <br/> advertentie.start.value > 0 => &quot;WAAR&quot; </li> <li> **Meldend Pad van het Gebied XDM:**<br/> mediaReporting.advertentieDetails.isStarted </li> </ul> |



### Toevoegen voltooid

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Sleutel van SDK:**<br/> automatisch plaatsen </li> <li> **API Sleutel:**<br/> n.v.t. </li> <li> **Vereist:**<br/> ja </li> <li> **Type:**<br/> koord </li> <li> **Verzonden met:**<br/> en dicht </li> <li> **Min. SDK-versie:** alle </li> <li> **de Waarde van de Steekproef:**<br/> WAAR </li><li> **Beschrijving:**<br/> Aantal video en voltooit.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/> volledig) </li> <li> **Hartslag:**<br/> (<code> s :event: type=complete</code>) <br/> (<code> s :asset: type=ad</code>)  </li> </ul> | <ul> <li> **Beschikbaar:**<br/> ja </li> <li> **Gereserveerde Variabele:**<br/> gebeurtenis </li> <li> **de Naam van het Rapport:**<br/> voltooit toevoegt </li> <li> **Diervoer van Gegevens:**<br/> n.v.t. </li> <li> **Gegevens van de Context:**<br/> (a.media.ad.<br/> volledig) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/> a.media.ad.complete) </li> <li> **Pad van het Gebied XDM:** (Vervangen) <br/> advertentie.completes.value > 0 => &quot;WAAR&quot; </li> <li> **Meldend Pad van het Gebied XDM:**<br/> mediaReporting.advertentieDetails.<br/> isCompleted </li> </ul> |



### Toegevoegde tijd

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Sleutel van SDK:**<br/> automatisch plaatsen </li> <li> **API Sleutel:**<br/> n.v.t. </li> <li> **Vereist:**<br/> ja </li> <li> **Type:**<br/> koord </li> <li> **Verzonden met:**<br/> en dicht </li> <li> **Min. SDK-versie:** alle </li> <li> **Waarde van de Steekproef:**<br/> 15 </li><li> **Beschrijving:**<br/> de totale hoeveelheid tijd, in seconden, besteed het letten op de advertentie (d.w.z., het aantal gespeeld seconden).  De waarde zal in het tijdformaat (<code> worden getoond HH :MM: SS</code>) in Analysis Workspace en Reports &amp; Analytics. In Data Feeds, Data Warehouse en Reporting API&#39;s worden de waarden in seconden weergegeven.  <br/>**Datum van de Versie: 09/13/18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/> timePlayed) </li> <li> **Hartslag:**<br/> </li> </ul> | <ul> <li> **Beschikbaar:**<br/> ja </li> <li> **Gereserveerde Variabele:**<br/> gebeurtenis </li> <li> **Naam van het Rapport:**<br/> bestede tijd van de Advertentie </li> <li> **Diervoer van Gegevens:**<br/> videoadtime </li> <li> **Gegevens van de Context:**<br/> (a.media.ad.<br/> timePlayed) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/> a.media.ad.timePlayed) </li> <li> **Pad van het Gebied XDM:** (Vervangen) <br/> advertentie.timePlayed.value </li> <li> **Meldend Pad van het Gebied XDM:**<br/> mediaReporting.advertentieDetails.<br/> timePlayed </li> </ul> |



## Verwante API&#39;s {#section_Related_APIs}

### createAdObject-API&#39;s:

* Android - [ createAdObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdObject-java.lang.String-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [ createAdObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdObjectWithName:adId:position:length:)
* JavaScript - [ createAdObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdObject)

### createAdBreakObject-API&#39;s:

* Android - [ createAdBreakObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdBreakObject-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [ createAdBreakObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdBreakObjectWithName:position:startTime:)
* JavaScript - [ createAdBreakObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdBreakObject)

### MediaHeartboneConfig-API&#39;s:

* Android - [ MediaHeartbeatConfig ](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ ADBMediaHeartbeatConfig ](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [ MediaHeartbeatConfig ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html#toc0)
