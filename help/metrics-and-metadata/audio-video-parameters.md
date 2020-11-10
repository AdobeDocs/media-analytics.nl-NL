---
title: Parameters voor audio en video
description: null
uuid: fdacfb8b-db3e-46fb-b9ad-c3a749555b2a
translation-type: tm+mt
source-git-commit: 4dad6507966e30accfb4f6c2eb5f1d6a5507d29d
workflow-type: tm+mt
source-wordcount: '6234'
ht-degree: 2%

---


# Parameters voor audio en video{#audio-and-video-parameters}

>[!IMPORTANT]
>
>Op 7 februari 2019 heeft Adobe Analytics for Video en Audio een naamswijziging in metrische vorm uitgebracht. <i>Media wordt gestart</i> wordt nu <i>Start media</i>. Deze wijziging werd aangebracht om de industriestandaarden in metriek en rapportage weer te geven en om de metrische gegevens gemakkelijk te kunnen identificeren in de rapportage.

>[!NOTE]
>
>Vanaf 13 september 2018 is er een wijziging aangebracht in de labels voor bepaalde afmetingen, meetgegevens en rapporten, zodat video- en audioanalyses op verschillende inhoud kunnen worden bijgehouden. De labels die zijn gewijzigd, zijn onder andere: *video wordt gestart* tot *media initieert*, *videolengte* tot *lengte van inhoud*, en *videonaam* tot *inhoudsnaam*. De videorapporten in Reports and Analytics zijn allemaal bijgewerkt met de naam &quot;Media&quot; in plaats van &quot;Video&quot;. De veranderingen van het etiket veranderden geen gegevensinzameling of historische gegevens. Houd rekening met deze wijzigingen als u deze gebruikt binnen Report Builder of in andere externe automatische gegevenspullen die mogelijk door deze wijziging worden beïnvloed.

Dit onderwerp stelt een lijst van audio en videoinhoudsgegevens, met inbegrip van contextgegevenswaarden voor, die Adobe via oplossingsvariabelen verzamelt.

Beschrijving van tabelgegevens:

* **Implementatie:** Informatie over implementatiewaarden en -vereisten
   * *Sleutel* - Variabele, stelt u deze handmatig in in uw app in of automatisch door de Adobe Media SDK.
   * *Vereist* - Geeft aan of de parameter vereist is voor het bijhouden van elementaire audio en video.
   * *Type* - Geeft het type aan van de variabele die moet worden ingesteld, de tekenreeks of het getal.
   * *Verzonden met* - Geeft aan wanneer de gegevens worden verzonden: *Start media* de analytische oproep die bij het starten van de media wordt verzonden; *Ad Start* wordt de analytische oproep verzonden op ad start, enzovoort; de *Sluiten* de vraag is de gecompileerde analytische vraag die rechtstreeks van de hartslagserver naar de analyseserver aan het eind van de media zitting, of het eind van de advertentie, het hoofdstuk, enz. wordt verzonden. De dichte vraag is niet beschikbaar in de vraag van het netwerkpakket.
   * *Min. SDK-versie* - Geeft aan welke SDK-versie u toegang tot de parameter nodig hebt.
   * *Samplewaarde* - Verstrekt voorbeeld van gemeenschappelijk veranderlijk gebruik.
* **Netwerkparameters:** Hiermee geeft u de waarden weer die worden doorgegeven aan Adobe Analytics- of Hartslagservers. Deze kolom toont de namen van de parameters die in de netwerkvraag worden gezien die door Adobe Media SDKs wordt geproduceerd.
* **Rapportage:** Informatie over het weergeven en analyseren van audio- en videogegevens.
   * *Beschikbaar* - Geeft aan of de gegevens standaard beschikbaar zijn in de rapportage (*Ja*), of aangepaste instelling vereist (*Aangepast*)
   * *Gereserveerde variabele* - Geeft aan of de gegevens zijn vastgelegd als een gebeurtenis, eVar, eigenschap of classificatie in een gereserveerde variabele.
   * *Verlopen* - Geeft aan of de gegevens verlopen na elke aanraking of na elk bezoek.
   * *Rapportnaam* - Naam van Adobe Analytics-rapport voor variabele
   * *Contextgegevens* - Naam van de Adobe Analytics-contextgegevens die aan de rapportserver worden doorgegeven en die in verwerkingsregels worden gebruikt.
   * *Gegevensfeed* - Kolomnaam voor variabele in Clickstream- of Live Stream-gegevensfeeds
   * *Audience Manager* - Trainingsnaam gevonden in Adobe Audience Manager

>[!IMPORTANT]
>
>Wijzig de classificatienamen niet voor onderstaande variabelen die onder Rapportage/Gereserveerde variabele worden beschreven als &quot;classificatie&quot;.\
>De mediaclassificaties worden gedefinieerd wanneer een rapportsuite is ingeschakeld voor het bijhouden van media. Van tijd tot tijd, voegt Adobe nieuwe eigenschappen toe, en, wanneer dit voorkomt, moeten de klanten hun rapportsuites opnieuw toelaten om toegang tot de nieuwe media eigenschappen te krijgen. Tijdens het updateproces bepaalt Adobe of de classificaties worden toegelaten door de namen van de variabelen te controleren. Als een van deze ontbrekende elementen ontbreekt, voegt Adobe de ontbrekende opnieuw toe.

## Gegevens over kernstuurmedia {#core-audio-and-video-data}

