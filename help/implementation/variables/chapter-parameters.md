---
title: Hoofdstukparameters
description: "Leer over hoofdstukparameters voor implementatie, netwerk, en rapportering."
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
exl-id: 73da3e52-9498-478e-bfd7-8ff6c8e6bfc5
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 917c87d759a43f124dfb3e3ac7f6a441c65fde94
workflow-type: tm+mt
source-wordcount: '1142'
ht-degree: 0%

---

# Hoofdstukparameters{#chapter-parameters}

Dit onderwerp stelt een lijst van hoofdstuk en/of segmentgegevens, met inbegrip van de waarden van contextgegevens voor, die de Adobe via oplossingsvariabelen verzamelt.

Beschrijving van tabelgegevens:

* **Implementatie:** Informatie over implementatiewaarden en -vereisten
   * *Sleutel* - Variabele, stelt u handmatig in in uw app of automatisch in door de SDK van Adobe Media.
   * *Vereist* - Geeft aan of de parameter vereist is voor het bijhouden van basisvideo.
   * *Type* - Geeft het type aan van de variabele die moet worden ingesteld, de tekenreeks of het getal.
   * *Verzonden met* - Geeft aan wanneer de gegevens worden verzonden: *Start media* de analytische oproep die bij het starten van de media wordt verzonden; *Ad Start* is de analytische oproep die op ad start wordt verzonden, enzovoort; de *Sluiten* de vraag is de gecompileerde analytische vraag die rechtstreeks van de hartslagserver naar de analyseserver aan het eind van de media zitting, of het eind van de advertentie, het hoofdstuk, enz. wordt verzonden. De dichte vraag is niet beschikbaar in de vraag van het netwerkpakket.
   * *Min. SDK-versie* - Geeft aan welke SDK-versie u toegang tot de parameter nodig hebt.
   * *Samplewaarde* - Verstrekt voorbeeld van gemeenschappelijk veranderlijk gebruik.
* **Netwerkparameters:** Hiermee geeft u de waarden weer die worden doorgegeven aan Adobe Analytics- of Hartslagservers. Deze kolom toont de namen van de parameters die in de netwerkvraag worden gezien die door Adobe Media SDKs wordt geproduceerd.
* **Rapportage:** Informatie over het weergeven en analyseren van videogegevens.
   * *Beschikbaar* - Geeft aan of de gegevens standaard beschikbaar zijn in de rapportage (*Ja*), of aangepaste instelling vereist (*Aangepast*)
   * *Gereserveerde variabele* - Geeft aan of de gegevens zijn vastgelegd als een gebeurtenis, eVar, eigenschap of classificatie in een gereserveerde variabele.
   * *Rapportnaam* - Naam van het analyserapport van de Adobe voor de variabele
   * *Contextgegevens* - Naam van de Adobe Analytics-contextgegevens die aan de rapportserver worden doorgegeven en die in verwerkingsregels worden gebruikt.
   * *Gegevensfeed* - Kolomnaam voor variabele in Clickstream- of Live Stream-gegevensfeeds
   * *Audience Manager* - Trainingsnaam gevonden in Adobe Audience Manager

>[!IMPORTANT]
>
>Wijzig de classificatienamen niet voor onderstaande variabelen die onder Rapportage/Gereserveerde variabele worden beschreven als &quot;classificatie&quot;.\
>De mediaclassificaties worden gedefinieerd wanneer een rapportsuite is ingeschakeld voor het bijhouden van media. Van tijd tot tijd, voegt de Adobe nieuwe eigenschappen toe, en, wanneer dit voorkomt, moeten de klanten hun rapportsuites opnieuw toelaten om toegang tot de nieuwe media eigenschappen te krijgen. Tijdens het updateproces bepaalt de Adobe of de classificaties worden toegelaten door de namen van de variabelen te controleren. Als een van de ontbrekende elementen ontbreekt, voegt de Adobe de ontbrekende opnieuw toe.

## Metagegevens hoofdstuk {#chapter-metadata}

