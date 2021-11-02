---
title: Parameters voor kwaliteit
description: Leer meer over de QoE-parameters (Quality of Experience) die worden gebruikt om metagegevens van hoge kwaliteit vast te leggen.
uuid: 0d9fa764-edef-4178-8650-90c9a0852a57
exl-id: aac178dc-5a46-4ce3-80e9-ec82cbfbfff5
feature: Media Analytics, Variables
role: User, Admin, Data Engineer
source-git-commit: 6e01f55ac498d69a6f7eac4ac0086e276cc0dd8a
workflow-type: tm+mt
source-wordcount: '3106'
ht-degree: 2%

---

# Parameters voor kwaliteit{#quality-parameters}

Dit onderwerp stelt een lijst van kwaliteit van ervaringsgegevens (QoE/QoS), met inbegrip van de waarden van contextgegevens voor, die Adobe via oplossingsvariabelen verzamelt.

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

## Metagegevens kwaliteit {#quality-metadata}

### Gemiddelde bitsnelheid

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>  [bitsnelheid](./quality-parameters.md#related_apis_section) </li> <li> **API-sleutel:**<br/> media.qoe.bitrate </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> 800-899 </li><li> **Omschrijving:**<br/> De gemiddelde bitsnelheid (in kbps). De waarde is vooraf bepaalde emmers met intervallen 100 kbps. De gemiddelde bitsnelheid wordt berekend als het gewogen gemiddelde van alle bitsnelheidwaarden die betrekking hebben op de afspeelduur die tijdens een afspeelsessie is opgetreden.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bitrateAverageBucket) </li> <li> **Hartslag:**<br/> l:stream:bitsnelheid) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Gemiddelde bitsnelheid </li> <li> **Contextgegevens:**<br/> (a.media.qoe.<br/>bitrateAverageBucket) </li> <li> **Gegevensfeed:**<br/> videoqoebitrateaverageevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateAverageBucket) </li> <li> **XDM-veldpad:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverageBucket </li> </ul> |


### Te starten tijd

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> </li> <li> **API-sleutel:**<br/> media.qoe.timeToStart </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> 30 000 </li><li> **Omschrijving:**<br/> Deze waarde is standaard ingesteld op nul als u deze niet instelt via het object QoSO. U stelt deze waarde in milliseconden in. De waarde wordt weergegeven in de tijdnotatie (HH:MM:SS) in Analysis Workspace en Reports &amp; Analytics. In de Diervoeders van Gegevens, Data Warehouse, en Rapporterende APIs zullen de waarden in seconden worden getoond.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>timeToStart) </li> <li> **Hartslag:**<br/> l:stream:opstarten_tijd) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Te starten tijd </li> <li> **Contextgegevens:**<br/> (a.media.qoe.<br/>timeToStart) </li> <li> **Gegevensfeed:**<br/> videoqoetimetostartevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>timeToStart) </li> <li> **XDM-veldpad:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart.value </li> </ul> |


### Frames per seconde

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> </li> <li> **API-sleutel:**<br/> media.qoe.framesPerSecond </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> 24 </li><li> **Omschrijving:**<br/> De huidige waarde van de streamframesnelheid (in frames per seconde). Het gebied wordt in kaart gebracht aan het fps gebied op de dichte vraag en kan door verwerkingsregels worden betreden.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **Hartslag:**<br/> l:stream:fps) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Nee </li> <li> **Gereserveerde variabele:**<br/> N.v.t. </li> <li> **Rapportnaam:**<br/> N.v.t. </li> <li> **Contextdata:**<br/> </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> </li> <li> **XDM-veldpad:**<br/>  </li> </ul> |



### Gedropte frames

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> droppedFrames </li> <li> **API-sleutel:**<br/> media.qoe.droppedFrames </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> 3 </li><li> **Omschrijving:**<br/> Het aantal gedropte frames (Int). Deze waarde wordt berekend als de som van alle frames die tijdens een afspeelsessie zijn gedropt. Deze waarde wordt ontleend aan de laatste waarde van (l:stream:dropped_frames).  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>droppedFrameCount) </li> <li> **Hartslag:**<br/> l:stream:<br/>dropped_frames) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Gedropte frames </li> <li> **Contextgegevens:**<br/> (a.media.qoe.<br/>droppedFrameCount) </li> <li> **Gegevensfeed:**<br/> videoqoedroppedframecountevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>droppedFrameCount) </li> <li> **XDM-veldpad:**<br/>  media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames.value </li> </ul> |