### Type stream {#stream-type}

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **API-sleutel:**<br/> media.streamType </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 2,2 <br/><br/>Beschikbaar in [API-overzicht van mediagroep](/help/media-collection-api/mc-api-overview.md) of [SDK&#39;s downloaden - Versies 2.2](/help/sdk-implement/download-sdks.md).  </li>  <li> **Samplewaarde:**<br/> &quot;video&quot; </li> <li> **Omschrijving:**<br/> Hiermee wordt het streamtype aangegeven. Geldige waarden zijn &quot;audio&quot;, &quot;video&quot; en &quot; &quot;.  <br/><br/>[Segmenten rapporteren](/help/metrics-and-metadata/segments.md): <br/><br/>Type mediastroom: Alles - <br/>alle mediastreamgegevens segmenteren; Regel: Inhoud (ID) bestaat <br/><br/>Type mediastroom: Audio - <br/>alle audiostreamgegevens segmenteren; Regel: Content (ID) exists AND Media Stream Type = audio <br/><br/>Type mediastroom: &quot;Video&quot; - <br/>alle videostreamgegevens segmenteren; Regel: Inhoud (ID) bestaat EN Mediastroomtype != audio <br/><br/> **Releasedatum: 13-09-18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.streamType) </li> <li> **Hartmaten:**<br/> (s:meta:<br/>a.media.streamType) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Bij BEZOEK </li> <li> **Rapportnaam:**<br/> Inhoud </li> <li> **Contextgegevens:**<br/> (a.media.streamType) </li> <li> **Gegevensfeed:**<br/> videostreaming </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.streamType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### Inhoud-id

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> [mediaId](./audio-video-parameters.md#create-media-object) </li> <li> **API-sleutel:**<br/> media.id </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> &quot;4586695ABC&quot; </li> <li>**Omschrijving:**<br/> Inhoud-id van de inhoud, die kan worden gebruikt om terug te koppelen naar andere industrie-/CMS-id&#39;s, gelijk aan de laatste waarde van `s:asset:video_id.` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.name) </li> <li> **Hartmaten:**<br/> (s:asset:video_id) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Bij BEZOEK </li> <li> **Rapportnaam:**<br/> Inhoud </li> <li> **Contextgegevens:**<br/> (a.media.name) </li> <li> **Gegevensfeed:**<br/> video </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.name) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType,
                                            MediaHeartbeat.MediaType mediaType)
```

### Content Length (variable)

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **API-sleutel:**<br/> media.length </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> VOD: 128; Live: 86400; Lineair: 1800. </li><li> **Omschrijving:**<br/> Cliplengte/runtime - Dit is de maximale lengte (of duur) van de inhoud die wordt verbruikt (in seconden). Deze is gelijk aan de laatste waarde van `l:asset:length` vanuit gebeurtenissen van het type Main. <br/>Indien `l:asset:length` is niet ingesteld, dan is de laatste waarde van `l:asset:duration` wordt gebruikt. <br/>Bij rapportage is Videolengte de classificatie en Content Length (variabele) is de eVar.  <br/> **Belangrijk:** Deze eigenschap wordt gebruikt voor het berekenen van verschillende meetgegevens, zoals gegevens over het bijhouden van de voortgang en Gemiddeld Minuut publiek. Als deze niet is ingesteld of niet groter is dan nul, zijn deze cijfers niet beschikbaar.  Voor Live media met een onbekende duur is de standaardwaarde 86400. <br/>Voor versie 1.5.1 was dit `l:asset:duration`; na 1.5.1 `l:asset:length.` <br/> **Releasedatum: 13-09-18** </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.length) </li> <li> **Hartmaten:**<br/> (l:asset:length) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Content Length (variable) </li> <li> **Contextgegevens:**<br/> (a.media.length) </li> <li> **Gegevensfeed:**<br/> videolengte </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType,
                                            MediaHeartbeat.MediaType mediaType)
```

### Videolengte

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **API-sleutel:**<br/> media.length </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> VOD: 128; Live: 86400; Lineair: 1800. </li> <li> **Omschrijving:**<br/> Cliplengte/runtime - Dit is de maximale lengte (of duur) van de inhoud die wordt verbruikt (in seconden). Deze is gelijk aan de laatste waarde van `l:asset:length` vanuit gebeurtenissen van het type Main. Indien `l:asset:length` is niet ingesteld, dan is de laatste waarde van `l:asset:duration` wordt gebruikt. Bij rapportage is Videolengte de classificatie en Content Length (variabele) is de eVar.  <br/> **Belangrijk:** Deze eigenschap wordt gebruikt voor het berekenen van verschillende meetgegevens, zoals gegevens over het bijhouden van de voortgang en Gemiddeld Minuut publiek. Als deze niet is ingesteld of niet groter is dan nul, zijn deze cijfers niet beschikbaar.  Voor Live media met een onbekende duur is de standaardwaarde 86400. Voor versie 1.5.1 was dit `l:asset:duration`; na 1.5.1 `l:asset:length.`<br/> **Releasedatum: 13-09-18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.length) </li> <li> **Hartmaten:**<br/> (l:asset:length) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> Classificatie </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Videolengte </li> <li> **Contextgegevens:**<br/> (a.media.length) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType,
                                            MediaHeartbeat.MediaType mediaType)
```

### Inhoudstype

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>  [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **API-sleutel:**<br/> media.contentType </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> beperkte tekenreeks </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> &quot;vod&quot; </li> <li> **Omschrijving:**<br/> Beschikbare waarden per **Type stream**: <br/> _Audio:_ &quot;song&quot;, &quot;podcast&quot;, &quot;audiobook&quot;, &quot;radio&quot; <br/> _Video:_ &quot;VoD&quot;, &quot;Live&quot;, &quot;Linear&quot;, &quot;UGC&quot;, &quot;DVoD&quot; <br/> Klanten kunnen aangepaste waarden voor deze parameter opgeven. Dit is gelijk aan `s:stream:type.` Als dat niet is ingesteld, is dit gelijk aan `missing_content_type.` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.contentType) </li> <li> **Hartmaten:**<br/> (s:stream:type) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Inhoudstype </li> <li> **Contextgegevens:**<br/> (a.contentType) </li> <li> **Gegevensfeed:**<br/> videocontenttype </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.contentType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### Mediasessie-id

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> Verkregen van backend </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.8. </li> <li> **Samplewaarde:**<br/> 1482236761294786918253 </li> <li> **Omschrijving:**<br/> Dit identificeert een instantie van een inhoudsstroom uniek aan een individuele playback.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.vsid) </li> <li> **Hartslag:**<br/> (s:event:sid) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Verwerkingsregel gebruiken </li> <li> **Gereserveerde variabele:**<br/> N.v.t. </li> <li> **Rapportnaam:**<br/> Aangepast </li> <li> **Contextgegevens:**<br/> (a.media.vsid) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.vsid) </li> </ul> |

### Markering voor gedownloade media

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> `config.downloadedcontent` </li> <li> **API-sleutel:**<br/> Verkregen van backend </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> boolean </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** <br/>Android- en iOS-extensie v1.1.0 starten </li> <li> **Samplewaarde:**<br/> true </li> <li> **Omschrijving:**<br/> Ingesteld op true wanneer de hit wordt gegenereerd als gevolg van het afspelen van een gedownloade mediasessie voor inhoud. Niet aanwezig wanneer gedownloade inhoud niet wordt afgespeeld.<br/><br/>[Starten](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#create-a-media-tracker-with-optional-configuration)  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.download) </li> <li> **Hartslag:**<br/> (s:meta:a.media.downloaded) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Aangepaste verwerkingsregel gebruiken </li> <li> **Gereserveerde variabele:**<br/> N.v.t. </li> <li> **Rapportnaam:**<br/> Aangepast </li> <li> **Contextgegevens:**<br/> (a.media.download) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.downloaded) </li> </ul> |

### Naam van inhoudspeler

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> [playerName](./audio-video-parameters.md#config-media-object) </li> <li> **API-sleutel:**<br/> media.playerName </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> &quot;Brightcove&quot; </li> <li> **Omschrijving:**<br/> Naam van de speler.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>playerName) </li> <li> **Hartmaten:**<br/> (s:sp:player_name) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Naam van inhoudspeler </li> <li> **Contextgegevens:**<br/> (a.media.playerName) </li> <li> **Gegevensfeed:**<br/> videoplayernaam </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.playerName) </li> </ul> |

### Inhoudskanaal

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>  [channel](./audio-video-parameters.md#config-media-object) </li> <li> **API-sleutel:**<br/> media.channel </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> &quot;Sport&quot; </li> <li> **Omschrijving:**<br/> Distribution Station/Channels of waar de inhoud wordt afgespeeld. Elke tekenreekswaarde wordt hier geaccepteerd.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.channel) </li> <li> **Hartmaten:**<br/> (s:sp:channel) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Inhoudskanaal </li> <li> **Contextgegevens:**<br/> (a.media.channel) </li> <li> **Gegevensfeed:**<br/> videokanaal </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.channel) </li> </ul> |

### Segment Inhoud

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> &quot;0-10&quot; </li> <li> **Omschrijving:**<br/> Het interval dat het gedeelte van de inhoud beschrijft dat is weergegeven (in minuten). Het segment wordt berekend als min en max van de waarden van de afspeelkop tijdens een afspeelsessie.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> N.v.t. </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Segment Inhoud </li> <li> **Contextgegevens:**<br/> (a.media.segment) </li> <li> **Gegevensfeed:**<br/> videosegment </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.segment) </li> </ul> |

### Inhoudsnaam (variabele)

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>  [name](./audio-video-parameters.md#create-media-object) </li> <li> **API-sleutel:**<br/> media.name </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.1. </li> <li> **Samplewaarde:**<br/> &quot;The Big Bang Theory&quot; </li> <li> **Omschrijving:**<br/> Dit is de &#39;vriendelijke&#39; (leesbare) naam van de inhoud, gelijk aan de laatste waarde van `s:asset:name.`<br/>In rapportering, is de Naam van de Video de classificatie, en de Naam van de Inhoud (variabele) is de eVar. <br/> **Releasedatum: 13-09-18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>vriendelijkeName) </li> <li> **Hartmaten:**<br/> (s:asset:name) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Inhoudsnaam (variabele) </li> <li> **Contextgegevens:**<br/> (a.media.vriendelijkeName) </li> <li> **Gegevensfeed:**<br/> videonaam </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.vriendelijkeName) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType,
                                            MediaHeartbeat.MediaType mediaType)
```

