---
title: Hoofdstukparameters
description: null
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Hoofdstukparameters{#chapter-parameters}

Dit onderwerp presenteert een lijst met hoofdstuk- en/of segmentgegevens, inclusief contextgegevenswaarden, die Adobe verzamelt via oplossingsvariabelen.

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
>Wijzig de classificatienamen niet voor onderstaande variabelen die onder Rapportage/Gereserveerde variabele worden beschreven als &quot;classificatie&quot;.\
>De mediaclassificaties worden gedefinieerd wanneer een rapportsuite is ingeschakeld voor het bijhouden van media. Adobe voegt van tijd tot tijd nieuwe eigenschappen toe en wanneer dit gebeurt, moeten klanten hun rapportsuites opnieuw inschakelen om toegang tot de nieuwe media-eigenschappen te krijgen. Tijdens het updateproces bepaalt Adobe of de classificaties zijn ingeschakeld door de namen van de variabelen te controleren. Als een van deze ontbrekende items ontbreekt, voegt Adobe de ontbrekende items opnieuw toe.

## Metagegevens hoofdstuk {#chapter-metadata}

### Hoofdstuknaam

|   Implementatie | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>  [name](./chapter-parameters.md#related_apis_section) </li> <li> **API-sleutel:**<br/>media.chapter.bevriezingName</li> <li> **Vereist:**<br/>Nee</li> <li> **Type:**<br/>string</li> <li> **Verzonden met:**<br/>Hoofdstukbegin, Hoofdstuk sluiten</li> <li> **Min. SDK-versie:** 1,3 </li> <li> **Samplewaarde:**<br/>&quot;The Big Bang Chapter 2 - Dating&quot;</li><li> **Omschrijving:**<br/>de naam van het hoofdstuk en/of segment.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.chapter.<br/>vriendelijkeName)</li> <li> **Hartslag:**<br/>(s:stream:hoofdstuk_naam)</li> </ul> | <ul> <li> **Beschikbaar:**<br/>Standaard gemaakt...</li> <li> **Gereserveerde variabele:**<br/>Classificatie</li> <li> **Rapportnaam:**<br/>Hoofdstuknaam</li> <li> **Contextgegevens:**<br/>(a.media.chapter.<br/>vriendelijkeName)</li> <li> **Gegevensfeed:**<br/>N.v.t.</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.chapter.<br/>vriendelijkeName)</li> </ul> |

### Hoofdstukpositie

|   Implementatie | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>  [positie](./chapter-parameters.md#related_apis_section) </li> <li> **API-sleutel:**<br/>media.hoofdstuk.index</li> <li> **Vereist:**<br/>SDK: Neen; API: Ja.</li> <li> **Type:**<br/>getal</li> <li> **Verzonden met:**<br/>Hoofdstuk sluiten</li> <li> **Min. SDK-versie:** 1,3 </li> <li> **Samplewaarde:**<br/>2</li><li> **Beschrijving:**<br/>De positie (index, geheel getal) van het hoofdstuk binnen de inhoud.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.chapter.<br/>positie)</li> <li> **Hartslag:**<br/>(l:stream:hoofdstuk_pos)</li> </ul> | <ul> <li> **Beschikbaar:**<br/>Ja</li> <li> **Gereserveerde variabele:**<br/>Classificatie</li> <li> **Rapportnaam:**<br/>Hoofdstukpositie</li> <li> **Contextgegevens:**<br/>(a.media.chapter.<br/>positie)</li> <li> **Gegevensfeed:**<br/>N.v.t.</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.chapter.<br/>positie)</li> </ul> |

### Verschuiving hoofdstuk

|   Implementatie | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>  [startTime](./chapter-parameters.md#related_apis_section) </li> <li> **API-sleutel:**<br/>media.hoofdstuk.offset</li> <li> **Vereist:**<br/>SDK: Neen; API: Ja.</li> <li> **Type:**<br/>getal</li> <li> **Verzonden met:**<br/>Hoofdstuk sluiten</li> <li> **Min. SDK-versie:** 1,3 </li> <li> **Samplewaarde:**<br/>58</li><li> **Beschrijving:**<br/>De verschuiving van het hoofdstuk binnen de inhoud (in seconden) vanaf het begin.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.chapter.<br/>offset)</li> <li> **Hartslag:**<br/>(l:stream:chapter_offset)</li> </ul> | <ul> <li> **Beschikbaar:**<br/>Ja</li> <li> **Gereserveerde variabele:**<br/>Classificatie</li> <li> **Rapportnaam:**<br/>Verschuiving hoofdstuk</li> <li> **Contextgegevens:**<br/>(a.media.chapter.<br/>offset)</li> <li> **Gegevensfeed:**<br/>N.v.t.</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.chapter.<br/>offset)</li> </ul> |

### Hoofdstuklengte

|   Implementatie | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> </li> <li> **API-sleutel:**<br/>media.hoofdstuk.length</li> <li> **Vereist:**<br/>SDK: Neen; API: Ja.</li> <li> **Type:**<br/>getal</li> <li> **Verzonden met:**<br/>Hoofdstuk sluiten</li> <li> **Min. SDK-versie:** 1,3 </li> <li> **Samplewaarde:**<br/>486</li><li> **Beschrijving:**<br/>de lengte van het hoofdstuk, in seconden.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.chapter.<br/>lengte)</li> <li> **Hartslag:**<br/>(l:stream:chapter_length)</li> </ul> | <ul> <li> **Beschikbaar:**<br/>Ja</li> <li> **Gereserveerde variabele:**<br/>Classificatie</li> <li> **Rapportnaam:**<br/>Hoofdstuklengte</li> <li> **Contextgegevens:**<br/>(a.media.chapter.<br/>lengte)</li> <li> **Gegevensfeed:**<br/>N.v.t.</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.chapter.<br/>lengte)</li> </ul> |

### Hoofdstuk

|   Implementatie | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>Automatisch instellen</li> <li> **API-sleutel:**<br/>N.v.t.</li> <li> **Vereist:**<br/>Nee</li> <li> **Type:**<br/>string</li> <li> **Verzonden met:**<br/>Hoofdstuk sluiten</li> <li> **Min. SDK-versie:** 1,3 </li> <li> **Samplewaarde:**<br/> </li><li> **Beschrijving:**<br/>De automatisch gegenereerde id van het hoofdstuk.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.chapter.<br/>name)</li> <li> **Hartslag:**<br/>(s:stream:hoofdstuk_id)</li> </ul> | <ul> <li> **Beschikbaar:**<br/>Ja</li> <li> **Gereserveerde variabele:**<br/>eVar</li> <li> **Verlopen:**<br/>Op HIT</li> <li> **Rapportnaam:**<br/>Hoofdstuk</li> <li> **Contextgegevens:**<br/>(a.media.chapter.<br/>name)</li> <li> **Gegevensfeed:**<br/>videohoofdstuk</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.chapter.<br/>name)</li> </ul> |