### Buffergebeurtenissen

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> 2 </li><li> **Omschrijving:**<br/> Het aantal buffergebeurtenissen. Deze metrische waarde wordt berekend als een telling van de verschillende bufferstaten die tijdens een playbackzitting voorkwamen. Dit is een telling van hoeveel keer de speler een bufferstaat van andere staten ingaat, bijvoorbeeld, speel of pauzeert.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bufferCount) </li> <li> **Hartslag:**<br/> (s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Buffergebeurtenissen </li> <li> **Contextgegevens:**<br/> (a.media.qoe.<br/>bufferCount) </li> <li> **Gegevensfeed:**<br/> videoqoebuffercountevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bufferCount) </li> <li> **XDM-veldpad:**<br/>  media.mediaTimed.primaryAssetViewDetails.qoe.buffers.value </li> </ul> |



### Totale bufferduur

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** </li> <li> **Samplewaarde:**<br/> 30 </li><li> **Omschrijving:**<br/> De totale hoeveelheid tijd, in seconden, besteed het als buffer optreden voor. Deze waarde wordt berekend als de som van alle buffergebeurtenissen tijdens een afspeelsessie. De waarde wordt weergegeven in de tijdnotatie (HH:MM:SS) in Analysis Workspace en Reports &amp; Analytics. In de Diervoeders van Gegevens, Data Warehouse, en Rapporterende APIs zullen de waarden in seconden worden getoond. <br/>**Releasedatum: 13-09-18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bufferTime) </li> <li> **Hartslag:**<br/> l:event:duur) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Totale bufferduur </li> <li> **Contextgegevens:**<br/> (a.media.qoe.<br/>bufferTime) </li> <li> **Gegevensfeed:**<br/> videoqoebuffertimeevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bufferTime) </li> <li> **XDM-veldpad:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime.value </li> </ul> |



### Wijzigingen in bitsnelheid

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> </li> <li> **API-sleutel:**<br/> media.qoe.bitrateChange </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> 3 </li><li> **Omschrijving:**<br/> Het aantal wijzigingen in bitsnelheid (geheel getal). Deze waarde wordt berekend als de som van alle gebeurtenissen die zich tijdens een afspeelsessie hebben voorgedaan om de bitsnelheid te wijzigen.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bitrateChangeCount) </li> <li> **Hartslag:**<br/> (s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Wijzigingen in bitsnelheid </li> <li> **Contextgegevens:**<br/> (a.media.qoe.<br/>bitrateChangeCount) </li> <li> **Gegevensfeed:**<br/> videoqobitratechangecountevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateChangeCount) </li> <li> **XDM-veldpad:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges.value </li> </ul> |



### Fouten/foutgebeurtenissen

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> </li> <li> **API-sleutel:**<br/> </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> 1 </li><li> **Omschrijving:**<br/> Het aantal fouten is opgetreden (geheel getal). Deze waarde wordt berekend als de som van alle foutgebeurtenissen die tijdens een afspeelsessie zijn opgetreden.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>errorCount) </li> <li> **Hartslag:**<br/> (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Fouten </li> <li> **Contextgegevens:**<br/> (a.media.qoe.<br/>errorCount) </li> <li> **Gegevensfeed:**<br/> videoqoeerrorcountevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>errorCount) </li> <li> **XDM-veldpad:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.errors.value </li> </ul> |



### Fout-id&#39;s van speler-SDK

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> </li><li> **Omschrijving:**<br/> De unieke fout-id&#39;s die worden gegenereerd door de speler SDK. Klanten moeten de foutcodes/id&#39;s tijdens de implementatie opgeven via de API&#39;s met foutmeldingen.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>playerSdkErrors) </li> <li> **Hartslag:**<br/> (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Fout-id&#39;s van speler-SDK </li> <li> **Contextgegevens:**<br/> (a.media.qoe.<br/>playerSdkErrors) </li> <li> **Gegevensfeed:**<br/> videoqoeplayersdkerrors </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>playerSdkErrors) </li> <li> **XDM-veldpad:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.playerSdkErrors </li> </ul> |



### Externe fout-id&#39;s

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> </li><li> **Omschrijving:**<br/> De unieke fout-id&#39;s van externe bronnen, bijvoorbeeld CDN-fouten. Klanten moeten de foutcodes/id&#39;s tijdens de implementatie opgeven via de API&#39;s met foutmeldingen.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>externalErrors) </li> <li> **Hartslag:**<br/> (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Externe fout-id&#39;s </li> <li> **Contextgegevens:**<br/> (a.media.qoe.<br/>externalErrors) </li> <li> **Gegevensfeed:**<br/> videoTextExtendedError </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>externalErrors) </li> <li> **XDM-veldpad:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.externalSdkErrors </li> </ul> |