### Videonaam

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>  [name](./audio-video-parameters.md#config-media-object) </li> <li> **API-sleutel:**<br/> media.name </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.1. </li> <li> **Samplewaarde:**<br/> &quot;The Big Bang Theory&quot; </li> <li> **Omschrijving:**<br/> Dit is de &#39;vriendelijke&#39; (leesbare) naam van de inhoud, gelijk aan de laatste waarde van `s:asset:name.` <br/>In rapportering, is de Naam van de Video de classificatie, en de Naam van de Inhoud (variabele) is de eVar.  <br/> **Releasedatum: 13-09-18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>vriendelijkeName) </li> <li> **Hartmaten:**<br/> (s:asset:name) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> Classificatie </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Videonaam </li> <li> **Contextgegevens:**<br/> (a.media.vriendelijkeName) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.vriendelijkeName) </li> </ul> |

### Videopad

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Start media </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> &quot;4586695ABC&quot; </li> <li> **Omschrijving:**<br/> Biedt de mogelijkheid om het pad van een viewer voor een site en/of een app bij te houden en het pad te zien dat deze hebben ingenomen om een bepaalde video weer te geven. Een geheel getal en/of lettercombinatie.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.name) </li> <li> **Hartmaten:**<br/> (s:asset:video_id) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> prop </li> <li> **Rapportnaam:**<br/> Videopad </li> <li> **Contextgegevens:**<br/> (a.media.name) </li> <li> **Gegevensfeed:**<br/> videopath </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.name) </li> </ul> |

### SDK-versie

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>  [appVersion](./audio-video-parameters.md#config-media-object) </li> <li> **API-sleutel:**<br/> media.sdkVersion </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7. </li> <li> **Samplewaarde:**<br/> &quot;2.62.0_release&quot; </li> <li> **Omschrijving:**<br/> De SDK-versie die door de speler wordt gebruikt. Dit kan elke aangepaste waarde hebben die voor uw speler zinnig is. <br/><br/>Klanten moeten hun eigen verwerkingsregels maken om de waarde voor rapportage beschikbaar te hebben.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>sdkVersion) </li> <li> **Hartmaten:**<br/> (s:sp:sdk) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Aangepaste verwerkingsregel gebruiken </li> <li> **Gereserveerde variabele:**<br/> N.v.t. </li> <li> **Rapportnaam:**<br/> </li> <li> **Contextgegevens:**<br/> (a.media.sdkVersion) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.sdkVersion) </li> </ul> |

### VHL-versie

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7. </li> <li> **Samplewaarde:**<br/> &quot;js-2.0.1.88-c8c0b1&quot; </li> <li> **Omschrijving:**<br/> De SDK-versie van Media die wordt gebruikt voor de volgende sessie. <br/><br/>Klanten moeten hun eigen verwerkingsregels maken om de waarde voor rapportage beschikbaar te hebben.  <br/><br/>[MediaHeartbone.version();](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html) </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>vhlVersion) </li> <li> **Hartmaten:**<br/> (s:sp:hb_version) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Aangepaste verwerkingsregel gebruiken </li> <li> **Gereserveerde variabele:**<br/> N.v.t. </li> <li> **Rapportnaam:**<br/> Aangepast </li> <li> **Contextgegevens:**<br/> (a.media.vhlVersion) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.vhlVersion) </li> </ul> |

## Metagegevens van standaard stuurmedia {#standard-audio-and-video-metadata}

### Tonen

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> TONEN </li> <li> **API-sleutel:**<br/> media.show </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7. </li> <li> **Samplewaarde:**<br/> &quot;Modern Familie&quot; &quot;De Laatste Dans&quot; &quot;New Girl&quot; </li> <li> **Omschrijving:**<br/> Naam programma/serie <br/>De Naam van het programma wordt vereist slechts als de show deel van een reeks uitmaakt.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.show) </li> <li> **Hartmaten:**<br/> (s:meta:<br/>a.media.show) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Tonen </li> <li> **Contextgegevens:**<br/> (a.media.show) </li> <li> **Gegevensfeed:**<br/> videoshow </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.show) </li> </ul> |