### Hoofdstuknaam

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-sleutel:**<br/>  [name](./chapter-parameters.md#related_apis_section) </li> <li> **API-sleutel:**<br/> media.chapter.bevriezingName </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Hoofdstukbegin, Hoofdstuk sluiten </li> <li> **Min. SDK-versie:** 1,3 </li> <li> **Samplewaarde:**<br/> &quot;The Big Bang Chapter 2 - Dating&quot; </li><li> **Omschrijving:**<br/> De naam van het hoofdstuk en/of segment.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>vriendelijkeName) </li> <li> **Hartslag:**<br/> (<code>s:stream:hoofdstuk_naam</code>) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Standaard gemaakt.  </li> <li> **Gereserveerde variabele:**<br/> Classificatie </li> <li> **Rapportnaam:**<br/> Hoofdstuknaam </li> <li> **Contextgegevens:**<br/> (a.media.chapter.<br/>vriendelijkeName) </li> <li> **Gegevensfeed:**<br/> NVT </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>vriendelijkeName) </li> <li> **XDM-veldpad:**<br/> media.mediaTimed.mediaChapter.<br/>chapterAssetReference.dc:title </li> <li> **XDM-veldpad voor verzameling:**<br/> mediaCollection.chapterDetails.FriName </li> <li> **XDM-veldpad rapporteren:**<br/> mediaReporting.chapterDetails.VriendschappelijkeNaam </li> </ul> |

### Hoofdstukpositie

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-sleutel:**<br/>  [positie](./chapter-parameters.md#related_apis_section) </li> <li> **API-sleutel:**<br/> media.hoofdstuk.index </li> <li> **Vereist:**<br/> SDK: Nee; API: Ja. </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Hoofdstuk sluiten </li> <li> **Min. SDK-versie:** 1,3 </li> <li> **Samplewaarde:**<br/> 2 </li><li> **Omschrijving:**<br/> De positie (index, geheel getal) van het hoofdstuk binnen de inhoud.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>positie) </li> <li> **Hartslag:**<br/> (<code>l:stream:hoofdstuk_pos</code>) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> Classificatie </li> <li> **Rapportnaam:**<br/> Hoofdstukpositie </li> <li> **Contextgegevens:**<br/> (a.media.chapter.<br/>positie) </li> <li> **Gegevensfeed:**<br/> NVT </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>positie) </li> <li> **XDM-veldpad:**<br/> media.mediaTimed.mediaChapter.<br/>hoofdstukAssetViewDetails.index </li> <li> **XDM-veldpad voor verzameling:**<br/> mediaCollection.chapterDetails.index </li> <li> **XDM-veldpad rapporteren:**<br/> mediaReporting.chapterDetails.index </li> </ul> |

### Verschuiving hoofdstuk

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-sleutel:**<br/>  [startTime](./chapter-parameters.md#related_apis_section) </li> <li> **API-sleutel:**<br/> media.hoofdstuk.offset </li> <li> **Vereist:**<br/> SDK: Nee; API: Ja. </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Hoofdstuk sluiten </li> <li> **Min. SDK-versie:** 1,3 </li> <li> **Samplewaarde:**<br/> 58 </li><li> **Omschrijving:**<br/> De verschuiving van het hoofdstuk binnen de inhoud (in seconden) vanaf het begin.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>verschuiving) </li> <li> **Hartslag:**<br/> (<code>l:stream:hoofdstuk_offset</code>) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> Classificatie </li> <li> **Rapportnaam:**<br/> Verschuiving hoofdstuk </li> <li> **Contextgegevens:**<br/> (a.media.chapter.<br/>verschuiving) </li> <li> **Gegevensfeed:**<br/> NVT </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>verschuiving) </li> <li> **XDM-veldpad:**<br/> media.mediaTimed.mediaChapter.<br/>hoofdstukAssetViewDetails.offset </li> <li> **XDM-veldpad voor verzameling:**<br/> mediaCollection.chapterDetails.offset </li> <li> **XDM-veldpad rapporteren:**<br/> mediaReporting.chapterDetails.offset </li> </ul> |

### Hoofdstuklengte

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-sleutel:**<br/> </li> <li> **API-sleutel:**<br/> media.hoofdstuk.length </li> <li> **Vereist:**<br/> SDK: Nee; API: Ja. </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Hoofdstuk sluiten </li> <li> **Min. SDK-versie:** 1,3 </li> <li> **Samplewaarde:**<br/> 486 </li><li> **Omschrijving:**<br/> De lengte van het hoofdstuk, in seconden.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>lengte) </li> <li> **Hartslag:**<br/> (<code>l:stream:hoofdstuk_lengte</code>) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> Classificatie </li> <li> **Rapportnaam:**<br/> Hoofdstuklengte </li> <li> **Contextgegevens:**<br/> (a.media.chapter.<br/>lengte) </li> <li> **Gegevensfeed:**<br/> NVT </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>lengte) </li> <li> **XDM-veldpad:**<br/> media.mediaTimed.mediaChapter.<br/>chapterAssetReference.xmpDM:duration </li> <li> **XDM-veldpad voor verzameling:**<br/> mediaCollection.chapterDetails.length </li> <li> **XDM-veldpad rapporteren:**<br/> mediaReporting.chapterDetails.length </li> </ul> |

### Hoofdstuk

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> NVT </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Hoofdstuk sluiten </li> <li> **Min. SDK-versie:** 1,3 </li> <li> **Samplewaarde:**<br/> </li><li> **Omschrijving:**<br/> De automatisch gegenereerde id van het hoofdstuk.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>name) </li> <li> **Hartslag:**<br/> (<code>s:stream:hoofdstuk_id</code>) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Hoofdstuk </li> <li> **Contextgegevens:**<br/> (a.media.chapter.<br/>name) </li> <li> **Gegevensfeed:**<br/> videohoofdstuk </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>name) </li> <li> **XDM-veldpad:**<br/> media.mediaTimed.mediaChapter.<br/>hoofdstukAssetReference.@id </li> <li> **XDM-veldpad rapporteren:**<br/> mediaReporting.chapterDetails.ID </li> </ul> |

