---
title: Parameters van de Player-status
description: In dit onderwerp worden parameters voor het bijhouden van spelerstatussen beschreven.
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
translation-type: tm+mt
source-git-commit: 1cf631d7f3d5365a02be99af78655ac3b53fb3cb
workflow-type: tm+mt
source-wordcount: '2236'
ht-degree: 1%

---


# Parameters van de Speler{#player-state-parameters}

Dit onderwerp stelt een lijst van spelerstaatsgegevens voor die Adobe via oplossingsvariabelen verzamelt.

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
>Wijzig de classificatienamen niet voor onderstaande variabelen die onder Rapportage/Gereserveerde variabele worden beschreven als &quot;classificatie&quot;.\
>De mediaclassificaties worden gedefinieerd wanneer een rapportsuite is ingeschakeld voor het bijhouden van media. Van tijd tot tijd, voegt Adobe nieuwe eigenschappen toe, en, wanneer dit voorkomt, moeten de klanten hun rapportsuites opnieuw toelaten om toegang tot de nieuwe media eigenschappen te krijgen. Tijdens het updateproces bepaalt Adobe of de classificaties worden toegelaten door de namen van de variabelen te controleren. Als een van deze ontbrekende elementen ontbreekt, voegt Adobe de ontbrekende opnieuw toe.

## Eigenschappen van afspeelstatus {#player-state-properties}

De mogelijkheden voor het bijhouden van de spelerstatus kunnen worden gekoppeld aan een audio- of videostream. De gestandaardiseerde metriek voor het bijhouden van spelerstatussen worden opgeslagen als oplossingsvariabelen. De standaardstatussen zijn: fullScreen, dempen, closeCaption, pictureInPicture en inFocus.

### Eigenschappen van Volledig scherm

#### Streams beïnvloed door volledig scherm

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeyAutomatically set  </li> <li> **API**<br/> KeyN/A </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Verzonden**<br/> met Media Close </li> <li> **Min. SDK-versie**<br/> 3.0</li> <li> **Voorbeeld**<br/> van ValueTRUE </li><li> ****<br/> BeschrijvingHet aantal streams dat wordt beïnvloed door Volledig scherm. Deze metrische waarde wordt slechts ingesteld op 1 als minstens één Volledige staat van het Scherm tijdens een playbackzitting voorkwam. <br/> **** <br/> BelangrijkAls deze gebeurtenis is ingesteld, is de enige mogelijke waarde TRUE. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.   </li> </ul> | <ul> <li> **Adobe**<br/> Analyticsa.media.states.fullscreen.set<br/></li> <li> ****<br/> HartslagN.v.t. </li> </ul> | <ul> <li> ****<br/> AvailableYes </li> <li> **Gereserveerde**<br/> variabeleEvent </li> <li> **Rapportnaamstromen**<br/> beïnvloed door volledig scherm </li> <li> **Context**<br/> Data.media.states.fullscreen.set<br/> </li> <li> **Data**<br/> Feedvideostatefullscreen </li> <li> **Audience**<br/> Managerc_contextdata.a.media.states.fullscreen.set </li> </ul> |

#### Aantal op volledig scherm

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeyAutomatically set  </li> <li> **API**<br/> KeyN/A </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Verzonden**<br/> met Media Close </li> <li> **Min. SDK-versie**<br/> 3.0</li> <li> **Voorbeeld**<br/> van ValueTRUE </li><li> ****<br/> BeschrijvingHet aantal keren dat een volledig scherm werd weergegeven. Deze metrische waarde wordt slechts ingesteld op 1 als minstens één Volledige staat van het Scherm tijdens een playbackzitting voorkwam. <br/> ****<br/> BelangrijkAls deze gebeurtenis is ingesteld, is het aantal gelijk aan het aantal keren dat de video zich in de status Volledig scherm bevond. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.</li> </ul> | <ul> <li> **Adobe**<br/> Analyticsa.media.states.fullscreen.count<br/></li> <li> ****<br/> HartslagN.v.t. </li> </ul> | <ul> <li> ****<br/> AvailableYes </li> <li> **Gereserveerde**<br/> variabeleEvent </li> <li> **Rapportnaam**<br/> Volledig scherm tellen </li> <li> **Context**<br/> Data.media.states.fullscreen.count<br/> </li> <li> **Gegevens**<br/> Feedvideostatefullscreencount </li> <li> **Audience**<br/> Managerc_contextdata.media.states.fullscreen.count </li> </ul> |



