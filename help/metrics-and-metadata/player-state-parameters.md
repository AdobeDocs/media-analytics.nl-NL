---
title: Parameters van de Player-status
description: In dit onderwerp worden parameters voor het bijhouden van spelerstatussen beschreven.
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
translation-type: tm+mt
source-git-commit: c23a8787a8f59746665702eb5e2e74dde2c213e8
workflow-type: tm+mt
source-wordcount: '2167'
ht-degree: 0%

---


# Parameters van de Player-status{#player-state-parameters}

Dit onderwerp bevat een lijst met gegevens over de spelerstatus die Adobe verzamelt via oplossingsvariabelen.

Beschrijving van tabelgegevens:

* **Implementatie:** Informatie over implementatiewaarden en -vereisten
   * *Sleutel* - Variabel, stelt u deze handmatig in uw app in of automatisch in door de SDK van Adobe Media.
   * *Vereist* - Geeft aan of de parameter is vereist voor het bijhouden van basisvideo.
   * *Type* - Geeft het type op van de variabele die moet worden ingesteld, de tekenreeks of het getal.
   * *Verzonden met* - Geeft aan wanneer de gegevens worden verzonden: *Het Begin* van media is de analytische vraag die op media begin wordt verzonden, *Ad Begin* is de analytische vraag die op ad start wordt verzonden, etc. de *Dichte* vraag is de gecompileerde analytische vraag die rechtstreeks van de hartslagserver naar de analyseserver aan het eind van de media zitting, of het eind van de advertentie, het hoofdstuk, enz. wordt verzonden. De dichte vraag is niet beschikbaar in de vraag van het netwerkpakket.
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
>Wijzig de classificatienamen niet voor onderstaande variabelen die onder Rapportage/Gereserveerde variabele worden beschreven als &quot;classificatie&quot;.\
>De mediaclassificaties worden gedefinieerd wanneer een rapportsuite is ingeschakeld voor het bijhouden van media. Adobe voegt van tijd tot tijd nieuwe eigenschappen toe en wanneer dit gebeurt, moeten klanten hun rapportsuites opnieuw inschakelen om toegang tot de nieuwe media-eigenschappen te krijgen. Tijdens het updateproces bepaalt Adobe of de classificaties zijn ingeschakeld door de namen van de variabelen te controleren. Als een van deze ontbrekende items ontbreekt, voegt Adobe de ontbrekende items opnieuw toe.

## Eigenschappen van spelerstatus {#player-state-properties}

De mogelijkheden voor het bijhouden van de spelerstatus kunnen worden gekoppeld aan een audio- of videostream. De gestandaardiseerde metriek voor het bijhouden van spelerstatussen worden opgeslagen als oplossingsvariabelen. De standaardstatussen zijn: fullScreen, dempen, closeCaption, pictureInPicture en inFocus.

### Eigenschappen van Volledig scherm

#### Streams beïnvloed door volledig scherm

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel **<br/>automatisch instellen</li> <li> **API-sleutel **<br/>N.v.t.</li> <li> **Vereist **<br/>nr.</li> <li> **Type **<br/>nummer</li> <li> **Verzonden met **<br/>Media Sluiten</li> <li> **Min. SDK-versie **<br/>3.0</li> <li> **Samplewaarde **<br/>TRUE</li><li> ****<br/>BeschrijvingHet aantal streams dat wordt beïnvloed door Volledig scherm. Deze metrische waarde wordt slechts ingesteld op 1 als minstens één Volledige staat van het Scherm tijdens een playbackzitting voorkwam.<br/> **Belangrijk** <br/> : als deze gebeurtenis is ingesteld, is TRUE de enige mogelijke waarde. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.fullscreen.set)<br/></li> <li> **Hartslag **<br/>N.V.</li> </ul> | <ul> <li> **Beschikbaar **<br/>Ja</li> <li> **Gereserveerde variabele **<br/>, gebeurtenis</li> <li> **De stromen van de Naam **<br/>van het rapport beïnvloedden door het Volledige Scherm</li> <li> **Contextgegevens **<br/>(a.media.states.fullscreen.set)<br/> </li> <li> **Data Feed **<br/>media.states.fullscreen</li> <li> **Audience Manager **<br/>(c_contextdata.a.media.states.fullscreen.set)</li> </ul> |

