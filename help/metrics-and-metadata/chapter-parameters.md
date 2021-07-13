---
title: Hoofdstukparameters
description: '"Leer over hoofdstukparameters voor implementatie, netwerk, en rapportering."'
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
exl-id: 73da3e52-9498-478e-bfd7-8ff6c8e6bfc5
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '1067'
ht-degree: 2%

---

# Hoofdstukparameters{#chapter-parameters}

Dit onderwerp stelt een lijst van hoofdstuk en/of segmentgegevens, met inbegrip van de waarden van contextgegevens voor, die Adobe via oplossingsvariabelen verzamelt.

Beschrijving van tabelgegevens:

* **Implementatie:** informatie over implementatiewaarden en -vereisten
   * *Sleutel*  - Variabele, plaats of manueel in uw app, of automatisch door de Adobe Media SDK.
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

## Metagegevens hoofdstuk {#chapter-metadata}

### Hoofdstuknaam

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>  [name](./chapter-parameters.md#related_apis_section) </li> <li> **API-sleutel:**<br/> media.hoofdstuk.vriendelijkeName </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:Start**<br/> hoofdstuk, Sluiten </li> <li> **Min. SDK-versie:** 1.3 </li> <li> **Samplewaarde:**<br/> &quot;The Big Bang Chapter 2 - Dating&quot; </li><li> **Omschrijving:**<br/> de naam van het hoofdstuk en/of segment.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>vriendelijkeName) </li> <li> **hartslag:**<br/> (:stream:naam_naam) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> standaard gemaakt...  </li> <li> **Gereserveerde variabele:**<br/> classificatie </li> <li> **Rapportnaam:**<br/> hoofdstuknaam </li> <li> **Contextgegevens:**<br/> (a.media.chapter.<br/>vriendelijkeName) </li> <li> **Gegevensfeed:**<br/> n.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>vriendelijkeName) </li> </ul> |

### Hoofdstukpositie

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>  [position](./chapter-parameters.md#related_apis_section) </li> <li> **API-sleutel:**<br/> media.chapter.index </li> <li> **Vereist:**<br/> SDK: Neen; API: Ja. </li> <li> **Tekst:**<br/> nummer </li> <li> **Verzonden met:**<br/> Hoofdstuk sluiten </li> <li> **Min. SDK-versie:** 1.3 </li> <li> **Samplewaarde:**<br/> 2 </li><li> **Beschrijving:**<br/> De positie (index, geheel getal) van het hoofdstuk binnen de inhoud.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>position) </li> <li> **hartslag:**<br/> (:stream:hoofdstuk_pos) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> classificatie </li> <li> **Rapportnaam:**<br/> hoofdstukpositie </li> <li> **Contextgegevens:**<br/> (a.media.chapter.<br/>positie) </li> <li> **Gegevensfeed:**<br/> n.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>positie) </li> </ul> |

### Verschuiving hoofdstuk

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>  [startTime](./chapter-parameters.md#related_apis_section) </li> <li> **API-sleutel:**<br/> media.chapter.offset </li> <li> **Vereist:**<br/> SDK: Neen; API: Ja. </li> <li> **Tekst:**<br/> nummer </li> <li> **Verzonden met:**<br/> Hoofdstuk sluiten </li> <li> **Min. SDK-versie:** 1.3 </li> <li> **Samplewaarde:**<br/> 58 </li><li> **Beschrijving:**<br/> De verschuiving van het hoofdstuk binnen de inhoud (in seconden) vanaf het begin.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>offset) </li> <li> **hartslag:**<br/> (:stream:hoofdstuk_offset) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> classificatie </li> <li> **Rapportnaam:**<br/> hoofdstukverschuiving </li> <li> **Contextgegevens:**<br/> (a.media.chapter.<br/>offset) </li> <li> **Gegevensfeed:**<br/> n.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>offset) </li> </ul> |

### Hoofdstuklengte

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> </li> <li> **API-sleutel:**<br/> media.chapter.length </li> <li> **Vereist:**<br/> SDK: Neen; API: Ja. </li> <li> **Tekst:**<br/> nummer </li> <li> **Verzonden met:**<br/> Hoofdstuk sluiten </li> <li> **Min. SDK-versie:** 1.3 </li> <li> **Samplewaarde:**<br/> 486 </li><li> **Beschrijving:**<br/> de lengte van het hoofdstuk, in seconden.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>length) </li> <li> **hartslag:**<br/> (:stream:hoofdstuk_lengte) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> classificatie </li> <li> **rapportnaam:**<br/> hoofdstuklengte </li> <li> **Contextgegevens:**<br/> (a.media.chapter.<br/>lengte) </li> <li> **Gegevensfeed:**<br/> n.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>lengte) </li> </ul> |

### Hoofdstuk

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Hoofdstuk sluiten </li> <li> **Min. SDK-versie:** 1.3 </li> <li> **Samplewaarde:**<br/> </li><li> **Beschrijving:**<br/> De automatisch gegenereerde id van het hoofdstuk.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>name) </li> <li> **hartslag:**<br/> (:stream:schapter_id) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **verlopen:**<br/> op HIT </li> <li> **Rapportnaam:**<br/> hoofdstuk </li> <li> **Contextgegevens:**<br/> (a.media.chapter.<br/>name) </li> <li> **Gegevensfeed:**<br/> videohoofdstuk </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>name) </li> </ul> |