## Hoofdstukmetriek {#chapter-Metrics}

### Begin hoofdstuk

|   Implementatie | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>Automatisch instellen</li> <li> **API-sleutel:**<br/>N.v.t.</li> <li> **Vereist:**<br/>Ja</li> <li> **Type:**<br/>string</li> <li> **Verzonden met:**<br/>Begin hoofdstuk</li> <li> **Min. SDK-versie:** 1,3 </li> <li> **Samplewaarde:**<br/>TRUE</li><li> **Beschrijving:**<br/>Het aantal hoofdstukken begint.**Belangrijk:**Als deze gebeurtenis is ingesteld, is TRUE de enige mogelijke waarde. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.chapter.<br/>weergave)</li> <li> **Hartslag:**<br/>(s:event:<br/>type=chapter_start)</li> </ul> | <ul> <li> **Beschikbaar:**<br/>Ja</li> <li> **Gereserveerde variabele:**<br/>event</li> <li> **Rapportnaam:**<br/>Hoofdstukartikelen g</li> <li> **Contextgegevens:**<br/>(a.media.chapter.<br/>weergave)</li> <li> **Gegevensfeed:**<br/>N.v.t.</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.chapter.<br/>weergave)</li> </ul> |

### Hoofdstuk voltooid

|   Implementatie | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>Automatisch instellen</li> <li> **API-sleutel:**<br/>N.v.t.</li> <li> **Vereist:**<br/>Ja</li> <li> **Type:**<br/>string</li> <li> **Verzonden met:**<br/>Hoofdstuk sluiten</li> <li> **Min. SDK-versie:** 1,3</li> <li> **Samplewaarde:**<br/>TRUE</li><li> **Beschrijving:**<br/>het aantal hoofdstukken is voltooid.**Belangrijk:**Als deze gebeurtenis is ingesteld, is TRUE de enige mogelijke waarde. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.chapter.<br/>complete)</li> <li> **Hartslag:**<br/>(s:event:<br/>type=chapter_complete)</li> </ul> | <ul> <li> **Beschikbaar:**<br/>Ja</li> <li> **Gereserveerde variabele:**<br/>event</li> <li> **Rapportnaam:**<br/>Hoofdstuk Voltooien g</li> <li> **Contextgegevens:**<br/>(a.media.chapter.<br/>complete)</li> <li> **Gegevensfeed:**<br/>N.v.t.</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.chapter.<br/>complete)</li> </ul> |

### Tijd besteed aan hoofdstuk

|   Implementatie | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>Automatisch instellen</li> <li> **API-sleutel:**<br/>N.v.t.</li> <li> **Vereist:**<br/>Ja</li> <li> **Type:**<br/>getal</li> <li> **Verzonden met:**<br/>Hoofdstuk sluiten</li> <li> **Min. SDK-versie:** 1,3 </li> <li> **Samplewaarde:**<br/> </li><li> **Beschrijving:**<br/>De tijd die aan het hoofdstuk wordt besteed.  De waarde zal in het tijdformaat (HH:MM.:SS) in de Werkruimte van de Analyse en Rapporten &amp; Analytics worden getoond. In de Eigen Gegevens, het Pakhuis van Gegevens, en het Melden APIs zullen de waarden in seconden worden getoond.<br/>**Releasedatum: 13-09-18**</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.chapter.<br/>timePlayed)</li> <li> **Hartslag:**<br/> </li> </ul> | <ul> <li> **Beschikbaar:**<br/>Ja</li> <li> **Gereserveerde variabele:**<br/>event</li> <li> **Rapportnaam:**<br/>Tijd van hoofdstuk doorgebracht g</li> <li> **Contextgegevens:**<br/>(a.media.chapter.<br/>timePlayed)</li> <li> **Gegevensfeed:**<br/>N.v.t.</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.chapter.<br/>timePlayed)</li> </ul> |

## Verwante API&#39;s {#related_apis_section}

* Android - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* iOS - [createChapterObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:length:startTime:)
* Javascript - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)