### Stroomindeling

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> STREAM_FORMAT </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7. </li> <li> **Samplewaarde:**<br/> &quot;Live&quot; </li> <li> **Omschrijving:**<br/> Indeling van de stream (Live, VOD, Lineair).  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.format) </li> <li> **Hartmaten:**<br/> (s:meta:<br/>a.media.format) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Aangepaste verwerkingsregel gebruiken </li> <li> **Gereserveerde variabele:**<br/> N.v.t. </li> <li> **Rapportnaam:**<br/> Aangepast </li> <li> **Contextgegevens:**<br/> (a.media.format) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.format) </li> </ul> |

### Seizoen

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> SEASON </li> <li> **API-sleutel:**<br/> media.seizoen </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7. </li> <li> **Samplewaarde:**<br/> &quot;2&quot; </li> <li> **Omschrijving:**<br/> Het seizoensnummer waartoe de show behoort.  Reeks seizoen is alleen vereist als de presentatie deel uitmaakt van een reeks.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.seizoen) </li> <li> **Hartmaten:**<br/> (s:meta:<br/>a.media.seizoen) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Seizoen </li> <li> **Contextgegevens:**<br/> (a.media.seizoen) </li> <li> **Gegevensfeed:**<br/> videoseizoen </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.seizoen) </li> </ul> |

### Episode

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> EPISODE </li> <li> **API-sleutel:**<br/> media.episode </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7. </li> <li> **Samplewaarde:**<br/> &quot;13&quot; </li> <li> **Omschrijving:**<br/> The number of the episode.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.episode) </li> <li> **Hartmaten:**<br/> (s:meta:<br/>a.media.episode) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Episode </li> <li> **Contextgegevens:**<br/> (a.media.episode) </li> <li> **Gegevensfeed:**<br/> videoaflevering </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.episode) </li> </ul> |

### Element-id

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> ASSET_ID </li> <li> **API-sleutel:**<br/> media.assetId </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7. </li> <li> **Samplewaarde:**<br/> &quot;89745363&quot; </li> <li> **Omschrijving:**<br/> Dit is de unieke id voor de inhoud van het media-element, zoals de aflevering-id van de tv-reeks, de id van het filmelement of de livegebeurtenis. Deze id&#39;s zijn doorgaans afgeleid van metagegevensautoriteiten zoals EIDR, TMS/Gracenote of Rovi. Deze id&#39;s kunnen ook afkomstig zijn van andere bedrijfseigen of interne systemen.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.asset) </li> <li> **Hartmaten:**<br/> (s:meta:<br/>a.media.asset) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> Classificatie </li> <li> **Rapportnaam:**<br/> Element-id </li> <li> **Contextgegevens:**<br/> (a.media.asset) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.asset) </li> </ul> |

### Genre

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> GENRE </li> <li> **API-sleutel:**<br/> media.genre </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7. </li> <li> **Samplewaarde:**<br/> &quot;Drama&quot;, &quot;Comedy&quot; </li> <li> **Omschrijving:**<br/> Type of groepering van inhoud zoals gedefinieerd door de producent van inhoud. Waarden moeten worden gescheiden door komma&#39;s in een variabele implementatie. Bij het rapporteren wordt elke waarde in een regelitem opgedeeld door de eVar van de lijst, waarbij elk regelitem een gelijk metrisch gewicht krijgt.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.genre) </li> <li> **Hartmaten:**<br/> (s:meta:<br/>a.media.genre) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> EVar List </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Genre </li> <li> **Contextgegevens:**<br/> (a.media.genre) </li> <li> **Gegevensfeed:**<br/> videogene </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.genre) </li> </ul> |

### Eerste luchtdatum

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> FIRST_AIR_DATE </li> <li> **API-sleutel:**<br/> media.firstAirDate </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Start media </li> <li> **Min. SDK-versie:** 1.5.7. </li> <li> **Samplewaarde:**<br/> &quot;2016-01-25&quot; </li> <li> **Omschrijving:**<br/> De datum waarop de inhoud voor het eerst op de televisie is uitgezonden. Elke datumnotatie is acceptabel, maar Adobe raadt aan: YYYY-MM-DD </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.airDate) </li> <li> **Hartmaten:**<br/> (s:meta:<br/>a.media.airDate) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> Classificatie </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Eerste luchtdatum </li> <li> **Contextgegevens:**<br/> (a.media.airDate) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.airDate) </li> </ul> |

### Eerste digitale datum

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> FIRST_DIGITAL_DATE </li> <li> **API-sleutel:**<br/> media.firstDigitalDate </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7. </li> <li> **Samplewaarde:**<br/> &quot;2016-01-25&quot; </li> <li> **Omschrijving:**<br/> De datum waarop de inhoud voor het eerst via een digitaal kanaal of platform is verzonden. Elke datumnotatie is acceptabel, maar Adobe raadt aan: YYYY-MM-DD </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.digitalDate) </li> <li> **Hartmaten:**<br/> (s:meta:<br/>a.media.digitalDate) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> Classificatie </li> <li> **Rapportnaam:**<br/> Eerste digitale datum </li> <li> **Contextgegevens:**<br/> (a.media.digitalDate) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.digitalDate) </li> </ul> |

### Classificatie van inhoud

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> RATING </li> <li> **API-sleutel:**<br/> media.rating </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7. </li> <li> **Samplewaarde:**<br/> TVY, TVG, TVPG, TVMA </li> <li> **Omschrijving:**<br/> Classificatie zoals gedefinieerd in de TV Parental Guidelines.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.rating) </li> <li> **Hartmaten:**<br/> (s:meta:<br/>a.media.rating) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> Classificatie </li> <li> **Rapportnaam:**<br/> Classificatie van inhoud </li> <li> **Contextgegevens:**<br/> (a.media.rating) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.rating) </li> </ul> |

### Maker

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> ORIGINATOR </li> <li> **API-sleutel:**<br/> media.originator </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7. </li> <li> **Samplewaarde:**<br/> &quot;Warner Brothers&quot;, &quot;Sony&quot;, &quot;Disney&quot; </li> <li> **Omschrijving:**<br/> Maker van de inhoud.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.originator) </li> <li> **Hartmaten:**<br/> (s:meta:<br/>a.media.originator) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> Classificatie </li> <li> **Rapportnaam:**<br/> Maker </li> <li> **Contextgegevens:**<br/> (a.media.originator) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.originator) </li> </ul> |