## Hoofdstukmetriek {#chapter-Metrics}

### Begin hoofdstuk

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> automatisch instellen  </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:Begin**<br/> hoofdstuk </li> <li> **Min. SDK-versie:** 1.3 </li> <li> **Samplewaarde:**<br/> TRUE </li><li> **Beschrijving:**<br/> Het aantal hoofdstukken begint.  **Belangrijk:**  Als deze gebeurtenis is ingesteld, is TRUE de enige mogelijke waarde. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>weergave) </li> <li> **Hartslag:**<br/> (:event:<br/>stype=type_start) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> gebeurtenis </li> <li> **rapportnaam:**<br/> hoofdstukbeheer</li> <li> **Contextgegevens:**<br/> (a.media.chapter.<br/>weergave) </li> <li> **Gegevensfeed:**<br/> n.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>weergave) </li> </ul> |

### Hoofdstuk voltooid

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> automatisch instellen  </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Hoofdstuk sluiten </li> <li> **Min. SDK-versie:** 1.3</li> <li> **Samplewaarde:**<br/> TRUE </li><li> **Beschrijving:**<br/> het aantal hoofdstukken is voltooid.  **Belangrijk:**  Als deze gebeurtenis is ingesteld, is TRUE de enige mogelijke waarde. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>complete) </li> <li> **Hartslag:**<br/> (:event:<br/>stype=type_complete) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> gebeurtenis </li> <li> **rapportnaam:**<br/> hoofdstukvoltooiing</li> <li> **Contextgegevens:**<br/> (a.media.chapter.<br/>complete) </li> <li> **Gegevensfeed:**<br/> n.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>complete) </li> </ul> |

### Tijd besteed aan hoofdstuk

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> automatisch instellen  </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Ja </li> <li> **Tekst:**<br/> nummer </li> <li> **Verzonden met:**<br/> Hoofdstuk sluiten </li> <li> **Min. SDK-versie:** 1.3 </li> <li> **Samplewaarde:**<br/> </li><li> **Beschrijving:**<br/> De tijd die aan het hoofdstuk wordt besteed.  De waarde zal in het tijdformaat (HH:MM:SS) in Analysis Workspace en Rapporten &amp; Analytics worden getoond. In de Diervoeders van Gegevens, Data Warehouse, en Rapporterende APIs zullen de waarden in seconden worden getoond. <br/>**Releasedatum: 13-09-18**   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>timePlayed) </li> <li> **Hartslag:**<br/> </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> gebeurtenis </li> <li> **rapportnaam:**<br/> hoofdstuktijd besteed</li> <li> **Contextgegevens:**<br/> (a.media.chapter.<br/>timePlayed) </li> <li> **Gegevensfeed:**<br/> n.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>timePlayed) </li> </ul> |

## Verwante API&#39;s {#related_apis_section}

* Android - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* iOS - [createChapterObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:length:startTime:)
* Javascript - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)