#### Aantal op volledig scherm

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel **<br/>automatisch instellen</li> <li> **API-sleutel **<br/>N.v.t.</li> <li> **Vereist **<br/>nr.</li> <li> **Type **<br/>nummer</li> <li> **Verzonden met **<br/>Media Sluiten</li> <li> **Min. SDK-versie **<br/>3.0</li> <li> **Samplewaarde **<br/>TRUE</li><li> ****<br/>BeschrijvingHet aantal keren dat een volledig scherm werd weergegeven. Deze metrische waarde wordt slechts ingesteld op 1 als minstens één Volledige staat van het Scherm tijdens een playbackzitting voorkwam.<br/> **Belangrijk **<br/>als deze gebeurtenis is ingesteld, is het aantal keer dat de video zich in de status Volledig scherm bevond. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.fullscreen.count)<br/></li> <li> **Hartslag **<br/>N.V.</li> </ul> | <ul> <li> **Beschikbaar **<br/>Ja</li> <li> **Gereserveerde variabele **<br/>, gebeurtenis</li> <li> **Rapportnaam **<br/>Volledig scherm</li> <li> **Contextgegevens **<br/>(media.states.fullscreen.count)<br/> </li> <li> **Data Feed **<br/>media.states.fullscreen.count</li> <li> **Audience Manager **<br/>(c_contextdata.media.states.fullscreen.count)</li> </ul> |



#### Totale duur volledig scherm

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel **<br/>automatisch instellen</li> <li> **API-sleutel **<br/>N.v.t.</li> <li> **Vereist **<br/>nr.</li> <li> **Type **<br/>nummer</li> <li> **Verzonden met **<br/>Media Sluiten</li> <li> **Min. SDK-versie **<br/>3.0</li> <li> **Samplewaarde **<br/>TRUE</li><li> ****<br/>BeschrijvingDe tijdsduur dat een volledig scherm werd weergegeven. Deze metrische waarde wordt slechts ingesteld op 1 als minstens één Volledige staat van het Scherm tijdens een playbackzitting voorkwam.<br/> **Belangrijk **<br/>als deze gebeurtenis is ingesteld, is de tijd gelijk aan de duur van de video in de status Volledig scherm. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.fullscreen.time)<br/></li> <li> **Hartslag **<br/>N.V.</li> </ul> | <ul> <li> **Beschikbaar **<br/>Ja</li> <li> **Gereserveerde variabele **<br/>, gebeurtenis</li> <li> **Rapportnaam **<br/>Totale duur volledig scherm</li> <li> **Contextgegevens **<br/>(media.states.fullscreen.time)<br/> </li> <li> **Data Feed **<br/>media.states.fullscreen.time</li> <li> **Audience Manager **<br/>(c_contextdata.media.states.fullscreen.time)</li> </ul> |


### Eigenschappen bijschrift sluiten

#### Streams die worden beïnvloed door ondertiteling

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel **<br/>automatisch instellen</li> <li> **API-sleutel **<br/>N.v.t.</li> <li> **Vereist **<br/>nr.</li> <li> **Type **<br/>nummer</li> <li> **Verzonden met **<br/>Media Sluiten</li> <li> **Min. SDK-versie **<br/>3.0</li> <li> **Samplewaarde **<br/>TRUE</li><li> ****<br/>BeschrijvingHet aantal stromen die door Gesloten Captioning worden beïnvloed. Deze metrische waarde wordt slechts geplaatst aan 1 als minstens één Gesloten Staat van de Titel tijdens een playbackzitting voorkwam.<br/> **Belangrijk** <br/> : als deze gebeurtenis is ingesteld, is TRUE de enige mogelijke waarde. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.closedCaptioning.set)<br/></li> <li> **Hartslag **<br/>N.V.</li> </ul> | <ul> <li> **Beschikbaar **<br/>Ja</li> <li> **Gereserveerde variabele **<br/>, gebeurtenis</li> <li> **Rapportnaamstromen **<br/>die worden beïnvloed door ondertiteling</li> <li> **Contextgegevens **<br/>(a.media.states.closedCaptioning.set)<br/> </li> <li> **Data Feed **<br/>media.states.closedcaptioning</li> <li> **Audience Manager **<br/>(c_contextdata.a.media.states.closedCaptioning.set)</li> </ul> |