#### Totale duur volledig scherm

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeyAutomatically set  </li> <li> **API**<br/> KeyN/A </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Verzonden**<br/> met Media Close </li> <li> **Min. SDK-versie**<br/> 3.0</li> <li> **Voorbeeld**<br/> van ValueTRUE </li><li> ****<br/> BeschrijvingDe tijdsduur dat een volledig scherm werd weergegeven. Deze metrische waarde wordt slechts ingesteld op 1 als minstens één Volledige staat van het Scherm tijdens een playbackzitting voorkwam. <br/> ****<br/>  BelangrijkAls deze gebeurtenis is ingesteld, is de tijd gelijk aan de duur van de video in de status Volledig scherm. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.  </li> </ul> | <ul> <li> **Adobe**<br/> Analyticsa.media.states.fullscreen.time<br/></li> <li> ****<br/> HartslagN.v.t. </li> </ul> | <ul> <li> ****<br/> AvailableYes </li> <li> **Gereserveerde**<br/> variabeleEvent </li> <li> **Volledige**<br/> schermduur rapport </li> <li> **Context**<br/> Data.media.states.fullscreen.time<br/> </li> <li> **Gegevens**<br/> Feedvideostatefullscreentime </li> <li> **Audience**<br/> Managerc_contextdata.media.states.fullscreen.time </li> </ul> |


### Eigenschappen bijschrift sluiten

#### Streams die worden beïnvloed door ondertiteling

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeyAutomatically set  </li> <li> **API**<br/> KeyN/A </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Verzonden**<br/> met Media Close </li> <li> **Min. SDK-versie**<br/> 3.0</li> <li> **Voorbeeld**<br/> van ValueTRUE </li><li> ****<br/> BeschrijvingHet aantal stromen die door Gesloten Captioning worden beïnvloed. Deze metrische waarde wordt slechts geplaatst aan 1 als minstens één Gesloten Staat van de Titel tijdens een playbackzitting voorkwam. <br/> **** <br/>  BelangrijkAls deze gebeurtenis is ingesteld, is de enige mogelijke waarde TRUE. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.   </li> </ul> | <ul> <li> **Adobe**<br/> Analyticsa.media.states.closedcaptioning.set<br/></li> <li> ****<br/> HartslagN.v.t. </li> </ul> | <ul> <li> ****<br/> AvailableYes </li> <li> **Gereserveerde**<br/> variabeleEvent </li> <li> **Report**<br/> NameStreams die zijn beïnvloed door Closed Captioning </li> <li> **Context**<br/> Data.media.states.closedcaptioning.set<br/> </li> <li> **Data**<br/> FeedvideoStatusLoskoppeling </li> <li> **Audience**<br/> Managerc_contextdata.a.media.states.closed edcaptioning.set </li> </ul> |