### Netwerk

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> NETWERK </li> <li> **API-sleutel:**<br/> media.network </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7. </li> <li> **Samplewaarde:**<br/> &quot;Fox&quot;, &quot;Bravo&quot;, &quot;ESPN&quot; </li> <li> **Omschrijving:**<br/> De netwerk-/kanaalnaam.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.network) </li> <li> **Hartmaten:**<br/> (s:meta:<br/>a.media.network) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Netwerk </li> <li> **Contextgegevens:**<br/> (a.media.network) </li> <li> **Gegevensfeed:**<br/> videonetwerk </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.network) </li> </ul> |

### Tekst tonen

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> SHOW_TYPE </li> <li> **API-sleutel:**<br/> media.showType </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7. </li> <li> **Samplewaarde:**<br/> &quot;0&quot; = volledige aflevering; &quot;1&quot; = Voorbeeld/aanhangwagen; &quot;2&quot; = Clip; &quot;3&quot; = Overige. </li> <li> **Omschrijving:**<br/> Type inhoud, uitgedrukt als een geheel getal tussen 0 en 3.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.type) </li> <li> **Hartmaten:**<br/> (s:meta:<br/>a.media.type) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Tekst tonen </li> <li> **Contextgegevens:**<br/> (a.media.type) </li> <li> **Gegevensfeed:**<br/> videoshowtype </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.type) </li> </ul> |

### MVPD

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> MVPD </li> <li> **API-sleutel:**<br/> media.pass.mvpd </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7. </li> <li> **Samplewaarde:**<br/> &quot;Comcast&quot;, &quot;DirecTV&quot;, &quot;Dish&quot; </li> <li> **Omschrijving:**<br/> MVPD verstrekt via Adobe authentificatie.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.pass.mvpd) </li> <li> **Hartmaten:**<br/> (s:meta:<br/>a.media.pass.<br/>mvpd) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> MVPD </li> <li> **Contextgegevens:**<br/> (a.media.pass.mvpd) </li> <li> **Gegevensfeed:**<br/> videomvpd </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pass.mvpd) </li> </ul> |

### Geautoriseerd

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> GEMACHTIGD </li> <li> **API-sleutel:**<br/> media.pass.auth </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7. </li> <li> **Samplewaarde:**<br/> &quot;TRUE&quot; </li> <li> **Omschrijving:**<br/> De gebruiker is geautoriseerd via Adobe-verificatie.  <br/>**Belangrijk:** Dit kan alleen waar zijn als het is ingesteld. Als deze niet is ingesteld, wordt geen waarde geretourneerd.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.pass.auth) </li> <li> **Hartmaten:**<br/> (s:meta:<br/>a.media.pass.<br/>auth) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Geautoriseerd </li> <li> **Contextgegevens:**<br/> (a.media.pass.auth) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pass.auth) </li> </ul> |

### Dagdeel

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> DAY_PART </li> <li> **API-sleutel:**<br/> media.dayPart </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7. </li> <li> **Samplewaarde:**<br/> </li> <li> **Omschrijving:**<br/> Een eigenschap die de tijd definieert van de dag waarop de inhoud werd uitgezonden of afgespeeld. Dit zou om het even welke waarde kunnen hebben die zonodig door klanten wordt geplaatst.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.dayPart) </li> <li> **Hartmaten:**<br/> (s:meta:<br/>a.media.dayPart) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Dagdeel </li> <li> **Contextgegevens:**<br/> (a.media.dayPart) </li> <li> **Gegevensfeed:**<br/> videodagverblijf </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.dayPart) </li> </ul> |

### Type mediafeed

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> VOEDING </li> <li> **API-sleutel:**<br/> media.feed </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7. </li> <li> **Samplewaarde:**<br/> &quot;East-HD&quot;, &quot;West-HD&quot;, &quot;East-SD&quot; </li> <li> **Omschrijving:**<br/> Type diervoeder.  <br/> **Releasedatum: 13-09-18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.feed) </li> <li> **Hartmaten:**<br/> (s:meta:<br/>a.media.feed) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> Type mediafeed </li> <li> **Contextgegevens:**<br/> (a.media.feed) </li> <li> **Gegevensfeed:**<br/> videofeedtype </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.feed) </li> </ul> |