#### Aantal ondertitelingen

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel **<br/>automatisch instellen</li> <li> **API-sleutel **<br/>N.v.t.</li> <li> **Vereist **<br/>nr.</li> <li> **Type **<br/>nummer</li> <li> **Verzonden met **<br/>Media Sluiten</li> <li> **Min. SDK-versie **<br/>3.0</li> <li> **Samplewaarde **<br/>TRUE</li><li> ****<br/>BeschrijvingHet aantal keren dat Closed Captioning is weergegeven. Deze metrische waarde wordt slechts geplaatst aan 1 als minstens één Gesloten Captioning Staat tijdens een playbackzitting voorkwam.<br/> **Belangrijk **<br/>als deze gebeurtenis is ingesteld, is het aantal gelijk aan het aantal keren dat de video zich in de status Closed Captioning bevond. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(C19)<br/></li> <li> **Hartslag **<br/>N.V.</li> </ul> | <ul> <li> **Beschikbaar **<br/>Ja</li> <li> **Gereserveerde variabele **<br/>, gebeurtenis</li> <li> **Rapportnaam **<br/>Aantal ondertitelingen</li> <li> **Contextgegevens **<br/>(media.states.closedcaptioning.count)<br/> </li> <li> **Data Feed **<br/>media.states.closedcaptioning.count</li> <li> **Audience Manager **<br/>(c_contextdata.media.states.closedcaptioning.count)</li> </ul> |


#### Totale duur van ondertiteling

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel **<br/>automatisch instellen</li> <li> **API Key **<br/>N/A</li> <li> **Vereist **<br/>nr.</li> <li> **Type **<br/>nummer</li> <li> **Verzonden met **<br/>Media Sluiten</li> <li> **Min. SDK-versie **<br/>3.0</li> <li> **Samplewaarde **<br/>TRUE</li><li> ****<br/>BeschrijvingDe tijdsduur voor Ondertiteling is weergegeven. This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **Belangrijk **<br/>als deze gebeurtenis is ingesteld, is de tijd gelijk aan de duur van de video in de status Closed Captioning. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.closedcaptioning.time)<br/></li> <li> **Hartslag **<br/>N.V.</li> </ul> | <ul> <li> **Beschikbaar **<br/>Ja</li> <li> **Gereserveerde variabele **<br/>, gebeurtenis</li> <li> **De Naam **<br/>van het rapport Gesloten Captioning Totale Duur</li> <li> **Contextgegevens **<br/>(media.states.closedcaptioning.time)<br/> </li> <li> **Data Feed **<br/>media.states.closedcaptioning.time</li> <li> **Audience Manager **<br/>(c_contextdata.media.states.closedCaptioning.time)</li> </ul> |


### Eigenschappen dempen

#### Streams beïnvloed door Dempen

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel **<br/>automatisch instellen</li> <li> **API-sleutel **<br/>N.v.t.</li> <li> **Vereist **<br/>nr.</li> <li> **Type **<br/>nummer</li> <li> **Verzonden met **<br/>Media Sluiten</li> <li> **Min. SDK-versie **<br/>3.0</li> <li> **Samplewaarde **<br/>TRUE</li><li> ****<br/>BeschrijvingHet aantal streams dat door Dempen wordt beïnvloed. Deze metrische waarde wordt ingesteld op 1 alleen als ten minste één dempingsstatus is opgetreden tijdens een afspeelsessie.<br/> **Belangrijk** <br/> : als deze gebeurtenis is ingesteld, is TRUE de enige mogelijke waarde. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.mute.set)<br/></li> <li> **Hartslag **<br/>N.V.</li> </ul> | <ul> <li> **Beschikbaar **<br/>Ja</li> <li> **Gereserveerde variabele **<br/>, gebeurtenis</li> <li> **Rapportnaamstromen **<br/>beïnvloed door Dempen</li> <li> **Contextgegevens **<br/>(a.media.states.mute.set)<br/> </li> <li> **Data Feed **<br/>media.states.mute</li> <li> **Audience Manager **<br/>(c_contextdata.a.media.states.mute.set)</li> </ul> |