#### Aantal ondertitelingen

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeyAutomatically set  </li> <li> **API**<br/> KeyN/A </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Verzonden**<br/> met Media Close </li> <li> **Min. SDK-versie**<br/> 3.0</li> <li> **Voorbeeld**<br/> van ValueTRUE </li><li> ****<br/> BeschrijvingHet aantal keren dat Closed Captioning is weergegeven. Deze metrische waarde wordt slechts geplaatst aan 1 als minstens één Gesloten Captioning Staat tijdens een playbackzitting voorkwam. <br/> ****<br/>  BelangrijkAls deze gebeurtenis is ingesteld, is het aantal gelijk aan het aantal keren dat de video zich in de status Closed Captioning bevond. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.   </li> </ul> | <ul> <li> **Adobe**<br/> Analyticsa.media.states.closedcaptioning.count<br/></li> <li> ****<br/> HartslagN.v.t. </li> </ul> | <ul> <li> ****<br/> AvailableYes </li> <li> **Gereserveerde**<br/> variabeleEvent </li> <li> **Aantal**<br/> ondertiteling in rapport </li> <li> **Context**<br/> Data.media.states.closedcaptioning.count<br/> </li> <li> **Gegevens**<br/> FeedbackCaptioningCount </li> <li> **Audience**<br/> Managerc_contextdata.media.states.closedcaptioning.count </li> </ul> |


#### Totale duur van ondertiteling

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeyAutomatically set  </li> <li> **API**<br/> KeyN/A </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Verzonden**<br/> met Media Close </li> <li> **Min. SDK-versie**<br/> 3.0</li> <li> **Voorbeeld**<br/> van ValueTRUE </li><li> ****<br/> BeschrijvingDe tijdsduur voor Ondertiteling is weergegeven. Deze metrische waarde wordt slechts ingesteld op 1 als minstens één Volledige staat van het Scherm tijdens een playbackzitting voorkwam. <br/> ****<br/>  BelangrijkAls deze gebeurtenis is ingesteld, is de tijd gelijk aan hoe lang de video zich in de status Closed Captioning bevond. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.   </li> </ul> | <ul> <li> **Adobe**<br/> Analyticsa.media.states.closedcaptioning.time<br/></li> <li> ****<br/> HartslagN.v.t. </li> </ul> | <ul> <li> ****<br/> AvailableYes </li> <li> **Gereserveerde**<br/> variabeleEvent </li> <li> **Totale duur**<br/> van ondertiteling rapporteren </li> <li> **Context**<br/> Data.media.states.closedcaptioning.time<br/> </li> <li> **Data**<br/> FeedVideoStatusLoedcaptionTime </li> <li> **Audience**<br/> Managerc_contextdata.media.states.closed edcaptioning.time </li> </ul> |


### Eigenschappen dempen

#### Streams beïnvloed door Dempen

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeyAutomatically set  </li> <li> **API**<br/> KeyN/A </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Verzonden**<br/> met Media Close </li> <li> **Min. SDK-versie**<br/> 3.0</li> <li> **Voorbeeld**<br/> van ValueTRUE </li><li> ****<br/> BeschrijvingHet aantal streams dat door Dempen wordt beïnvloed. Deze metrische waarde wordt ingesteld op 1 alleen als ten minste één dempingsstatus is opgetreden tijdens een afspeelsessie. <br/> **** <br/> BelangrijkAls deze gebeurtenis is ingesteld, is de enige mogelijke waarde TRUE. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.   </li> </ul> | <ul> <li> **Adobe**<br/> Analyticsa.media.states.mute.set<br/></li> <li> ****<br/> HartslagN.v.t. </li> </ul> | <ul> <li> ****<br/> AvailableYes </li> <li> **Gereserveerde**<br/> variabeleEvent </li> <li> **Rapportnaamstromen**<br/> beïnvloed door Dempen </li> <li> **Context**<br/> Data.media.states.mute.set<br/> </li> <li> **Gegevens-**<br/> feedvideoverklaring </li> <li> **Audience**<br/> Managerc_contextdata.a.media.states.mute.set </li> </ul> |