## Hoofdstukstatistieken {#chapter-Metrics}

### Begin hoofdstuk

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen  </li> <li> **API-sleutel:**<br/> NVT </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Begin hoofdstuk </li> <li> **Min. SDK-versie:** 1,3 </li> <li> **Samplewaarde:**<br/> TRUE </li><li> **Omschrijving:**<br/> Het aantal hoofdstukken begint.  **Belangrijk:**  Als deze gebeurtenis is ingesteld, is TRUE de enige mogelijke waarde. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>weergave) </li> <li> **Hartslag:**<br/> (<code>s:event:</code><br/>type=hoofdstuk_start) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Hoofdstuk start</li> <li> **Contextgegevens:**<br/> (a.media.chapter.<br/>weergave) </li> <li> **Gegevensfeed:**<br/> NVT </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>weergave) </li> <li> **XDM-veldpad:**<br/> media.mediaTimed.chapterCount.<br/>value > 0 => &quot;TRUE&quot; </li> <li> **XDM-veldpad rapporteren:**<br/> mediaReporting.chapterDetails.isStarted </li> </ul> |

### Hoofdstuk voltooid

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen  </li> <li> **API-sleutel:**<br/> NVT </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Hoofdstuk sluiten </li> <li> **Min. SDK-versie:** 1,3</li> <li> **Samplewaarde:**<br/> TRUE </li><li> **Omschrijving:**<br/> Het aantal hoofdstukken is voltooid.  **Belangrijk:**  Als deze gebeurtenis is ingesteld, is TRUE de enige mogelijke waarde. Als deze gebeurtenis niet is ingesteld, wordt geen waarde verzonden.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>complete) </li> <li> **Hartslag:**<br/> (<code>s:event:</code><br/>type=chapter_complete) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Hoofdstuk voltooid</li> <li> **Contextgegevens:**<br/> (a.media.chapter.<br/>complete) </li> <li> **Gegevensfeed:**<br/> NVT </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>complete) </li> <li> **XDM-veldpad:**<br/> media.mediaTimed.mediaChapter.<br/>completes.value </li> <li> **XDM-veldpad rapporteren:**<br/> mediaReporting.chapterDetails.isCompleted </li> </ul> |

### Tijd besteed aan hoofdstuk

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen  </li> <li> **API-sleutel:**<br/> NVT </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Hoofdstuk sluiten </li> <li> **Min. SDK-versie:** 1,3 </li> <li> **Samplewaarde:**<br/> </li><li> **Omschrijving:**<br/> De tijd die aan het hoofdstuk wordt doorgebracht.  De waarde wordt weergegeven in de tijdnotatie (<code>HH:MM:SS</code>) in Analysis Workspace en Reports &amp; Analytics. In de Diervoeders van Gegevens, Data Warehouse, en Rapporterende APIs zullen de waarden in seconden worden getoond. <br/>**Releasedatum: 13-09-18**   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>timePlayed) </li> <li> **Hartslag:**<br/> </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Tijd besteed aan hoofdstuk</li> <li> **Contextgegevens:**<br/> (a.media.chapter.<br/>timePlayed) </li> <li> **Gegevensfeed:**<br/> NVT </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>timePlayed) </li> <li> **XDM-veldpad:**<br/> media.mediaTimed.mediaChapter.<br/>timePlayed.value </li> <li> **XDM-veldpad rapporteren:**<br/> mediaReporting.chapterDetails.timePlayed </li> </ul> |

## Verwante API&#39;s {#related_apis_section}

* Android - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* IOS - [createChapterObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:length:startTime:)
* JavaScript - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)