#### Aantal dempen

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel **<br/>automatisch instellen</li> <li> **API-sleutel **<br/>N.v.t.</li> <li> **Vereist **<br/>nr.</li> <li> **Type **<br/>nummer</li> <li> **Verzonden met **<br/>Media Sluiten</li> <li> **Min. SDK-versie **<br/>3.0</li> <li> **Samplewaarde **<br/>TRUE</li><li> ****<br/>BeschrijvingHet aantal keren dat Dempen is weergegeven. Deze metrische waarde wordt ingesteld op 1 alleen als ten minste één dempingsstatus is opgetreden tijdens een afspeelsessie.<br/> **Belangrijk **<br/>Als deze gebeurtenis is ingesteld, is het aantal gelijk aan het aantal keer dat de video in de toestand Dempen is geweest. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.mute.count)<br/></li> <li> **Hartslag **<br/>N.V.</li> </ul> | <ul> <li> **Beschikbaar **<br/>Ja</li> <li> **Gereserveerde variabele **<br/>, gebeurtenis</li> <li> **Aantal dempen van **<br/>rapportnaam</li> <li> **Contextgegevens **<br/>(media.states.mute.count)<br/> </li> <li> **Data Feed **<br/>media.states.mute.count</li> <li> **Audience Manager **<br/>(c_contextdata.media.states.mute.count)</li> </ul> |

#### Totale duur dempen

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel **<br/>automatisch instellen</li> <li> **API-sleutel **<br/>N.v.t.</li> <li> **Vereist **<br/>nr.</li> <li> **Type **<br/>nummer</li> <li> **Verzonden met **<br/>Media Sluiten</li> <li> **Min. SDK-versie **<br/>3.0</li> <li> **Samplewaarde **<br/>TRUE</li><li> ****<br/>BeschrijvingDe tijdsduur van Dempen is weergegeven. Deze metrische waarde wordt ingesteld op 1 alleen als ten minste één dempingsstatus is opgetreden tijdens een afspeelsessie.<br/> **Belangrijk **<br/>Als deze gebeurtenis is ingesteld, is de tijd gelijk aan de duur van de video in de toestand Dempen. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.mute.time)<br/></li> <li> **Hartslag **<br/>N.V.</li> </ul> | <ul> <li> **Beschikbaar **<br/>Ja</li> <li> **Gereserveerde variabele **<br/>, gebeurtenis</li> <li> **Totale duur dempen **<br/>rapportnaam</li> <li> **Contextgegevens **<br/>(media.states.mute.time)<br/> </li> <li> **Data Feed **<br/>media.states.mute.time</li> <li> **Audience Manager **<br/>(c_contextdata.media.states.mute.time)</li> </ul> |


### Eigenschappen van Beeld-in-beeld