#### Aantal dempen

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeyAutomatically set  </li> <li> **API**<br/> KeyN/A </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Verzonden**<br/> met Media Close </li> <li> **Min. SDK-versie**<br/> 3.0</li> <li> **Voorbeeld**<br/> van ValueTRUE </li><li> ****<br/> BeschrijvingHet aantal keren dat Dempen is weergegeven. Deze metrische waarde wordt ingesteld op 1 alleen als ten minste één dempingsstatus is opgetreden tijdens een afspeelsessie. <br/> ****<br/>  ImportantIf this event is set, the count is equal to the number of times the video was in the Mute state. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.   </li> </ul> | <ul> <li> **Adobe**<br/> Analyticsa.media.states.mute.count<br/></li> <li> ****<br/> HartslagN.v.t. </li> </ul> | <ul> <li> ****<br/> AvailableYes </li> <li> **Gereserveerde**<br/> variabeleEvent </li> <li> **Mute**<br/> aantal rapporteren </li> <li> **Context**<br/> Data.media.states.mute.count<br/> </li> <li> **Data**<br/> FeedVideoStutecount </li> <li> **Audience**<br/> Managerc_contextdata.media.states.mute.count </li> </ul> |

#### Totale duur dempen

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeyAutomatically set  </li> <li> **API**<br/> KeyN/A </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Verzonden**<br/> met Media Close </li> <li> **Min. SDK-versie**<br/> 3.0</li> <li> **Voorbeeld**<br/> van ValueTRUE </li><li> ****<br/> BeschrijvingDe tijdsduur van Dempen is weergegeven. Deze metrische waarde wordt ingesteld op 1 alleen als ten minste één dempingsstatus is opgetreden tijdens een afspeelsessie. <br/> ****<br/> BelangrijkAls deze gebeurtenis is ingesteld, is de tijd gelijk aan de duur van de video in de toestand Dempen. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.   </li> </ul> | <ul> <li> **Adobe**<br/> Analyticsa.media.states.mute.time<br/></li> <li> ****<br/> HartslagN.v.t. </li> </ul> | <ul> <li> ****<br/> AvailableYes </li> <li> **Gereserveerde**<br/> variabeleEvent </li> <li> **Totale duur**<br/> van Mute rapporteren </li> <li> **Context**<br/> Data.media.states.mute.time<br/> </li> <li> **Data**<br/> Feedvideostatemutetime </li> <li> **Audience**<br/> Managerc_contextdata.media.states.mute.time </li> </ul> |


### Eigenschappen van Beeld-in-beeld


#### Streams beïnvloed door beeld-in-beeld

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeyAutomatically set  </li> <li> **API**<br/> KeyN/A </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Verzonden**<br/> met Media Close </li> <li> **Min. SDK-versie**<br/> 3.0</li> <li> **Voorbeeld**<br/> van ValueTRUE </li><li> ****<br/> BeschrijvingHet aantal stromen dat door Beeld-in-beeld wordt beïnvloed. Deze metrische waarde wordt alleen ingesteld op 1 als ten minste één Beeld-in-beeldstatus is opgetreden tijdens een afspeelsessie. <br/> **** <br/> BelangrijkAls deze gebeurtenis is ingesteld, is de enige mogelijke waarde TRUE. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.   </li> </ul> | <ul> <li> **Adobe**<br/> Analyticsa.media.states.pictureinpicture.set<br/></li> <li> ****<br/> HartslagN.v.t. </li> </ul> | <ul> <li> ****<br/> AvailableYes </li> <li> **Gereserveerde**<br/> variabeleEvent </li> <li> **Naamstromen**<br/> rapporteren die door Beeld-in-beeld zijn beïnvloed </li> <li> **Context**<br/> Data.media.states.picturenpicture.set<br/> </li> <li> **Gegevens**<br/> Feedvideostatepictureinpicture </li> <li> **Audience**<br/> Managerc_contextdata.a.media.states.pictureinpicture.set </li> </ul> |