### Media SDK-fout-id&#39;s

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> </li><li> **Omschrijving:**<br/> De unieke fout-id&#39;s die door de Media SDK tijdens het afspelen worden gegenereerd.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>mediaSDKErrors) </li> <li> **Hartslag:**<br/> (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Aangepast </li> <li> **Contextgegevens:**<br/> (a.media.qoe.<br/>mediaSDKErrors) </li> <li> **Gegevensfeed:**<br/> mediaquExternalError </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>mediaSDKErrors) </li> <li> **XDM-veldpad:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.mediaSdkErrors </li> </ul><br/> |




### Einde sessie {#session-end}

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** 2,1 </li> <li> **Samplewaarde:**<br/> end </li><li> **Omschrijving:**<br/> De gebeurtenis end betekent dat SDK een dichte vraag naar het achtereind verzendt. Na ontvangst van deze gebeurtenis sluit de achterzijde de sessie voor deze video en wordt de video niet verder verwerkt. <br/>Als het medium tot 100% is voltooid, moet dit na `s:event:type=complete.` Zie [Inhoud voltooid](audio-video-parameters.md#content-complete) voor gerelateerde informatie. </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> (s:event:type=end) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Aangepaste verwerkingsregel gebruiken </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> N.v.t. </li> <li> **Contextdata:**<br/> </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> </li> <li> **XDM-veldpad:**<br/>  </li> </ul> |



## Kwaliteitswaarden {#quality-metrics}

### Te starten tijd

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> 30 000 </li><li> **Omschrijving:**<br/> Deze waarde is standaard ingesteld op nul als u deze niet instelt via het object QoSO. U stelt deze waarde in milliseconden in. De waarde wordt weergegeven in de tijdnotatie (HH:MM:SS) in Analysis Workspace en Reports &amp; Analytics. In de Diervoeders van Gegevens, Data Warehouse, en Rapporterende APIs zullen de waarden in seconden worden getoond. <br/>**Releasedatum: 13-09-18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>timeToStart) </li> <li> **Hartslag:**<br/> l:stream:opstarten_tijd) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Te starten tijd </li> <li> **Contextgegevens:**<br/> (a.media.qoe.<br/>timeToStart) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>timeToStart) </li> <li> **XDM-veldpad:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart.value </li> </ul> |



### Buffergebeurtenissen

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>  [opstarttijd](./quality-parameters.md#related_apis_section) </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> 2 </li><li> **Omschrijving:**<br/> Het aantal buffergebeurtenissen (geheel getal). Deze metrische waarde wordt berekend als een aantal buffergebeurtenissen die tijdens een playbackzitting voorkwamen.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bufferCount) </li> <li> **Hartslag:**<br/> (s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Buffergebeurtenissen </li> <li> **Contextgegevens:**<br/> (a.media.qoe.<br/>bufferCount) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bufferCount) </li> <li> **XDM-veldpad:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.buffers.value </li> </ul> |



### Totale bufferduur

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> 15 </li><li> **Omschrijving:**<br/> de totale hoeveelheid tijd die is besteed aan bufferen (seconden); geheel getal). Deze waarde wordt berekend als de som van alle buffergebeurtenissen tijdens een afspeelsessie. De waarde wordt weergegeven in de tijdnotatie (HH:MM:SS) in Analysis Workspace en Reports &amp; Analytics. In de Diervoeders van Gegevens, Data Warehouse, en Rapporterende APIs zullen de waarden in seconden worden getoond. <br/>**Releasedatum: 13-09-18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bufferTime) </li> <li> **Hartslag:**<br/> l:event:duur) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Totale bufferduur </li> <li> **Contextgegevens:**<br/> (a.media.qoe.<br/>bufferTime) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bufferTime) </li> <li> **XDM-veldpad:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime.value </li> </ul> |



### Wijzigingen in bitsnelheid

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> Gebeurtenis </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> &quot;3&quot; </li><li> **Omschrijving:**<br/> Het aantal wijzigingen in bitsnelheid. Deze waarde wordt berekend als de som van alle gebeurtenissen die zich tijdens een afspeelsessie hebben voorgedaan om de bitsnelheid te wijzigen.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bitrateChangeCount) </li> <li> **Hartslag:**<br/> (s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Wijzigingen in bitsnelheid </li> <li> **Contextgegevens:**<br/> (a.media.qoe.<br/>bitrateChangeCount) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateChangeCount) </li> <li> **XDM-veldpad:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges.value </li> </ul> |