#### Streams beïnvloed door beeld-in-beeld

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel **<br/>automatisch instellen</li> <li> **API-sleutel **<br/>N.v.t.</li> <li> **Vereist **<br/>nr.</li> <li> **Type **<br/>nummer</li> <li> **Verzonden met **<br/>Media Sluiten</li> <li> **Min. SDK-versie **<br/>3.0</li> <li> **Samplewaarde **<br/>TRUE</li><li> ****<br/>BeschrijvingHet aantal stromen dat door Beeld-in-beeld wordt beïnvloed. Deze metrische waarde wordt alleen ingesteld op 1 als ten minste één Beeld-in-beeldstatus is opgetreden tijdens een afspeelsessie.<br/> **Belangrijk** <br/> : als deze gebeurtenis is ingesteld, is TRUE de enige mogelijke waarde. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.pictureinpicture.set)<br/></li> <li> **Hartslag **<br/>N.V.</li> </ul> | <ul> <li> **Beschikbaar **<br/>Ja</li> <li> **Gereserveerde variabele **<br/>, gebeurtenis</li> <li> **Naamstromen **<br/>rapporteren beïnvloed door Beeld-in-beeld</li> <li> **Contextgegevens **<br/>(a.media.states.picturenpicture.set)<br/> </li> <li> **Gegevensfeed **<br/>media.states.picturenpicture</li> <li> **Audience Manager **<br/>(c_contextdata.a.media.states.pictureinpicture.set)</li> </ul> |


#### Aantal afbeeldingen in beeld

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel **<br/>automatisch instellen</li> <li> **API-sleutel **<br/>N.v.t.</li> <li> **Vereist **<br/>nr.</li> <li> **Type **<br/>nummer</li> <li> **Verzonden met **<br/>Media Sluiten</li> <li> **Min. SDK-versie **<br/>3.0</li> <li> **Samplewaarde **<br/>TRUE</li><li> ****<br/>BeschrijvingHet aantal keren dat Beeld-in-beeld werd weergegeven. Deze metrische waarde wordt alleen ingesteld op 1 als ten minste één Beeld-in-beeldstatus is opgetreden tijdens een afspeelsessie.<br/> **Belangrijk** <br/> als deze gebeurtenis is ingesteld, is het aantal gelijk aan het aantal keer dat de video zich in de beeldstatus bevond. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.pictureinpicture.count)<br/></li> <li> **Hartslag **<br/>N.V.</li> </ul> | <ul> <li> **Beschikbaar **<br/>Ja</li> <li> **Gereserveerde variabele **<br/>, gebeurtenis</li> <li> **Naam **<br/>afbeelding in aantal afbeeldingen melden</li> <li> **Contextgegevens **<br/>(media.states.picturenpicture.count)<br/> </li> <li> **Data Feed **<br/>media.states.picturenpicture.count</li> <li> **Audience Manager **<br/>(c_contextdata.media.states.pictureinpicture.count)</li> </ul> |


#### Totale duur van afbeelding in beeld

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel **<br/>automatisch instellen</li> <li> **API-sleutel **<br/>N.v.t.</li> <li> **Vereist **<br/>nr.</li> <li> **Type **<br/>nummer</li> <li> **Verzonden met **<br/>Media Sluiten</li> <li> **Min. SDK-versie **<br/>3.0</li> <li> **Samplewaarde **<br/>TRUE</li><li> ****<br/>BeschrijvingDe tijdsduur dat Beeld-in-beeld werd weergegeven. Deze metrische waarde wordt alleen ingesteld op 1 als ten minste één Beeld-in-beeldstatus is opgetreden tijdens een afspeelsessie.<br/> **Belangrijk** <br/> : als deze gebeurtenis is ingesteld, is de tijd gelijk aan de duur van de video in de status Beeld-in-beeld. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.pictureinpicture.time)<br/></li> <li> **Hartslag **<br/>N.V.</li> </ul> | <ul> <li> **Beschikbaar **<br/>Ja</li> <li> **Gereserveerde variabele **<br/>, gebeurtenis</li> <li> **Naam **<br/>afbeelding in beeld Totale duur melden</li> <li> **Contextgegevens **<br/>(media.states.picturenpicture.time)<br/> </li> <li> **Gegevensfeed **<br/>media.states.picturenpicture.time</li> <li> **Audience Manager **<br/>(c_contextdata.media.states.pictureinpicture.time)</li> </ul> |


### Eigenschappen bij focus