#### Aantal afbeeldingen in beeld

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeyAutomatically set  </li> <li> **API**<br/> KeyN/A </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Verzonden**<br/> met Media Close </li> <li> **Min. SDK-versie**<br/> 3.0</li> <li> **Voorbeeld**<br/> van ValueTRUE </li><li> ****<br/> BeschrijvingHet aantal keren dat Beeld-in-beeld werd weergegeven. Deze metrische waarde wordt alleen ingesteld op 1 als ten minste één Beeld-in-beeldstatus is opgetreden tijdens een afspeelsessie. <br/> **** <br/> BelangrijkAls deze gebeurtenis is ingesteld, is het aantal gelijk aan het aantal keer dat de video zich in de status Beeld-in-beeld bevond. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.   </li> </ul> | <ul> <li> **Adobe**<br/> Analyticsa.media.states.pictureinpicture.count<br/></li> <li> ****<br/> HartslagN.v.t. </li> </ul> | <ul> <li> ****<br/> AvailableYes </li> <li> **Gereserveerde**<br/> variabeleEvent </li> <li> **Aantal**<br/> Beeld-in-beeld rapporteren </li> <li> **Context**<br/> Data.media.states.picturenpicture.count<br/> </li> <li> **Gegevens**<br/> Feedvideostatepictureinpicturecount </li> <li> **Audience**<br/> Managerc_contextdata.media.states.pictureinpicture.count </li> </ul> |


#### Totale duur van afbeelding in beeld

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeyAutomatically set  </li> <li> **API**<br/> KeyN/A </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Verzonden**<br/> met Media Close </li> <li> **Min. SDK-versie**<br/> 3.0</li> <li> **Voorbeeld**<br/> van ValueTRUE </li><li> ****<br/> BeschrijvingDe tijdsduur dat Beeld-in-beeld werd weergegeven. Deze metrische waarde wordt alleen ingesteld op 1 als ten minste één Beeld-in-beeldstatus is opgetreden tijdens een afspeelsessie. <br/> **** <br/> BelangrijkAls deze gebeurtenis is ingesteld, is de tijd gelijk aan de duur van de video in de status Beeld-in-beeld. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.   </li> </ul> | <ul> <li> **Adobe**<br/> Analyticsa.media.states.pictureinpicture.time<br/></li> <li> ****<br/> HartslagN.v.t. </li> </ul> | <ul> <li> ****<br/> AvailableYes </li> <li> **Gereserveerde**<br/> variabeleEvent </li> <li> **Totale duur van**<br/> Beeld-in-beeld rapporteren </li> <li> **Context**<br/> Data.media.states.picturenpicture.time<br/> </li> <li> **Data**<br/> FeedvideoStatusInPictureTime </li> <li> **Audience**<br/> Managerc_contextdata.media.states.pictureinpicture.time </li> </ul> |


### Eigenschappen bij focus

#### Streams die worden beïnvloed door In focus

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeyAutomatically set  </li> <li> **API**<br/> KeyN/A </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Verzonden**<br/> met Media Close </li> <li> **Min. SDK-versie**<br/> 3.0</li> <li> **Voorbeeld**<br/> van ValueTRUE </li><li> ****<br/> BeschrijvingHet aantal streams dat door In Focus wordt beïnvloed. Deze metrische waarde wordt slechts geplaatst aan 1 als minstens één In FocusStaat tijdens een playbackzitting voorkwam. <br/> **** <br/> BelangrijkAls deze gebeurtenis is ingesteld, is de enige mogelijke waarde TRUE. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.   </li> </ul> | <ul> <li> **Adobe**<br/> Analyticsa.media.states.infocus.set<br/></li> <li> ****<br/> HartslagN.v.t. </li> </ul> | <ul> <li> ****<br/> AvailableYes </li> <li> **Gereserveerde**<br/> variabeleEvent </li> <li> **NameStreams rapporteren die zijn beïnvloed door**<br/> In Focus </li> <li> **Context**<br/> Data.media.states.infocus.set<br/> </li> <li> **Data**<br/> Feedvideostateinfocus </li> <li> **Audience**<br/> Managerc_contextdata.a.media.states.infocus.set </li> </ul> |