### Artiest

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> </li> <li> **API-sleutel:**<br/> media.artiest </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7. <br/>Beschikbaar in [Overzicht van mediagroep](/help/media-collection-api/mc-api-overview.md) of [SDK&#39;s downloaden - Versies 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Samplewaarde:**<br/> &quot;The Beatles&quot; </li> <li> **Omschrijving:**<br/> Naam van de artiest.  <br/> **Releasedatum: 13-09-18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.artiest) </li> <li> **Hartmaten:**<br/> (s:meta:<br/>a.media.artiest) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> </li> <li> **Contextgegevens:**<br/> (a.media.artiest) </li> <li> **Gegevensfeed:**<br/> videoaudiokunstenaar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.artiest) </li> </ul> |

### Album

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> </li> <li> **API-sleutel:**<br/> media.album </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7. <br/>Beschikbaar in [Overzicht van mediagroep](/help/media-collection-api/mc-api-overview.md) of [SDK&#39;s downloaden - Versies 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Samplewaarde:**<br/> &quot;Revolver&quot; </li> <li> **Omschrijving:**<br/> Naam van het album.  <br/> **Releasedatum: 13-09-18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.album) </li> <li> **Hartmaten:**<br/> (s:meta:<br/>a.media.album) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> </li> <li> **Contextgegevens:**<br/> (a.media.album) </li> <li> **Gegevensfeed:**<br/> videoaudioalbum </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.album) </li> </ul> |

### Label

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> </li> <li> **API-sleutel:**<br/> media.label </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7. <br/>Beschikbaar in [Overzicht van mediagroep](/help/media-collection-api/mc-api-overview.md) of [SDK&#39;s downloaden - Versies 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Samplewaarde:**<br/> &quot;Revolver&quot; </li> <li> **Omschrijving:**<br/> Naam van het recordlabel.  <br/> **Releasedatum: 13-09-18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.label) </li> <li> **Hartmaten:**<br/> (s:meta:<br/>a.media.label) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> </li> <li> **Contextgegevens:**<br/> (a.media.label) </li> <li> **Gegevensfeed:**<br/> videoaudiolabel </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.label) </li> </ul> |

### Auteur

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> </li> <li> **API-sleutel:**<br/> media.maker </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7. <br/>Beschikbaar in [Overzicht van mediagroep](/help/media-collection-api/mc-api-overview.md) of [SDK&#39;s downloaden - Versies 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Samplewaarde:**<br/> &quot;John Kennedy Toole&quot; </li> <li> **Omschrijving:**<br/> Naam van de auteur (van een audiobook).  <br/> **Releasedatum: 13-09-18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.auteur) </li> <li> **Hartmaten:**<br/> (s:meta:<br/>a.media.auteur) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> </li> <li> **Contextgegevens:**<br/> (a.media.auteur) </li> <li> **Gegevensfeed:**<br/> videoaudiomaker </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.auteur) </li> </ul> |

### Station

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> </li> <li> **API-sleutel:**<br/> media.station </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7. <br/>Beschikbaar in [Overzicht van mediagroep](/help/media-collection-api/mc-api-overview.md) of [SDK&#39;s downloaden - Versies 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Samplewaarde:**<br/> &quot;NPR&quot; </li> <li> **Omschrijving:**<br/> Naam/ID van het radiostation.  <br/> **Releasedatum: 13-09-18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.station) </li> <li> **Hartmaten:**<br/> (s:meta:<br/>a.media.station) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> </li> <li> **Contextgegevens:**<br/> (a.media.station) </li> <li> **Gegevensfeed:**<br/> videoaudiostation </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.station) </li> </ul> |

### Uitgever

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> </li> <li> **API-sleutel:**<br/> media.publisher </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7. <br/>Beschikbaar in [Overzicht van mediagroep](/help/media-collection-api/mc-api-overview.md) of [SDK&#39;s downloaden - Versies 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Samplewaarde:**<br/> &quot;Random Bauhaus&quot; </li> <li> **Omschrijving:**<br/> Naam van de uitgever van de audio-inhoud.  <br/> **Releasedatum: 13-09-18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.publisher) </li> <li> **Hartmaten:**<br/> (s:meta:<br/>a.media.uitgever) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Op HIT </li> <li> **Rapportnaam:**<br/> </li> <li> **Contextgegevens:**<br/> (a.media.publisher) </li> <li> **Gegevensfeed:**<br/> videoluisteraar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.uitgever) </li> </ul> |

## Metrische gegevens van stemmedia {#audio-and-video-metrics}

### Start media

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen</li> <li> **API-sleutel:**<br/> N.v.t.</li> <li> **Type:**<br/> string</li> <li> **Verzonden met:**<br/> Start media</li> <li> **Min. SDK-versie:** Alle</li> <li> **Samplewaarde:**<br/> TRUE </li> <li> **Omschrijving:**<br/> Load-gebeurtenis voor het medium. (Dit gebeurt wanneer de viewer op de knop _Afspelen_ ). Dit zou tellen zelfs als er pre-roladvertenties, het bufferen, fouten, etc. zijn.  <br/>**Belangrijk:**  Dit kan alleen waar zijn als het is ingesteld. Als deze niet is ingesteld, wordt geen waarde geretourneerd.  <br/> **Releasedatum: 13-09-18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.view) </li> <li> **Hartmaten:**<br/> (s:event:<br/>type=start) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Start media </li> <li> **Contextgegevens:**<br/> (a.media.view) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.view) </li> </ul> |

### Inhoud start

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> TRUE </li> <li> **Omschrijving:**<br/> Het eerste frame met media wordt gebruikt. Als de gebruiker tijdens de advertentie valt, buffert, enz., is er geen gebeurtenis &quot;Inhoud starten&quot;.  <br/> **Belangrijk:** Dit kan alleen waar zijn als het is ingesteld. Als deze niet is ingesteld, wordt geen waarde geretourneerd.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> N.v.t. </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Inhoud start </li> <li> **Contextgegevens:**<br/> (a.media.play) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.play) </li> </ul> |

### Inhoud voltooid {#content-complete}

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> TRUE </li> <li> **Omschrijving:**<br/> Een stream die werd gecontroleerd op voltooiing. Dit betekent niet noodzakelijkerwijs dat de gebruiker naar de gehele stream heeft gekeken of geluisterd; ze hadden kunnen overslaan . Dit betekent alleen dat de gebruiker het einde van de stream heeft bereikt, 100%. <br/>Zie ook [Einde sessie](quality-parameters.md#session-end) <br/> **Belangrijk:** Dit kan alleen waar zijn als het is ingesteld. Als deze niet is ingesteld, wordt geen waarde geretourneerd.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> (s:event:<br/>type=complete) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Inhoud voltooid </li> <li> **Contextgegevens:**<br/> (a.media.complete) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.complete) </li> </ul> |

### Tijd van inhoud besteed

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> 105 </li> <li> **Omschrijving:**<br/> Hiermee wordt de gebeurtenisduur (in seconden) voor alle gebeurtenissen van het type PLAY in de hoofdinhoud samengevat.  De waarde wordt weergegeven in de tijdnotatie (HH:MM:SS) in Analysis Workspace en Reports &amp; Analytics. In de Diervoeders van Gegevens, Data Warehouse, en Rapporterende APIs zullen de waarden in seconden worden getoond.  <br/> **Releasedatum: 13-09-18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> N.v.t. </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Tijd van inhoud besteed </li> <li> **Contextgegevens:**<br/> (a.media.timePlayed) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.timePlayed) </li> </ul> |

### Tijd besteed aan media

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> 120 </li> <li> **Omschrijving:**<br/> De gebeurtenisduur (in seconden) voor alle gebeurtenissen van het type PLAY, zowel hoofd- als advertentie-inhoud.  De waarde wordt weergegeven in de tijdnotatie (HH:MM:SS) in Analysis Workspace en Reports &amp; Analytics. In de Diervoeders van Gegevens, Data Warehouse, en Rapporterende APIs zullen de waarden in seconden worden getoond.  <br/> **Releasedatum: 13-09-18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> N.v.t. </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Tijd besteed aan media </li> <li> **Contextgegevens:**<br/> (a.media.totalTimePlayed) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.totalTimePlayed) </li> </ul> |

### Unieke afgespeelde tijd

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> 94 </li> <li> **Omschrijving:**<br/> De waarde in seconden van de unieke segmenten met inhoud die tijdens een sessie worden afgespeeld. Hiermee sluit u de tijd uit die wordt afgespeeld bij terugzoekscenario&#39;s waarbij een viewer hetzelfde segment van de inhoud meerdere keren bekijkt.  De waarde wordt weergegeven in de tijdnotatie (HH:MM:SS) in Analysis Workspace en Reports &amp; Analytics. In de Diervoeders van Gegevens, Data Warehouse, en Rapporterende APIs zullen de waarden in seconden worden getoond.  <br/> **Releasedatum: 13-09-18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> N.v.t. </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Aangepast </li> <li> **Contextgegevens:**<br/> (a.media.uniqueTimePlayed) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.uniqueTimePlayed) </li> </ul> |

### Voortgangsmarkering van tien %

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> TRUE </li> <li> **Omschrijving:**<br/> De afspeelkop geeft de 10%-markering van de inhoud door op basis van de lengte. De markering wordt slechts eenmaal geteld, zelfs als u achterwaarts zoekt. Als u voorwaarts zoekt, worden markeringen die worden overgeslagen, niet geteld.  <br/> **Belangrijk:** Dit kan alleen waar zijn als het is ingesteld. Als deze niet is ingesteld, wordt geen waarde geretourneerd.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> N.v.t. </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> 10% voortgangsmarkering </li> <li> **Contextgegevens:**<br/> (a.media.progress10) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress10) </li> </ul> |

### 25 % voortgangsmarkering

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> TRUE </li> <li> **Omschrijving:**<br/> De afspeelkop geeft de 25%-markering van de inhoud door op basis van de lengte van de inhoud. Markering telde maar één keer, zelfs als u achterwaarts zoekt. Als u voorwaarts zoekt, worden markeringen die worden overgeslagen, niet geteld.  <br/> **Belangrijk:** Dit kan alleen waar zijn als het is ingesteld. Als deze niet is ingesteld, wordt geen waarde geretourneerd.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> N.v.t. </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Voortgangsmarkering van 25% </li> <li> **Contextgegevens:**<br/> (a.media.progress25) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress25) </li> </ul> |