#### Streams die worden beïnvloed door In focus

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel **<br/>automatisch instellen</li> <li> **API-sleutel **<br/>N.v.t.</li> <li> **Vereist **<br/>nr.</li> <li> **Type **<br/>nummer</li> <li> **Verzonden met **<br/>Media Sluiten</li> <li> **Min. SDK-versie **<br/>3.0</li> <li> **Samplewaarde **<br/>TRUE</li><li> ****<br/>BeschrijvingHet aantal streams dat door In Focus wordt beïnvloed. Deze metrische waarde wordt slechts geplaatst aan 1 als minstens één In FocusStaat tijdens een playbackzitting voorkwam.<br/> **Belangrijk** <br/> : als deze gebeurtenis is ingesteld, is TRUE de enige mogelijke waarde. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.infocus.set)<br/></li> <li> **Hartslag **<br/>N.V.</li> </ul> | <ul> <li> **Beschikbaar **<br/>Ja</li> <li> **Gereserveerde variabele **<br/>, gebeurtenis</li> <li> **Rapportnaamstromen **<br/>die door In Focus zijn beïnvloed</li> <li> **Contextgegevens **<br/>(a.media.states.infocus.set)<br/> </li> <li> **Data Feed **<br/>media.states.infocus</li> <li> **Audience Manager **<br/>(c_contextdata.a.media.states.infocus.set)</li> </ul> |


#### Aantal focuspunten

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel **<br/>automatisch instellen</li> <li> **API-sleutel **<br/>N.v.t.</li> <li> **Vereist **<br/>nr.</li> <li> **Type **<br/>nummer</li> <li> **Verzonden met **<br/>Media Sluiten</li> <li> **Min. SDK-versie **<br/>3.0</li> <li> **Samplewaarde **<br/>TRUE</li><li> ****<br/>BeschrijvingHet aantal keren dat de focus is weergegeven. Deze metrische waarde wordt slechts geplaatst aan 1 als minstens één In FocusStaat tijdens een playbackzitting voorkwam.<br/> **Belangrijk **<br/>Als deze gebeurtenis is ingesteld, is het aantal gelijk aan het aantal keren dat de video zich in de status In focus bevond. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.infocus.count)<br/></li> <li> **Hartslag **<br/>N.V.</li> </ul> | <ul> <li> **Beschikbaar **<br/>Ja</li> <li> **Gereserveerde variabele **<br/>, gebeurtenis</li> <li> **Rapportnaam **<br/>in aantal focussen</li> <li> **Contextgegevens **<br/>(media.states.infocus.count)<br/> </li> <li> **Data Feed **<br/>media.states.infocus.count</li> <li> **Audience Manager **<br/>(c_contextdata.media.states.infocus.count)</li> </ul> |


#### Totale duur bij focus

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel **<br/>automatisch instellen</li> <li> **API-sleutel **<br/>N.v.t.</li> <li> **Vereist **<br/>nr.</li> <li> **Type **<br/>nummer</li> <li> **Verzonden met **<br/>Media Sluiten</li> <li> **Min. SDK-versie **<br/>3.0</li> <li> **Samplewaarde **<br/>TRUE</li><li> ****<br/>BeschrijvingDe tijdsduur waarop In focus werd weergegeven. Deze metrische waarde wordt slechts geplaatst aan 1 als minstens één In FocusStaat tijdens een playbackzitting voorkwam.<br/> **Belangrijk** <br/> als deze gebeurtenis is ingesteld, is de tijd gelijk aan hoe lang de video zich in de focus-status bevond. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.infocus.time)<br/></li> <li> **Hartslag **<br/>N.V.</li> </ul> | <ul> <li> **Beschikbaar **<br/>Ja</li> <li> **Gereserveerde variabele **<br/>, gebeurtenis</li> <li> **Rapportnaam **<br/>in focus Totale duur</li> <li> **Contextgegevens **<br/>(media.states.infocus.time)<br/> </li> <li> **Data Feed **<br/>media.states.infocus.time</li> <li> **Audience Manager **<br/>(c_contextdata.media.states.infocus.time)</li> </ul> |



## Verwante API&#39;s {#related_apis_section}

* Android - [createStateObject](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
* iOS - [createStateObjectWithName](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
* Javascript - [createStateObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)