### Fouten

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> 1 </li><li> **Omschrijving:**<br/> Het aantal fouten dat is opgetreden (geheel getal). Deze waarde wordt berekend als de som van alle foutgebeurtenissen die tijdens een afspeelsessie zijn opgetreden.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>errorCount) </li> <li> **Hartslag:**<br/> (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Foutgebeurtenissen </li> <li> **Contextgegevens:**<br/> (a.media.qoe.<br/>errorCount) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>errorCount) </li> <li> **XDM-veldpad:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.errors.value </li> </ul> |



### Gedropte frames

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> 1 </li><li> **Omschrijving:**<br/> Het aantal gedropte frames (geheel getal). Deze waarde wordt berekend als de som van alle frames die tijdens een afspeelsessie zijn gedropt.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>droppedFrameCount) </li> <li> **Hartslag:**<br/> l:stream:<br/>dropped_frames) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Gedropte frames </li> <li> **Contextgegevens:**<br/> (a.media.qoe.<br/>droppedFrameCount) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>droppedFrameCount) </li> <li> **XDM-veldpad:**<br/>  media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames.value </li> </ul> |



### Druppels voor starten

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> TRUE </li><li> **Omschrijving:**<br/> Het aantal keren dat een gebruiker de video heeft afgesloten voordat deze wordt gestart. Deze metrische waarde wordt alleen op 1 ingesteld als er geen inhoud is gerenderd, ongeacht advertenties.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>dropBeforeStart) </li> <li> **Hartslag:**<br/> (s:event:<br/>type=aa_start) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Druppels voor starten </li> <li> **Contextgegevens:**<br/> (a.media.qoe.<br/>dropBeforeStart) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>dropBeforeStart) </li> <li> **XDM-veldpad:**<br/>  media.mediaTimed.primaryAssetViewDetails.qoe.dropBeforeStarts.value >= 1 => &quot;TRUE&quot; </li> </ul> |



>[!IMPORTANT]
>
>Als deze gebeurtenis is ingesteld, is TRUE de enige mogelijke waarde. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.

### Door buffer beïnvloede stromen

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> TRUE </li><li> **Omschrijving:**<br/> Het aantal streams dat wordt beïnvloed door buffering. Deze metrische waarde wordt alleen ingesteld op 1 als er tijdens een afspeelsessie ten minste één buffergebeurtenis heeft plaatsgevonden.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>buffer) </li> <li> **Hartslag:**<br/> (s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Door buffer beïnvloede stromen </li> <li> **Contextgegevens:**<br/> (a.media.qoe.<br/>buffer) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>buffer) </li> <li> **XDM-veldpad:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.bufferImpmedStreams.value >= 1 => &quot;TRUE&quot; </li> </ul> |



>[!IMPORTANT]
>
>Als deze gebeurtenis is ingesteld, is TRUE de enige mogelijke waarde. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.

### Door bitsnelheidwijziging beïnvloede stromen

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> TRUE </li><li> **Omschrijving:**<br/> Het aantal streams waarin wijzigingen in bitsnelheid zijn opgetreden. Deze metrische waarde wordt alleen op 1 ingesteld als er tijdens een afspeelsessie ten minste één gebeurtenis voor het wijzigen van de bitsnelheid heeft plaatsgevonden.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bitrateChange) </li> <li> **Hartslag:**<br/> (s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Door bitsnelheidwijziging beïnvloede stromen </li> <li> **Contextgegevens:**<br/> (a.media.qoe.<br/>bitrateChange) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateChange) </li> <li> **XDM-veldpad:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChangeImpmedStreams.value >= 1 => &quot;TRUE&quot; </li> </ul> |



>[!IMPORTANT]
>
>Als deze gebeurtenis is ingesteld, is TRUE de enige mogelijke waarde. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.

### Gemiddelde bitsnelheid

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> 3200 </li><li> **Omschrijving:**<br/> De gemiddelde bitsnelheid (in kbps, geheel getal). Deze metrische waarde wordt berekend als gewogen gemiddelde van alle bitsnelheidwaarden met betrekking tot de afspeelduur die tijdens een afspeelsessie plaatsvond.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bitrateAverage) </li> <li> **Hartslag:**<br/> l:stream:bitsnelheid) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Gemiddelde bitsnelheid </li> <li> **Contextgegevens:**<br/> (a.media.qoe.<br/>bitrateAverage) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateAverage) </li> <li> **XDM-veldpad:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverage.value </li> </ul> |