### Voortgangsmarkering van 50 %

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> TRUE </li> <li> **Omschrijving:**<br/> De afspeelkop geeft de 50%-markering van de inhoud door op basis van de lengte van de inhoud. Markering telde maar één keer, zelfs als u achterwaarts zoekt. Als u voorwaarts zoekt, worden markeringen die worden overgeslagen, niet geteld.  <br/> **Belangrijk:** Dit kan alleen waar zijn als het is ingesteld. Als deze niet is ingesteld, wordt geen waarde geretourneerd.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> N.v.t. </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> 50% voortgangsmarkering </li> <li> **Contextgegevens:**<br/> (a.media.progress50) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress50) </li> </ul> |

### Voortgangsmarkering van 75 %

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> **N.v.t.** </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> TRUE </li> <li> **Omschrijving:**<br/> De afspeelkop geeft de 75%-markering van de inhoud door op basis van de lengte van de inhoud. Markering telde maar één keer, zelfs als u achterwaarts zoekt. Als u voorwaarts zoekt, worden markeringen die worden overgeslagen, niet geteld.  <br/> **Belangrijk:** Dit kan alleen waar zijn als het is ingesteld. Als deze niet is ingesteld, wordt geen waarde geretourneerd.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> N.v.t. </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> 75% voortgangsmarkering </li> <li> **Contextgegevens:**<br/> (a.media.progress75) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress75) </li> </ul> |

### 95 % voortgangsmarkering

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> TRUE </li> <li> **Omschrijving:**<br/> De afspeelkop geeft de 95%-markering van de inhoud door op basis van de lengte van de inhoud. Markering telde maar één keer, zelfs als u achterwaarts zoekt. Als u voorwaarts zoekt, worden markeringen die worden overgeslagen, niet geteld.  <br/> **Belangrijk:** Dit kan alleen waar zijn als het is ingesteld. Als deze niet is ingesteld, wordt geen waarde geretourneerd.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> N.v.t. </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> 95% voortgangsmarkering </li> <li> **Contextgegevens:**<br/> (a.media.progress95) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress95) </li> </ul> |

### Gemiddeld aantal minuten publiek

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> Groter dan of gelijk aan 1 </li> <li> **Omschrijving:**<br/> Gemiddelde metrische waarde voor Minuut publiek wordt berekend als Totale tijd bestede inhoud, voor één specifiek media-item, gedeeld door de lengte voor alle afspeelsessies: <br/><br/> `average_minute_audience = timeSpent / videoLength;` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> N.v.t. </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Gemiddeld aantal minuten publiek </li> <li> **Contextgegevens:**<br/> (a.media.averageMinuteAudience) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.averageMinuteAudience) </li> </ul> |

### Seconden sinds laatste Vraag

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> 600</li> <li> **Omschrijving:**<br/> De seconden sinds laatste vraag metrisch is 0 als de stroom met een volledige gebeurtenis of met een eindgebeurtenis werd gesloten, en is gewoonlijk 600 als het wegens onderbreking werd gesloten. Deze metrisch heeft geen oplossingsvariabele en autoverwerkingsregels, zodat moet u een regel van de douaneverwerking tot stand brengen om het te bewaren.</li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> N.v.t. </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Aangepaste verwerkingsregel gebruiken </li> <li> **Gereserveerde variabele:**<br/> N.v.t. </li> <li> **Rapportnaam:**<br/> N.v.t. </li> <li> **Contextgegevens:**<br/> (a.media.secondsSinceLastCall) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.secondsSinceLastCall) </li> </ul> |

### Federale gegevens

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Type:**<br/> boolean </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> true  </li> <li> **Omschrijving:**<br/> Reeks aan waar wanneer de slag wordt gefedereerd (d.w.z., ontvangen door de klant als deel van een gefedereerd gegevensaandeel, eerder dan hun eigen implementatie). </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> N.v.t. </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Aangepaste verwerkingsregel gebruiken </li> <li> **Gereserveerde variabele:**<br/> N.v.t. </li> <li> **Rapportnaam:**<br/> N.v.t. </li> <li> **Contextgegevens:**<br/> (a.media.federated) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.federated) </li> </ul> |

### Geschatte stromen

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> 1 - gedurende 19 minuten afspelen; <br/>2 - gedurende 31 minuten afspelen; <br/>3 - Voor 78 minuten afspelen. </li> <li> **Omschrijving:**<br/> Het geschatte aantal video- of audiostreams per afzonderlijke inhoud. Deze waarde wordt verhoogd voor elke 30 minuten afspeeltijd (inhoud + advertenties). De klanten moeten hun eigen verwerkingsregels tot stand brengen om de waarde voor rapportering beschikbaar te hebben. <br/><br/>Elke 30 minuten wordt een stream geteld op basis van de `ms_s` (of totalTimePlayed = Video Totale Tijd), gelijkend op: <br/> `estimatedStreams = ` <br/>   `FLOOR(ms_s/1800) + 1` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> N.v.t. </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Aangepaste verwerkingsregel gebruiken </li> <li> **Gereserveerde variabele:**<br/> N.v.t. </li> <li> **Rapportnaam:**<br/> Aangepast </li> <li> **Contextgegevens:**<br/> (a.media.estimatedStreams) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.estimatedStreams) </li> </ul> |