#### Aantal focuspunten

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeyAutomatically set  </li> <li> **API**<br/> KeyN/A </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Verzonden**<br/> met Media Close </li> <li> **Min. SDK-versie**<br/> 3.0</li> <li> **Voorbeeld**<br/> van ValueTRUE </li><li> ****<br/> BeschrijvingHet aantal keren dat de focus is weergegeven. Deze metrische waarde wordt slechts geplaatst aan 1 als minstens één In FocusStaat tijdens een playbackzitting voorkwam. <br/> ****<br/>  ImportantIf this event is set, the count is equal to the number of times the video was in the In Focus state. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.   </li> </ul> | <ul> <li> **Adobe**<br/> Analyticsa.media.states.infocus.count<br/></li> <li> ****<br/> HartslagN.v.t. </li> </ul> | <ul> <li> ****<br/> AvailableYes </li> <li> **Gereserveerde**<br/> variabeleEvent </li> <li> **Aantal**<br/> focus-innamen rapporteren </li> <li> **Context**<br/> Data.media.states.infocus.count<br/> </li> <li> **Gegevens**<br/> FeedbackFocusCount </li> <li> **Audience**<br/> Managerc_contextdata.media.states.infocus.count </li> </ul> |


#### Totale duur bij focus

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeyAutomatically set  </li> <li> **API**<br/> KeyN/A </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Verzonden**<br/> met Media Close </li> <li> **Min. SDK-versie**<br/> 3.0</li> <li> **Voorbeeld**<br/> van ValueTRUE </li><li> ****<br/> BeschrijvingDe tijdsduur waarop In focus werd weergegeven. Deze metrische waarde wordt slechts geplaatst aan 1 als minstens één In FocusStaat tijdens een playbackzitting voorkwam. <br/> **** <br/> BelangrijkAls deze gebeurtenis is ingesteld, is de tijd gelijk aan hoe lang de video zich in de focus-status bevond. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.   </li> </ul> | <ul> <li> **Adobe**<br/> Analyticsa.media.states.infocus.time<br/></li> <li> ****<br/> HartslagN.v.t. </li> </ul> | <ul> <li> ****<br/> AvailableYes </li> <li> **Gereserveerde**<br/> variabeleEvent </li> <li> **Totale duur**<br/> van rapportnaamIn focus </li> <li> **Context**<br/> Data.media.states.infocus.time<br/> </li> <li> **Gegevens**<br/> Feedvideostateinfocustime </li> <li> **Audience**<br/> Managerc_contextdata.media.states.infocus.time </li> </ul> |

## Lijst met eigenschappen voor XDM-identiteiten

Gegevens die zijn opgeslagen in Analytics kunnen voor elk doel worden gebruikt en de metriek van de spelerstatus kan in Adobe Experience Platform worden geïmporteerd met XDM en worden gebruikt met Customer Journey Analytics.

| Eigenschap spelerstatus | Toewijzing |
|---------------------------------------|------------------------------------|
| a.media.states.fullScreen.set | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateSet |
| a.media.states.fullScreen.count | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateCount |
| a.media.states.fullScreen.time | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateTime |
| a.media.states.mute.set | media.mediaTimed.primaryAssetViewDetails.mute.playerStateSet |
| a.media.states.mute.count | media.mediaTimed.primaryAssetViewDetails.mute.playerStateCount |
| a.media.states.mute.time | media.mediaTimed.primaryAssetViewDetails.mute.playerStateTime |
| a.media.states.closeCaption.set | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateSet |
| a.media.states.closeCaption.count | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateCount |
| a.media.states.closeCaption.time | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateTime |
| a.media.states.pictureInPicture.set | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateSet |
| a.media.states.pictureInPicture.count | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateCount |
| a.media.states.pictureInPicture.time | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateTime |
| a.media.states.inFocus.set | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateSet |
| a.media.states.inFocus.count | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateCount |
| a.media.states.inFocus.time | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateTime |

## Verwante API&#39;s {#related_apis_section}

* Android - [createStateObject](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
* iOS - [createStateObjectWithName](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
* Javascript - [createStateObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)