### Fout beïnvloede stromen

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> TRUE </li><li> **Omschrijving:**<br/> Het aantal stromen waarin een foutengebeurtenis (d.w.z., `trackError` tijdens de afspeelsessie is aangeroepen, en een `type=error` hartslagaanroep is gegenereerd). </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>fout) </li> <li> **Hartslag:**<br/> (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Fout beïnvloede stromen </li> <li> **Contextgegevens:**<br/> (a.media.qoe.<br/>fout) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>fout) </li> <li> **XDM-veldpad:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.errorImpmedStreams.value > 0 => &quot;TRUE&quot; </li> </ul> |



>[!IMPORTANT]
>
>Als deze gebeurtenis is ingesteld, is TRUE de enige mogelijke waarde. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.

### Gedropte framestromen

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> TRUE </li><li> **Omschrijving:**<br/> Het aantal stromen waarin kaders werden gelaten vallen. Deze metrische waarde wordt slechts geplaatst aan 1 als minstens één kader tijdens een playbackzitting werd gelaten vallen.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>droppedFrames) </li> <li> **Hartslag:**<br/> l:stream:<br/>dropped_frames) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Gedropte framestromen </li> <li> **Contextgegevens:**<br/> (a.media.qoe.<br/>droppedFrames) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>droppedFrames) </li> <li> **XDM-veldpad:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrameImpmedStreams.value >= 1 => &quot;TRUE&quot; </li> </ul> |



>[!IMPORTANT]
>
>Als deze gebeurtenis is ingesteld, is TRUE de enige mogelijke waarde. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.

### Betrokken stromen stoppen

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** 1,5+ </li> <li> **Samplewaarde:**<br/> TRUE </li><li> **Omschrijving:**<br/> Het aantal streams waarin een gebeurtenis stagneerde heeft plaatsgevonden. Deze metrische waarde wordt ingesteld op 1 als er tijdens het afspelen ten minste één keer wordt vastgezet. Klanten moeten hun eigen verwerkingsregels maken om de waarde voor rapportage beschikbaar te hebben.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>kraal) </li> <li> **Hartslag:**<br/> (s:event:<br/>type=stall) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Aangepaste verwerkingsregel gebruiken </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Aangepast</li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Contextgegevens:**<br/> (a.media.qoe.<br/>kraal) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>kraal) </li> <li> **XDM-veldpad:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.stallingImpmedStreams.value >= 1 => &quot;TRUE&quot; </li> </ul><br/> |

>[!IMPORTANT]
>
>Als deze gebeurtenis is ingesteld, is TRUE de enige mogelijke waarde. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.

### Stalling Events

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** 1,5+ </li> <li> **Samplewaarde:**<br/> &quot;3&quot; </li><li> **Omschrijving:**<br/> Het aantal keren dat het afspelen tijdens een afspeelsessie is gestopt. Klanten moeten hun eigen verwerkingsregels maken om de waarde voor rapportage beschikbaar te hebben.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>stallCount) </li> <li> **Hartslag:**<br/> (s:event:<br/>type=stall) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Aangepaste verwerkingsregel gebruiken </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Aangepast</li> <li> **Contextgegevens:**<br/> (a.media.qoe.<br/>stallCount) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>stallCount) </li> <li> **XDM-veldpad:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.stalls.value </li> </ul><br/> |



### Totale stapelduur

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** 1,5+ </li> <li> **Samplewaarde:**<br/> 12 </li><li> **Omschrijving:**<br/> de totale tijd (seconden); (geheel getal) het afspelen is tijdens een afspeelsessie gestopt. Klanten moeten hun eigen verwerkingsregels maken om de waarde voor rapportage beschikbaar te hebben.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>stallTime) </li> <li> **Hartslag:**<br/> (s:event:<br/>type=stall) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Aangepaste verwerkingsregel gebruiken </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Aangepast</li> <li> **Contextgegevens:**<br/> (a.media.qoe.<br/>stallTime) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>stallTime) </li> <li> **XDM-veldpad:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.stallTime.value </li> </ul> <br/> |



## Verwante API&#39;s {#related_apis_section}

* Android - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createQoSObject-java.lang.Long-java.lang.Double-java.lang.Double-java.lang.Long-)
* iOS - [createQoSObjectWithBitrate](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)
* JavaScript - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)