### Gepauzeerde beïnvloede stromen

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** 1.5.6. </li> <li> **Samplewaarde:**<br/> TRUE </li> <li> **Omschrijving:**<br/> Deze waarde is waar of onwaar. Het is waar als een of meer pauzes zijn opgetreden tijdens het afspelen van één media-item.  <br/> **Belangrijk:** Dit kan alleen waar zijn als het is ingesteld. Als deze niet is ingesteld, wordt geen waarde geretourneerd.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> (s:event:<br/>type=pause) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Gepauzeerde beïnvloede stroom </li> <li> **Contextgegevens:**<br/> (a.media.pause) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pause) </li> </ul> |

### Gebeurtenissen pauzeren

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** 1.5.6. </li> <li> **Samplewaarde:**<br/> 2 </li> <li> **Omschrijving:**<br/> Deze metrische waarde wordt berekend als een telling van pauzeperioden die tijdens een playbackzitting voorkwamen.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> (s:event:<br/>type=pause) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Gebeurtenissen pauzeren </li> <li> **Contextgegevens:**<br/> (a.media.pauseCount) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pauseCount) </li> </ul> |

### Totale pauzeduur

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** 1.5.6. </li> <li> **Samplewaarde:**<br/> 190 </li> <li> **Omschrijving:**<br/> Hiermee wordt de duur (in seconden) van alle gebeurtenissen van het type PAUSE samengevat. De waarde wordt weergegeven in de tijdnotatie (HH:MM:SS) in Analysis Workspace en Reports &amp; Analytics. In de Diervoeders van Gegevens, Data Warehouse, en Rapporterende APIs zullen de waarden in seconden worden getoond. <br/> **Releasedatum: 13-09-18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> N.v.t. </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Totale pauzeduur </li> <li> **Contextgegevens:**<br/> (a.media.pauseTime) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pauseTime) </li> </ul> |

### Inhoudsresultaten

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> **media.resume** </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** 1.5.6. </li> <li> **Samplewaarde:**<br/> TRUE </li> <li> **Omschrijving:**<br/> Een hervatten wordt geteld voor elke playback die na meer dan 30 minuten van buffer, pauze, of stallatieperiode OF hervat als deze waarde door de speler op VideoInfo trackPlay wordt geplaatst. <br/> **Belangrijk:** Dit kan alleen waar zijn als het is ingesteld. Als deze niet is ingesteld, wordt geen waarde geretourneerd.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> (s:event:<br/>type=resume) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Inhoudsresultaten </li> <li> **Contextgegevens:**<br/> (a.media.resume) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.resume) </li> </ul> |

### Weergaven van inhoudssegmenten

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> Automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Type:**<br/> string </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> TRUE </li> <li> **Omschrijving:**<br/> Het aantal weergaven van de hoofdinhoud. Een weergave van een inhoudssegment wordt geteld wanneer er ten minste één bekeken frame is.  <br/> **Belangrijk:** Dit kan alleen waar zijn als het is ingesteld. Als deze niet is ingesteld, wordt geen waarde geretourneerd. </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> N.v.t. </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> event </li> <li> **Rapportnaam:**<br/> Weergaven van inhoudssegmenten </li> <li> **Contextgegevens:**<br/> (a.media.segmentView) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.segmentView) </li> </ul> |


### Aantal advertenties

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> N.v.t. </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> 2 </li> <li> **Omschrijving:**<br/> Het aantal advertenties dat tijdens de mediasessie is gestart.   <br/> </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> N.v.t. </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Aangepaste verwerkingsregel gebruiken </li> <li> **Gereserveerde variabele:**<br/> N.v.t. </li> <li> **Rapportnaam:**<br/> Aangepast </li> <li> **Contextgegevens:**<br/> (a.media.adCount) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.adCount) </li> </ul> |

### Hoofdstuk tellen

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> N.v.t. </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Type:**<br/> getal </li> <li> **Verzonden met:**<br/> Media sluiten </li> <li> **Min. SDK-versie:** Alle </li> <li> **Samplewaarde:**<br/> 2 </li> <li> **Omschrijving:**<br/> Het aantal hoofdstukken dat tijdens de mediasessie is gestart.   <br/> </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> N.v.t. </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Aangepaste verwerkingsregel gebruiken </li> <li> **Gereserveerde variabele:**<br/> N.v.t. </li> <li> **Rapportnaam:**<br/> Aangepast </li> <li> **Contextgegevens:**<br/> (a.media.chapterCount) </li> <li> **Gegevensfeed:**<br/> N.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapterCount) </li> </ul> |


## California Consumer Privacy Act (CCPA) Parameters {#ccpa-params}

### Server-side doorsturen uitschakelen

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> N.v.t. </li> <li> **API-sleutel:**<br/> analytics.optOutServerSideForwarding </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> boolean </li> <li> **Verzonden met:**<br/> Start media </li> <li> **Min. SDK-versie:** N.v.t. </li> <li> **Samplewaarde:**<br/> true </li> <li>**Omschrijving:**<br/> Wordt ingesteld op true wanneer de eindgebruiker heeft opgegeven dat geen gegevens meer worden gedeeld tussen Adobe Analytics en andere Experience Cloud-oplossingen (bijvoorbeeld Audience Manager). </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (opt.dmp) </li> <li> **Hartmaten:**<br/> (s:meta:cm.ssf) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Bij BEZOEK </li> <li> **Rapportnaam:**<br/> Inhoud </li> <li> **Contextgegevens:**<br/> N.v.t. </li> <li> **Gegevensfeed:**<br/> video </li> <li> **Audience Manager:**<br/> N.v.t. </li> </ul> |

### Delen uitschakelen

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> N.v.t. </li> <li> **API-sleutel:**<br/> analytics.optOutShare </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> boolean </li> <li> **Verzonden met:**<br/> Start media </li> <li> **Min. SDK-versie:** N.v.t. </li> <li> **Samplewaarde:**<br/> true </li> <li>**Omschrijving:**<br/> Wordt ingesteld op true wanneer de eindgebruiker heeft opgegeven dat zijn gegevens niet meer worden gefedereerd (bijvoorbeeld naar andere Adobe Analytics-clients). </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (opt.oos) </li> <li> **Hartmaten:**<br/> (s:meta:cm.oos) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> Bij BEZOEK </li> <li> **Rapportnaam:**<br/> Inhoud </li> <li> **Contextgegevens:**<br/> N.v.t. </li> <li> **Gegevensfeed:**<br/> video </li> <li> **Audience Manager:**<br/> N.v.t. </li> </ul> |

## Verwante API&#39;s {#section_Related_APIs}

### createMediaObject-API&#39;s {#create-media-object}

* Android - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)
* iOS - [createMediaObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)
* JavaScript - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)
* Chromecast - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

### MediaHeartboneConfig-API&#39;s {#config-media-object}

* Android - [MediaHeartboneConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartboneConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html)
