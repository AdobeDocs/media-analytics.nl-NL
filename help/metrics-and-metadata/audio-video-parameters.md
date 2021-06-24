---
title: Parameters voor audio en video
description: Meer informatie over de variabelen Core Streaming Media Data, waaronder audio- en video-inhoudsgegevens en contextgegevens.
uuid: fdacfb8b-db3e-46fb-b9ad-c3a749555b2a
exl-id: 9dc84377-6eca-482f-89e7-c4008d1c0f07
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '6188'
ht-degree: 2%

---

# Parameters voor audio en video{#audio-and-video-parameters}

Dit onderwerp stelt een lijst van audio en videoinhoudsgegevens, met inbegrip van contextgegevenswaarden voor, die Adobe via oplossingsvariabelen verzamelt.

>[!IMPORTANT]
>
>Op 7 februari 2019 heeft Adobe Analytics for Video en Audio een naamswijziging in metrische vorm uitgebracht. <i>Media-</i> initiatieven worden nu  <i>Media Starts</i> genoemd. Deze wijziging werd aangebracht om de industriestandaarden in metriek en rapportage weer te geven en om de metrische gegevens gemakkelijk te kunnen identificeren in de rapportage.

>[!NOTE]
>
>Vanaf 13 september 2018 is er een wijziging aangebracht in de labels voor bepaalde afmetingen, meetgegevens en rapporten, zodat video- en audioanalyses op verschillende inhoud kunnen worden bijgehouden. De labels die zijn gewijzigd, zijn onder andere: *video initiates* to *media initiates*, *video length* to *content length*, and *video name* to *content name*. De videorapporten in Reports and Analytics zijn allemaal bijgewerkt met de naam &quot;Media&quot; in plaats van &quot;Video&quot;. De veranderingen van het etiket veranderden geen gegevensinzameling of historische gegevens. Houd rekening met deze wijzigingen als u deze gebruikt binnen Report Builder of in andere externe automatische gegevenspullen die mogelijk door deze wijziging worden beïnvloed.

Beschrijving van tabelgegevens:

* **Implementatie:** informatie over implementatiewaarden en -vereisten
   * *Sleutel*  - Variabele, plaats of manueel in uw app, of automatisch door de Adobe Media SDK.
   * *Vereist*  - Geeft aan of de parameter is vereist voor het bijhouden van audio en video.
   * *Type*  - Geeft het type op van de variabele die moet worden ingesteld, de tekenreeks of het getal.
   * *Verzonden met*  - Geeft aan wanneer de gegevens worden verzonden:  *Media* Startis de analytische aanroep die op het begin van de media wordt verzonden,  *Ad* Startis de analytische aanroep die op ad start wordt verzonden, enzovoort; de  ** Closecalls zijn de gecompileerde analytische vraag die rechtstreeks van de hartslagserver naar de analyseserver aan het eind van de media zitting, of het eind van de advertentie, het hoofdstuk, enz. wordt verzonden. De dichte vraag is niet beschikbaar in de vraag van het netwerkpakket.
   * *Min. SDK-versie* - Geeft aan welke SDK-versie u toegang tot de parameter nodig hebt.
   * *Samplewaarde* : geeft een voorbeeld van algemeen variabelengebruik.
* **Netwerkparameters:** geeft de waarden weer die worden doorgegeven aan Adobe Analytics- of Hartslagservers. Deze kolom toont de namen van de parameters die in de netwerkvraag worden gezien die door Adobe Media SDKs wordt geproduceerd.
* **Rapportage:** informatie over het weergeven en analyseren van audio- en videogegevens.
   * *Beschikbaar*  - Geeft aan of de gegevens standaard beschikbaar zijn in rapportage (*Ja*) of dat aangepaste installatie vereist is (*Aangepast*)
   * *Gereserveerde variabele*  - Geeft aan of de gegevens zijn vastgelegd als een gebeurtenis, eVar, eigenschap of classificatie in een gereserveerde variabele.
   * *Vervaldatum*  - Geeft aan of de gegevens verlopen na elke aanraking of na elk bezoek.
   * *Rapportnaam*  - Naam van analyserapport van Adobe voor variabele
   * *Contextgegevens*  - Naam van de Adobe Analytics-contextgegevens die aan de rapportserver worden doorgegeven en in verwerkingsregels worden gebruikt.
   * *Gegevensfeed*  - Kolomnaam voor variabele gevonden in Clickstream- of Live Stream-gegevensfeeds
   * *Audience Manager*  - Naam van dienstreis aangetroffen in Adobe Audience Manager

>[!IMPORTANT]
>
>Wijzig de classificatienamen niet voor onderstaande variabelen die onder Rapportage/Gereserveerde variabele worden beschreven als &quot;classificatie&quot;.\
>De mediaclassificaties worden gedefinieerd wanneer een rapportsuite is ingeschakeld voor het bijhouden van media. Van tijd tot tijd, voegt Adobe nieuwe eigenschappen toe, en, wanneer dit voorkomt, moeten de klanten hun rapportsuites opnieuw toelaten om toegang tot de nieuwe media eigenschappen te krijgen. Tijdens het updateproces bepaalt Adobe of de classificaties worden toegelaten door de namen van de variabelen te controleren. Als een van deze ontbrekende elementen ontbreekt, voegt Adobe de ontbrekende opnieuw toe.

## Core Streaming Media Data {#core-audio-and-video-data}

### Type stream {#stream-type}

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> [mediaType](./audio-video-parameters.md#create-media-object) </li> <li> **API-sleutel:**<br/> media.streamType </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 2.2 <br/><br/>Beschikbaar in [API-overzicht van mediagroep](/help/media-collection-api/mc-api-overview.md) of [SDK&#39;s downloaden - Versies 2.2](/help/sdk-implement/download-sdks.md).  </li>  <li> **Samplewaarde:**<br/> &quot;video&quot; </li> <li> **Beschrijving:**<br/> Identificeert het stroomtype. Geldige waarden zijn &quot;audio&quot;, &quot;video&quot; en &quot; &quot;.  <br/><br/>[Segmenten](/help/metrics-and-metadata/segments.md) rapporteren:  <br/><br/>Type mediastroom: All -  <br/>Segment all media stream data; Regel: Inhoud (ID) bestaat uit  <br/><br/>Mediastroomtype: Audio - Alle audiostreamgegevens  <br/>segmenteren; Regel: Content (ID) exists AND Media Stream Type = audio  <br/><br/>Media Stream Type: &quot;Video&quot; - alle videostreamgegevens  <br/>segmenteren; Regel: Inhoud (ID) bestaat EN Mediastroomtype != audio <br/><br/> **Releasedatum: 13-09-18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.streamType) </li> <li> **Heartbeats:**<br/> (:meta:<br/>sa.media.streamType) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **verlopen:**<br/> op HIT </li> <li> **Rapportnaam:**<br/> stroomtype </li> <li> **Contextgegevens:**<br/> (a.media.streamType) </li> <li> **Gegevensfeed:**<br/> videostreaming </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.streamType) </li> </ul> |

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
| <ul> <li> **SDK-sleutel:**<br/> [mediaId](./audio-video-parameters.md#create-media-object) </li> <li> **API-sleutel:**<br/> media.id </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** Willekeurige </li> <li> **Samplewaarde:**<br/> &quot;4586695ABC&quot; </li> <li>**Beschrijving:**<br/> inhoud-id van de inhoud, die kan worden gebruikt om terug te koppelen naar andere industrie-/CMS-id&#39;s, gelijk aan de laatste waarde van  `s:asset:video_id.` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.name) </li> <li> **hartslagen:**<br/> (:asset:svideo_id) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> BIJ BEZOEK </li> <li> **Rapportnaam:**<br/> inhoud </li> <li> **Contextgegevens:**<br/> (a.media.name) </li> <li> **Gegevensfeed:**<br/> video </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.name) </li> </ul> |

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
| <ul> <li> **SDK-sleutel:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **API-sleutel:**<br/> media.length </li> <li> **Vereist:**<br/> Ja </li> <li> **Tekst:**<br/> nummer </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** Willekeurige </li> <li> **Samplewaarde:**<br/> VOD: 128; Live: 86400; Lineair: 1800. </li><li> **Beschrijving:**<br/> Cliplengte/Runtime - Dit is de maximale lengte (of duur) van de inhoud die wordt verbruikt (in seconden). De waarde is gelijk aan de laatste waarde van `l:asset:length` van gebeurtenissen van het type Main. <br/>Als  `l:asset:length` deze niet is ingesteld,  `l:asset:duration` wordt de laatste waarde van gebruikt. <br/>Bij rapportage is Videolengte de classificatie en Content Length (variabele) is de eVar.   <br/> **Belangrijk:** Deze eigenschap wordt gebruikt om verschillende meetgegevens te berekenen, zoals gegevens over het bijhouden van de voortgang en Gemiddelde Minuut Publiek. Als deze niet is ingesteld of niet groter is dan nul, zijn deze cijfers niet beschikbaar.  Voor Live media met een onbekende duur is de standaardwaarde 86400. <br/>Vóór versie 1.5.1 was dit  `l:asset:duration`; na 1.5.1  `l:asset:length.` <br/> **Releasedatum: 13-09-18** </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.length) </li> <li> **hartslagen:**<br/> (:asset:lengte) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **verlopen:**<br/> op HIT </li> <li> **Rapportnaam:Lengte**<br/> inhoud (variabele) </li> <li> **Contextgegevens:**<br/> (a.media.length) </li> <li> **gegevensfeed:**<br/> videolengte </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.length) </li> </ul> |

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
| <ul> <li> **SDK-sleutel:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **API-sleutel:**<br/> media.length </li> <li> **Vereist:**<br/> Ja </li> <li> **Tekst:**<br/> nummer </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** Willekeurige </li> <li> **Samplewaarde:**<br/> VOD: 128; Live: 86400; Lineair: 1800. </li> <li> **Beschrijving:**<br/> Cliplengte/Runtime - Dit is de maximale lengte (of duur) van de inhoud die wordt verbruikt (in seconden). De waarde is gelijk aan de laatste waarde van `l:asset:length` van gebeurtenissen van het type Main. Als `l:asset:length` niet is ingesteld, wordt de laatste waarde van `l:asset:duration` gebruikt. Bij rapportage is Videolengte de classificatie en Content Length (variabele) is de eVar.  <br/> **Belangrijk:** Deze eigenschap wordt gebruikt om verschillende meetgegevens te berekenen, zoals gegevens over het bijhouden van de voortgang en Gemiddelde Minuut Publiek. Als deze niet is ingesteld of niet groter is dan nul, zijn deze cijfers niet beschikbaar.  Voor Live media met een onbekende duur is de standaardwaarde 86400. Voor versie 1.5.1 was dit `l:asset:duration`; na 1.5.1 is dit `l:asset:length.`<br/> **Releasedatum: 13-09-18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.length) </li> <li> **hartslagen:**<br/> (:asset:lengte) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> classificatie </li> <li> **verlopen:**<br/> op HIT </li> <li> **Rapportnaam:**<br/> videolengte </li> <li> **Contextgegevens:**<br/> (a.media.length) </li> <li> **gegevensfeed:**<br/> video.video.classificationlength </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.length) </li> </ul> |

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
| <ul> <li> **SDK-sleutel:**<br/>  [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **API-sleutel:**<br/> media.contentType </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> beperkte tekenreeks </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** Willekeurige </li> <li> **Samplewaarde:**<br/> &quot;vod&quot; </li> <li> **Beschrijving:**<br/> Beschikbare waarden per  **stroomtype**:  <br/> _Audio:_ &quot;song&quot;, &quot;podcast&quot;, &quot;audiobook&quot;, &quot;radio&quot;  <br/> _Video:_ &quot;VoD&quot;, &quot;Live&quot;, &quot;Lineair&quot;, &quot;UGC&quot;, &quot;DVoD&quot;  <br/> Klanten kunnen aangepaste waarden voor deze parameter opgeven. Dit is gelijk aan `s:stream:type.` Als dat niet is ingesteld, is dit gelijk aan `missing_content_type.` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.contentType) </li> <li> **Heartbeats:**<br/> (:stream:stype) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **verlopen:**<br/> op HIT </li> <li> **rapportnaam:**<br/> inhoudstype </li> <li> **Contextgegevens:**<br/> (a.contentType) </li> <li> **Gegevensfeed:**<br/> videocontenttype </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.contentType) </li> </ul> |

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
| <ul> <li> **SDK-sleutel:**<br/> automatisch instellen </li> <li> **API-sleutel:**<br/> verkregen van backend </li> <li> **Vereist:**<br/> Ja </li> <li> **Tekst:**<br/> nummer </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.8 </li> <li> **Samplewaarde:**<br/> 1482236761294786918253 </li> <li> **Beschrijving:**<br/> Dit identificeert een instantie van een inhoudsstroom die uniek is voor een individuele playback.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.vsid) </li> <li> **hartslag:**<br/> (:event:ssid) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> verwerkingsregel gebruiken </li> <li> **Gereserveerde variabele:**<br/> n.v.t. </li> <li> **Rapportnaam:**<br/> Aangepast </li> <li> **Contextgegevens:**<br/> (a.media.vsid) </li> <li> **gegevensfeed:**<br/> videosessionid </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.vsid) </li> </ul> |

### Markering voor gedownloade media

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> `config.downloadedcontent` </li> <li> **API-sleutel:**<br/> verkregen van backend </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> boolean </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** <br/>Android- en iOS-extensie v1.1.0 starten </li> <li> **Samplewaarde:**<br/> true </li> <li> **Beschrijving:**<br/> Instellen op true wanneer de hit wordt gegenereerd vanwege het afspelen van een gedownloade mediasessie voor inhoud. Niet aanwezig wanneer gedownloade inhoud niet wordt afgespeeld.<br/><br/>[Starten](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#create-a-media-tracker-with-optional-configuration)  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.downloaded) </li> <li> **Hartslag:**<br/> (:meta:sa.media.downloaded) </li> </ul> | <ul> <li> **Beschikbaar:aangepaste verwerkingsregel**<br/> gebruiken </li> <li> **Gereserveerde variabele:**<br/> n.v.t. </li> <li> **Rapportnaam:**<br/> Aangepast </li> <li> **Contextgegevens:**<br/> (a.media.downloaded) </li> <li> **Gegevensfeed:**<br/> n.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.downloaded) </li> </ul> |

### Naam van inhoudspeler

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> [playerName](./audio-video-parameters.md#config-media-object) </li> <li> **API-sleutel:**<br/> media.playerName </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** Willekeurige </li> <li> **Samplewaarde:**<br/> &quot;Brightcove&quot; </li> <li> **Beschrijving:**<br/> Naam van de speler.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>playerName) </li> <li> **hartslagen:**<br/> (:sp:splayer_name) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **verlopen:**<br/> op HIT </li> <li> **Rapportnaam:naam**<br/> van inhoudspeler </li> <li> **Contextgegevens:**<br/> (a.media.playerName) </li> <li> **gegevensfeed:**<br/> videoplayername </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.playerName) </li> </ul> |

### Inhoudskanaal

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>  [channel](./audio-video-parameters.md#config-media-object) </li> <li> **API-sleutel:**<br/> media.channel </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** Willekeurige </li> <li> **Samplewaarde:**<br/> &quot;Sport&quot; </li> <li> **Omschrijving:**<br/> Distributiestation/Kanalen of waar de inhoud wordt afgespeeld. Elke tekenreekswaarde wordt hier geaccepteerd.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.channel) </li> <li> **hartslagen:**<br/> (:sp:schannel) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **verlopen:**<br/> op HIT </li> <li> **Rapportnaam:**<br/> Inhoud kanaal </li> <li> **Contextgegevens:**<br/> (a.media.channel) </li> <li> **Gegevensfeed:**<br/> videokanaal </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.channel) </li> </ul> |

### Segment Inhoud

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Ja </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media Sluiten </li> <li> **Min. SDK-versie:** Willekeurige </li> <li> **Samplewaarde:**<br/> &quot;0-10&quot; </li> <li> **Beschrijving:**<br/> het interval dat het gedeelte van de inhoud beschrijft dat is weergegeven (in minuten). Het segment wordt berekend als min en max van de waarden van de afspeelkop tijdens een afspeelsessie.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> n.v.t. </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **verlopen:**<br/> op HIT </li> <li> **rapportnaam:**<br/> inhoudssegment </li> <li> **Contextgegevens:**<br/> (a.media.segment) </li> <li> **gegevensfeed:**<br/> video </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.segment) </li> </ul> |

### Inhoudsnaam (variabele)

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>  [name](./audio-video-parameters.md#create-media-object) </li> <li> **API-sleutel:**<br/> media.name </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.1 </li> <li> **Samplewaarde:**<br/> &quot;The Big Bang Theory&quot; </li> <li> **Beschrijving:**<br/> Dit is de &quot;vriendelijke&quot; (leesbare) naam van de inhoud, gelijk aan de laatste waarde van  `s:asset:name.`<br/>In rapportage, is de Videenaam de classificatie, en de Naam van de inhoud (variabele) is de eVar.  <br/> **Releasedatum: 13-09-18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>vriendelijkeName) </li> <li> **hartslagen:**<br/> (:asset:naam) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **verlopen:**<br/> op HIT </li> <li> **Rapportnaam:naam**<br/> inhoud (variabele) </li> <li> **Contextgegevens:**<br/> (a.media.vriendelijkeName) </li> <li> **gegevensfeed:**<br/> videonaam </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.vriendelijkeName) </li> </ul> |

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
| <ul> <li> **SDK-sleutel:**<br/>  [name](./audio-video-parameters.md#config-media-object) </li> <li> **API-sleutel:**<br/> media.name </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.1 </li> <li> **Samplewaarde:**<br/> &quot;The Big Bang Theory&quot; </li> <li> **Beschrijving:**<br/> Dit is de &quot;vriendelijke&quot; (leesbare) naam van de inhoud, gelijk aan de laatste waarde van  `s:asset:name.` <br/>In rapportage, is de Videenaam de classificatie, en de Naam van de inhoud (variabele) is de eVar.   <br/> **Releasedatum: 13-09-18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>vriendelijkeName) </li> <li> **hartslagen:**<br/> (:asset:naam) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> classificatie </li> <li> **verlopen:**<br/> op HIT </li> <li> **Rapportnaam:**<br/> videonaam </li> <li> **Contextgegevens:**<br/> (a.media.vriendelijkeName) </li> <li> **Gegevensfeed:**<br/> video.video.classificationname </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.vriendelijkeName) </li> </ul> |

### Videopad

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:Start**<br/> media </li> <li> **Min. SDK-versie:** Willekeurige </li> <li> **Samplewaarde:**<br/> &quot;4586695ABC&quot; </li> <li> **Beschrijving:**<br/> biedt de mogelijkheid om het pad van een viewer voor een site en/of een app bij te houden om het pad te zien dat deze hebben ingenomen om een bepaalde video te bekijken. Een geheel getal en/of lettercombinatie.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.name) </li> <li> **hartslagen:**<br/> (:asset:svideo_id) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> prop </li> <li> **Rapportnaam:**<br/> Videopad </li> <li> **Contextgegevens:**<br/> (a.media.name) </li> <li> **gegevensfeed:**<br/> videopath </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.name) </li> </ul> |

### SDK-versie

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/>  [appVersion](./audio-video-parameters.md#config-media-object) </li> <li> **API-sleutel:**<br/> media.sdkVersion </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media Sluiten </li> <li> **Min. SDK-versie:** 1.5.7 </li> <li> **Samplewaarde:**<br/> &quot;2.62.0_release&quot; </li> <li> **Beschrijving:**<br/> De SDK-versie die door de speler wordt gebruikt. Dit kan elke aangepaste waarde hebben die voor uw speler zinnig is. <br/><br/>Klanten moeten hun eigen verwerkingsregels maken om de waarde voor rapportage beschikbaar te hebben.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>sdkVersion) </li> <li> **hartslagen:**<br/> (:sp:ssdk) </li> </ul> | <ul> <li> **Beschikbaar:aangepaste verwerkingsregel**<br/> gebruiken </li> <li> **Gereserveerde variabele:**<br/> n.v.t. </li> <li> **Rapportnaam:**<br/> Aangepast </li> <li> **Contextgegevens:**<br/> (a.media.sdkVersion) </li> <li> **Gegevensfeed:**<br/> n.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.sdkVersion) </li> </ul> |

### VHL-versie

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media Sluiten </li> <li> **Min. SDK-versie:** 1.5.7 </li> <li> **Samplewaarde:**<br/> &quot;js-2.0.1.88-c8c0b1&quot; </li> <li> **Beschrijving:**<br/> De SDK-versie van Media die wordt gebruikt voor de volgende sessie. <br/><br/>Klanten moeten hun eigen verwerkingsregels maken om de waarde voor rapportage beschikbaar te hebben.  <br/><br/>[MediaHeartbone.version();](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html) </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>vhlVersion) </li> <li> **hartslagen:**<br/> (:sp:shb_version) </li> </ul> | <ul> <li> **Beschikbaar:aangepaste verwerkingsregel**<br/> gebruiken </li> <li> **Gereserveerde variabele:**<br/> n.v.t. </li> <li> **Rapportnaam:**<br/> Aangepast </li> <li> **Contextgegevens:**<br/> (a.media.vhlVersion) </li> <li> **Gegevensfeed:**<br/> n.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.vhlVersion) </li> </ul> |

## Standaardstreamingmediametagegevens {#standard-audio-and-video-metadata}

### Tonen

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> TONEN </li> <li> **API-sleutel:**<br/> media.show </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7 </li> <li> **Samplewaarde:**<br/> &quot;Modern Family&quot; &quot;The Last Dance&quot; &quot;New Girl&quot; </li> <li> **Beschrijving:De Naam van**<br/> het Programma van het Programma van de Naam van  <br/>Programma/van de Reeks wordt vereist slechts als de show deel van een reeks uitmaakt.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.show) </li> <li> **Hartmaten:**<br/> (:meta:<br/>sa.media.show) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **verlopen:**<br/> op HIT </li> <li> **Rapportnaam:**<br/> weergeven </li> <li> **Contextgegevens:**<br/> (a.media.show) </li> <li> **Gegevensfeed:**<br/> videoshow </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.show) </li> </ul> |

### Stroomindeling

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> STREAM_FORMAT </li> <li> **API-sleutel:**<br/> media.streamFormat </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7 </li> <li> **Samplewaarde:**<br/> &quot;HD&quot; </li> <li> **Beschrijving:**<br/> Indeling van de stream (HD, SD)  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.format) </li> <li> **Hartmaten:**<br/> (:meta:<br/>sa.media.format) </li> </ul> | <ul> <li> **Beschikbaar:aangepaste verwerkingsregel**<br/> gebruiken </li> <li> **Gereserveerde variabele:**<br/> n.v.t. </li> <li> **Rapportnaam:**<br/> Aangepast </li> <li> **Contextgegevens:**<br/> (a.media.format) </li> <li> **Gegevensfeed:**<br/> n.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.format) </li> </ul> |

### Seizoen

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> SEASON </li> <li> **API-sleutel:**<br/> media.seizoen </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7 </li> <li> **Samplewaarde:**<br/> &quot;2&quot; </li> <li> **Beschrijving:**<br/> Het seizoensnummer waartoe de show behoort.  Reeks seizoen is alleen vereist als de presentatie deel uitmaakt van een reeks.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.seizoen) </li> <li> **Hartmaten:**<br/> (:meta:<br/>sa.media.seizoen) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **verlopen:**<br/> op HIT </li> <li> **Rapportnaam:**<br/> seizoen </li> <li> **Contextgegevens:**<br/> (a.media.seizoen) </li> <li> **Gegevensfeed:**<br/> videoseizoen </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.seizoen) </li> </ul> |

### Episode

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> EPISODE </li> <li> **API-sleutel:**<br/> media.episode </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7 </li> <li> **Samplewaarde:**<br/> &quot;13&quot; </li> <li> **Omschrijving:**<br/> het nummer van de aflevering.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.episode) </li> <li> **Heartbeats:**<br/> (:meta:<br/>sa.media.episode) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **verlopen:**<br/> op HIT </li> <li> **Rapportnaam:**<br/> Aflevering </li> <li> **Contextgegevens:**<br/> (a.media.episode) </li> <li> **Gegevensfeed:**<br/> video-episode </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.episode) </li> </ul> |

### Element-id

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> ASSET_ID </li> <li> **API-sleutel:**<br/> media.assetId </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7 </li> <li> **Samplewaarde:**<br/> &quot;89745363&quot; </li> <li> **Beschrijving:**<br/> Dit is de unieke id voor de inhoud van het media-element, zoals de aflevering-id van de tv-reeks, de id van het filmelement of de livegebeurtenis. Deze id&#39;s zijn doorgaans afgeleid van metagegevensautoriteiten zoals EIDR, TMS/Gracenote of Rovi. Deze id&#39;s kunnen ook afkomstig zijn van andere bedrijfseigen of interne systemen.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.asset) </li> <li> **Hartmaten:**<br/> (:meta:<br/>sa.media.asset) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> classificatie </li> <li> **Rapportnaam:**<br/> Element-id </li> <li> **Contextgegevens:**<br/> (a.media.asset) </li> <li> **gegevensfeed:**<br/> video.video.classificationassetid </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.asset) </li> </ul> |

### Genre

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> GENRE </li> <li> **API-sleutel:**<br/> media.genre </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7 </li> <li> **Samplewaarde:**<br/> &quot;Drama&quot;, &quot;Comedy&quot; </li> <li> **Omschrijving:**<br/> Soort of groepering van inhoud zoals gedefinieerd door inhoudsproducent. Waarden moeten worden gescheiden door komma&#39;s in een variabele implementatie. Bij het rapporteren wordt elke waarde in een regelitem opgedeeld door de eVar van de lijst, waarbij elk regelitem een gelijk metrisch gewicht krijgt.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.genre) </li> <li> **Heartbeats:**<br/> (:meta:<br/>sa.media.genre) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> List, eVar </li> <li> **verlopen:**<br/> op HIT </li> <li> **Rapportnaam:**<br/> Genre </li> <li> **Contextgegevens:**<br/> (a.media.genre) </li> <li> **Gegevensfeed:**<br/> videogene </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.genre) </li> </ul> |

### Eerste luchtdatum

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> FIRST_AIR_DATE </li> <li> **API-sleutel:**<br/> media.firstAirDate </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:Start**<br/> media </li> <li> **Min. SDK-versie:** 1.5.7 </li> <li> **Samplewaarde:**<br/> &quot;2016-01-25&quot; </li> <li> **Omschrijving:**<br/> de datum waarop de inhoud voor het eerst op televisie werd uitgezonden. Elke datumnotatie is acceptabel, maar Adobe raadt aan: YYYY-MM-DD </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.airDate) </li> <li> **Heartbeats:**<br/> (:meta:<br/>sa.media.airDate) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> classificatie </li> <li> **verlopen:**<br/> op HIT </li> <li> **Rapportnaam:**<br/> eerste luchtdatum </li> <li> **Contextgegevens:**<br/> (a.media.airDate) </li> <li> **Gegevensfeed:**<br/> video.video.classificationairdate </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.airDate) </li> </ul> |

### Eerste digitale datum

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> FIRST_DIGITAL_DATE </li> <li> **API-sleutel:**<br/> media.firstDigitalDate </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7 </li> <li> **Samplewaarde:**<br/> &quot;2016-01-25&quot; </li> <li> **Beschrijving:**<br/> De datum waarop de inhoud voor het eerst via een digitaal kanaal of platform is verzonden. Elke datumnotatie is acceptabel, maar Adobe raadt aan: YYYY-MM-DD </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.digitalDate) </li> <li> **Hartmaten:**<br/> (:meta:<br/>sa.media.digitalDate) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> classificatie </li> <li> **Rapportnaam:**<br/> eerste digitale datum </li> <li> **Contextgegevens:**<br/> (a.media.digitalDate) </li> <li> **gegevensfeed:**<br/> video.video.classificationdigitaldate </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.digitalDate) </li> </ul> |

### Classificatie van inhoud

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> CLASSIFICATIE </li> <li> **API-sleutel:**<br/> media.rating </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7 </li> <li> **Samplewaarde:**<br/> TVY, TVG, TVPG, TVMA </li> <li> **Omschrijving:**<br/> Classificatie zoals gedefinieerd in de Ouderlijke Richtlijnen voor TV.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.rating) </li> <li> **Hartmaten:**<br/> (:meta:<br/>sa.media.rating) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> classificatie </li> <li> **Rapportnaam:**<br/> Inhoudsbeoordeling </li> <li> **Contextgegevens:**<br/> (a.media.rating) </li> <li> **Gegevensfeed:**<br/> video.video.classificationrating </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.rating) </li> </ul> |

### Maker

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> ORIGINATOR </li> <li> **API-sleutel:**<br/> media.originator </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7 </li> <li> **Samplewaarde:**<br/> &quot;Warner Brothers&quot;, &quot;Sony&quot;, &quot;Disney&quot; </li> <li> **Omschrijving:**<br/> Maker van de inhoud.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.originator) </li> <li> **Hartmaten:**<br/> (:meta:<br/>sa.media.originator) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> classificatie </li> <li> **Rapportnaam:**<br/> maker </li> <li> **Contextgegevens:**<br/> (a.media.originator) </li> <li> **Gegevensfeed:**<br/> video.video.video-classificationoriginator </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.originator) </li> </ul> |

### Netwerk

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> NETWERK </li> <li> **API-sleutel:**<br/> media.network </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7 </li> <li> **Samplewaarde:**<br/> &quot;Fox&quot;, &quot;Bravo&quot;, &quot;ESPN&quot; </li> <li> **Beschrijving:**<br/> de netwerk-/kanaalnaam.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.network) </li> <li> **Hartmaten:**<br/> (:meta:<br/>sa.media.network) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **verlopen:**<br/> op HIT </li> <li> **Rapportnaam:**<br/> Netwerk </li> <li> **Contextgegevens:**<br/> (a.media.network) </li> <li> **gegevensfeed:**<br/> videonetwork </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.network) </li> </ul> |

### Tekst tonen

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> SHOW_TYPE </li> <li> **API-sleutel:**<br/> media.showType </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7 </li> <li> **Monsterwaarde:**<br/> &quot;0&quot; = volledige aflevering; &quot;1&quot; = Voorbeeld/aanhangwagen; &quot;2&quot; = Clip; &quot;3&quot; = Overige. </li> <li> **Beschrijving:**<br/> Soort inhoud, uitgedrukt als een geheel getal tussen 0 en 3.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.type) </li> <li> **Hartmaten:**<br/> (:meta:<br/>sa.media.type) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **verlopen:**<br/> op HIT </li> <li> **Rapportnaam:Type**<br/> tonen </li> <li> **Contextgegevens:**<br/> (a.media.type) </li> <li> **Gegevensfeed:**<br/> videoshowtype </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.type) </li> </ul> |

### MVPD

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> MVPD </li> <li> **API-sleutel:**<br/> media.pass.mvpd </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7 </li> <li> **Samplewaarde:**<br/> &quot;Comcast&quot;, &quot;DirecTV&quot;, &quot;Dish&quot; </li> <li> **Omschrijving:**<br/> MVPD verstrekt via de authentificatie van de Adobe.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.pass.mvpd) </li> <li> **Hartmaten:**<br/> (:meta:<br/>sa.media.pass.<br/>mvpd) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **verlopen:**<br/> op HIT </li> <li> **Rapportnaam:**<br/> MVPD </li> <li> **Contextgegevens:**<br/> (a.media.pass.mvpd) </li> <li> **gegevensfeed:**<br/> videomvpd </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pass.mvpd) </li> </ul> |

### Geautoriseerd

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> GEMACHTIGD </li> <li> **API-sleutel:**<br/> media.pass.auth </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7 </li> <li> **Samplewaarde:**<br/> &quot;TRUE&quot; </li> <li> **Beschrijving:**<br/> De gebruiker is geautoriseerd via Adobe-verificatie.  <br/>**Belangrijk:** dit kan alleen waar zijn als het is ingesteld. Als deze niet is ingesteld, wordt geen waarde geretourneerd.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.pass.auth) </li> <li> **Hartmaten:**<br/> (:meta:<br/>sa.media.pass.<br/>auth) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> gebeurtenis </li> <li> **rapportnaam:**<br/> geautoriseerd </li> <li> **Contextgegevens:**<br/> (a.media.pass.auth) </li> <li> **Gegevensfeed:**<br/> videogeautoriseerde </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pass.auth) </li> </ul> |

### Dagdeel

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> DAY_PART </li> <li> **API-sleutel:**<br/> media.dayPart </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7 </li> <li> **Samplewaarde:**<br/> </li> <li> **Beschrijving:**<br/> Een eigenschap die de tijd definieert van de dag waarop de inhoud werd uitgezonden of afgespeeld. Dit zou om het even welke waarde kunnen hebben die zonodig door klanten wordt geplaatst.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.dayPart) </li> <li> **Hartmaten:**<br/> (:meta:<br/>sa.media.dayPart) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **verlopen:**<br/> op HIT </li> <li> **Rapportnaam:**<br/> Dagdeel </li> <li> **Contextgegevens:**<br/> (a.media.dayPart) </li> <li> **Gegevensfeed:**<br/> videodaypart </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.dayPart) </li> </ul> |

### Type mediafeed

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> FEED </li> <li> **API-sleutel:**<br/> media.feed </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7 </li> <li> **Samplewaarde:**<br/> &quot;East-HD&quot;, &quot;West-HD&quot;, &quot;East-SD&quot; </li> <li> **Omschrijving:**<br/> Soort diervoeder.   <br/> **Releasedatum: 13-09-18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.feed) </li> <li> **Hartmaten:**<br/> (:meta:<br/>sa.media.feed) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **verlopen:**<br/> op HIT </li> <li> **Rapportnaam:**<br/> Diertype voor media </li> <li> **Contextgegevens:**<br/> (a.media.feed) </li> <li> **Gegevensfeed:**<br/> videofeedtype </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.feed) </li> </ul> |

### Artiest

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> </li> <li> **API-sleutel:**<br/> media.artist </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7 <br/>Beschikbaar in [Overzicht van mediagroep](/help/media-collection-api/mc-api-overview.md) of [SDK&#39;s downloaden - Versies 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Samplewaarde:**<br/> &quot;The Beatles&quot; </li> <li> **Omschrijving:**<br/> Naam van de artiest.   <br/> **Releasedatum: 13-09-18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.artist) </li> <li> **Heartbeats:**<br/> (:meta:<br/>sa.media.artist) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **verlopen:**<br/> op HIT </li> <li> **Rapportnaam:**<br/> Artiest</li> <li> **Contextgegevens:**<br/> (a.media.artist) </li> <li> **Gegevensfeed:**<br/> videoaudioartiest </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.artiest) </li> </ul> |

### Album

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> </li> <li> **API-sleutel:**<br/> media.album </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7 <br/>Beschikbaar in [Overzicht van mediagroep](/help/media-collection-api/mc-api-overview.md) of [SDK&#39;s downloaden - Versies 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Samplewaarde:**<br/> &quot;Revolver&quot; </li> <li> **Beschrijving:**<br/> Naam van het album.   <br/> **Releasedatum: 13-09-18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.album) </li> <li> **Hartmaten:**<br/> (:meta:<br/>sa.media.album) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **verlopen:**<br/> op HIT </li> <li> **Rapportnaam:**<br/> Album </li> <li> **Contextgegevens:**<br/> (a.media.album) </li> <li> **Gegevensfeed:**<br/> videoaudioalbum </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.album) </li> </ul> |

### Label

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> </li> <li> **API-sleutel:**<br/> media.label </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7 <br/>Beschikbaar in [Overzicht van mediagroep](/help/media-collection-api/mc-api-overview.md) of [SDK&#39;s downloaden - Versies 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Samplewaarde:**<br/> &quot;Revolver&quot; </li> <li> **Beschrijving:**<br/> Naam van het recordlabel.   <br/> **Releasedatum: 13-09-18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.label) </li> <li> **Hartmaten:**<br/> (:meta:<br/>sa.media.label) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **verlopen:**<br/> op HIT </li> <li> **Rapportnaam:**<br/> Label</li> <li> **Contextgegevens:**<br/> (a.media.label) </li> <li> **Gegevensfeed:**<br/> videoaudiolabel </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.label) </li> </ul> |

### Auteur

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> </li> <li> **API-sleutel:**<br/> media.auteur </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7 <br/>Beschikbaar in [Overzicht van mediagroep](/help/media-collection-api/mc-api-overview.md) of [SDK&#39;s downloaden - Versies 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Samplewaarde:**<br/> &quot;John Kennedy Toole&quot; </li> <li> **Beschrijving:**<br/> Naam van de auteur (van een audiobook).   <br/> **Releasedatum: 13-09-18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.auteur) </li> <li> **Hartmaten:**<br/> (:meta:<br/>sa.media.auteur) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **verlopen:**<br/> op HIT </li> <li> **Rapportnaam:**<br/> auteur </li> <li> **Contextgegevens:**<br/> (a.media.auteur) </li> <li> **Gegevensfeed:**<br/> video-auteur </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.auteur) </li> </ul> |

### Station

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> </li> <li> **API-sleutel:**<br/> media.station </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7 <br/>Beschikbaar in [Overzicht van mediagroep](/help/media-collection-api/mc-api-overview.md) of [SDK&#39;s downloaden - Versies 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Samplewaarde:**<br/> &quot;NPR&quot; </li> <li> **Beschrijving:**<br/> Naam/ID van het radiostation.   <br/> **Releasedatum: 13-09-18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.station) </li> <li> **Heartbeats:**<br/> (:meta:<br/>sa.media.station) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **verlopen:**<br/> op HIT </li> <li> **Rapportnaam:**<br/> station </li> <li> **Contextgegevens:**<br/> (a.media.station) </li> <li> **Gegevensfeed:**<br/> videoaudiostation </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.station) </li> </ul> |

### Uitgever

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> </li> <li> **API-sleutel:**<br/> media.publisher </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media starten, Media sluiten </li> <li> **Min. SDK-versie:** 1.5.7 <br/>Beschikbaar in [Overzicht van mediagroep](/help/media-collection-api/mc-api-overview.md) of [SDK&#39;s downloaden - Versies 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Samplewaarde:**<br/> &quot;Random Bauhaus&quot; </li> <li> **Beschrijving:**<br/> Naam van de uitgever van de audio-inhoud.   <br/> **Releasedatum: 13-09-18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.publisher) </li> <li> **Hartmaten:**<br/> (:meta:<br/>sa.media.publisher) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **verlopen:**<br/> op HIT </li> <li> **Rapportnaam:**<br/> Aangepast </li> <li> **Contextgegevens:**<br/> (a.media.publisher) </li> <li> **Gegevensfeed:**<br/> videoaudiopublisher </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.uitgever) </li>  </ul> |

## Streaming media Metrics {#audio-and-video-metrics}

### Start media

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> automatisch instellen</li> <li> **API-sleutel:**<br/> N.v.t.</li> <li> **Type:**<br/> tekenreeks</li> <li> **Verzonden met:Start**<br/> media</li> <li> **Min. SDK-versie:** Willekeurige</li> <li> **Samplewaarde:**<br/> TRUE </li> <li> **Beschrijving:gebeurtenis**<br/> Laden voor de media. (Dit komt voor wanneer de kijker _Spel_ knoop) klikt. Dit zou tellen zelfs als er pre-roladvertenties, het bufferen, fouten, etc. zijn.  <br/>**Belangrijk:**  dit kan alleen waar zijn als het is ingesteld. Als deze niet is ingesteld, wordt geen waarde geretourneerd.  <br/> **Releasedatum: 13-09-18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.view) </li> <li> **Heartbeats:**<br/> (:event:<br/>stype=start) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> gebeurtenis </li> <li> **Rapportnaam:**<br/> Media starten </li> <li> **Contextgegevens:**<br/> (a.media.view) </li> <li> **Gegevensfeed:**<br/> videostart </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.view) </li> </ul> |

### Inhoud start

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media Sluiten </li> <li> **Min. SDK-versie:** Willekeurige </li> <li> **Samplewaarde:**<br/> TRUE </li> <li> **Beschrijving: het**<br/> eerste frame met media wordt gebruikt. Als de gebruiker tijdens de advertentie valt, buffert, enz., is er geen gebeurtenis &quot;Inhoud starten&quot;.  <br/> **Belangrijk:** dit kan alleen waar zijn als het is ingesteld. Als deze niet is ingesteld, wordt geen waarde geretourneerd.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> n.v.t. </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> gebeurtenis </li> <li> **Rapportnaam:**<br/> Inhoud starten </li> <li> **Contextgegevens:**<br/> (a.media.play) </li> <li> **gegevensfeed:**<br/> videoplay </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.play) </li> </ul> |

### Inhoud voltooid {#content-complete}

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media Sluiten </li> <li> **Min. SDK-versie:** Willekeurige </li> <li> **Samplewaarde:**<br/> TRUE </li> <li> **Beschrijving:**<br/> Een stroom die naar voltooiing is gecontroleerd. Dit betekent niet noodzakelijkerwijs dat de gebruiker naar de gehele stream heeft gekeken of geluisterd; ze hadden kunnen overslaan . Dit betekent alleen dat de gebruiker het einde van de stream heeft bereikt, 100%. <br/>Zie ook Einde  [sessie](quality-parameters.md#session-end) <br/> **Belangrijk:** dit kan alleen waar zijn als het is ingesteld. Als deze niet is ingesteld, wordt geen waarde geretourneerd.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Heartbeats:**<br/> (:event:<br/>stype=complete) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> gebeurtenis </li> <li> **rapportnaam:**<br/> Inhoud invullen </li> <li> **Contextgegevens:**<br/> (a.media.complete) </li> <li> **Gegevensfeed:**<br/> video voltooid   </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.complete) </li> </ul> |

### Tijd van inhoud besteed

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Tekst:**<br/> nummer </li> <li> **Verzonden met:**<br/> Media Sluiten </li> <li> **Min. SDK-versie:** Willekeurige </li> <li> **Samplewaarde:**<br/> 105 </li> <li> **Beschrijving:**<br/> vat de gebeurtenisduur (in seconden) voor alle gebeurtenissen van het type PLAY op de belangrijkste inhoud samen.  De waarde zal in het tijdformaat (HH:MM:SS) in Analysis Workspace en Rapporten &amp; Analytics worden getoond. In de Diervoeders van Gegevens, Data Warehouse, en Rapporterende APIs zullen de waarden in seconden worden getoond.  <br/> **Releasedatum: 13-09-18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> n.v.t. </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> gebeurtenis </li> <li> **Rapportnaam:**<br/> Inhoudstijd </li> <li> **Contextgegevens:**<br/> (a.media.timePlayed) </li> <li> **Gegevensfeed:**<br/> videotijd </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.timePlayed) </li> </ul> |

### Tijd besteed aan media

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Tekst:**<br/> nummer </li> <li> **Verzonden met:**<br/> Media Sluiten </li> <li> **Min. SDK-versie:** Willekeurige </li> <li> **Samplewaarde:**<br/> 120 </li> <li> **Beschrijving:**<br/> geeft een overzicht van de gebeurtenisduur (in seconden) voor alle gebeurtenissen van het type PLAY, zowel hoofd- als advertentie-inhoud.  De waarde zal in het tijdformaat (HH:MM:SS) in Analysis Workspace en Rapporten &amp; Analytics worden getoond. In de Diervoeders van Gegevens, Data Warehouse, en Rapporterende APIs zullen de waarden in seconden worden getoond.  <br/> **Releasedatum: 13-09-18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> n.v.t. </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> gebeurtenis </li> <li> **Rapportnaam:**<br/> mediatijd besteed </li> <li> **Contextgegevens:**<br/> (a.media.totalTimePlayed) </li> <li> **Gegevensfeed:**<br/> videototaltime </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.totalTimePlayed) </li> </ul> |

### Unieke afgespeelde tijd

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Tekst:**<br/> nummer </li> <li> **Verzonden met:**<br/> Media Sluiten </li> <li> **Min. SDK-versie:** Willekeurige </li> <li> **Samplewaarde:**<br/> 94 </li> <li> **Beschrijving:**<br/> De waarde in seconden van de unieke segmenten met inhoud die tijdens een sessie worden afgespeeld. Hiermee sluit u de tijd uit die wordt afgespeeld bij terugzoekscenario&#39;s waarbij een viewer hetzelfde segment van de inhoud meerdere keren bekijkt.  De waarde zal in het tijdformaat (HH:MM:SS) in Analysis Workspace en Rapporten &amp; Analytics worden getoond. In de Diervoeders van Gegevens, Data Warehouse, en Rapporterende APIs zullen de waarden in seconden worden getoond.  <br/> **Releasedatum: 13-09-18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> n.v.t. </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> gebeurtenis </li> <li> **Rapportnaam:**<br/> unieke afspeeltijd </li> <li> **Contextgegevens:**<br/> (a.media.uniqueTimePlayed) </li> <li> **gegevensfeed:**<br/> videouniquetimeplay </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.uniqueTimePlayed) </li> </ul> |

### Voortgangsmarkering van tien %

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media Sluiten </li> <li> **Min. SDK-versie:** Willekeurige </li> <li> **Samplewaarde:**<br/> TRUE </li> <li> **Beschrijving:**<br/> afspeelkop geeft de 10%-markering van inhoud door op basis van lengte. De markering wordt slechts eenmaal geteld, zelfs als u achterwaarts zoekt. Als u voorwaarts zoekt, worden markeringen die worden overgeslagen, niet geteld.  <br/> **Belangrijk:** dit kan alleen waar zijn als het is ingesteld. Als deze niet is ingesteld, wordt geen waarde geretourneerd.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> n.v.t. </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> gebeurtenis </li> <li> **Rapportnaam:**<br/> 10% voortgangsmarkering </li> <li> **Contextgegevens:**<br/> (a.media.progress10) </li> <li> **Gegevensfeed:**<br/> videoprogress10 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress10) </li> </ul> |

### 25 % voortgangsmarkering

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media Sluiten </li> <li> **Min. SDK-versie:** Willekeurige </li> <li> **Samplewaarde:**<br/> TRUE </li> <li> **Beschrijving:**<br/> afspeelkop geeft de 25%-markering van inhoud door op basis van de lengte van de inhoud. Markering telde maar één keer, zelfs als u achterwaarts zoekt. Als u voorwaarts zoekt, worden markeringen die worden overgeslagen, niet geteld.  <br/> **Belangrijk:** dit kan alleen waar zijn als het is ingesteld. Als deze niet is ingesteld, wordt geen waarde geretourneerd.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> n.v.t. </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> gebeurtenis </li> <li> **Rapportnaam:**<br/> 25% voortgangsmarkering </li> <li> **Contextgegevens:**<br/> (a.media.progress25) </li> <li> **Gegevensfeed:**<br/> videoprogress25 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress25) </li> </ul> |

### Voortgangsmarkering van 50 %

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media Sluiten </li> <li> **Min. SDK-versie:** Willekeurige </li> <li> **Samplewaarde:**<br/> TRUE </li> <li> **Beschrijving:**<br/> afspeelkop geeft de 50%-markering van inhoud door op basis van de lengte van de inhoud. Markering telde maar één keer, zelfs als u achterwaarts zoekt. Als u voorwaarts zoekt, worden markeringen die worden overgeslagen, niet geteld.  <br/> **Belangrijk:** dit kan alleen waar zijn als het is ingesteld. Als deze niet is ingesteld, wordt geen waarde geretourneerd.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> n.v.t. </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> gebeurtenis </li> <li> **Rapportnaam:**<br/> 50% voortgangsmarkering </li> <li> **Contextgegevens:**<br/> (a.media.progress50) </li> <li> **Gegevensfeed:**<br/> videoprogress50 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress50) </li> </ul> |

### Voortgangsmarkering van 75 %

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> automatisch instellen </li> <li> **API-sleutel:**<br/> **N.v.t.** </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media Sluiten </li> <li> **Min. SDK-versie:** Willekeurige </li> <li> **Samplewaarde:**<br/> TRUE </li> <li> **Beschrijving:**<br/> afspeelkop geeft 75%-markering voor inhoud door op basis van de lengte van de inhoud. Markering telde maar één keer, zelfs als u achterwaarts zoekt. Als u voorwaarts zoekt, worden markeringen die worden overgeslagen, niet geteld.  <br/> **Belangrijk:** dit kan alleen waar zijn als het is ingesteld. Als deze niet is ingesteld, wordt geen waarde geretourneerd.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> n.v.t. </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> gebeurtenis </li> <li> **Rapportnaam:**<br/> 75% voortgangsmarkering </li> <li> **Contextgegevens:**<br/> (a.media.progress75) </li> <li> **Gegevensfeed:**<br/> videoprogress75 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress75) </li> </ul> |

### 95 % voortgangsmarkering

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media Sluiten </li> <li> **Min. SDK-versie:** Willekeurige </li> <li> **Samplewaarde:**<br/> TRUE </li> <li> **Beschrijving:**<br/> afspeelkop geeft de 95%-markering van inhoud door op basis van de lengte van de inhoud. Markering telde maar één keer, zelfs als u achterwaarts zoekt. Als u voorwaarts zoekt, worden markeringen die worden overgeslagen, niet geteld.  <br/> **Belangrijk:** dit kan alleen waar zijn als het is ingesteld. Als deze niet is ingesteld, wordt geen waarde geretourneerd.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> n.v.t. </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> gebeurtenis </li> <li> **Rapportnaam:**<br/> 95% voortgangsmarkering </li> <li> **Contextgegevens:**<br/> (a.media.progress95) </li> <li> **Gegevensfeed:**<br/> videoprogress95 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress95) </li> </ul> |

### Gemiddeld aantal minuten publiek

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Tekst:**<br/> nummer </li> <li> **Verzonden met:**<br/> Media Sluiten </li> <li> **Min. SDK-versie:** Willekeurige </li> <li> **Samplewaarde:**<br/> groter dan of gelijk aan 1 </li> <li> **Beschrijving:De metrische waarde**<br/> Gemiddelde minuten publiek wordt berekend als Totale tijd van de Inhoud, voor één specifiek media-item, gedeeld door de lengte voor alle afspeelsessies:  <br/><br/> `average_minute_audience = timeSpent / videoLength;` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> n.v.t. </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> gebeurtenis </li> <li> **Rapportnaam:**<br/> gemiddeld aantal minuten publiek </li> <li> **Contextgegevens:**<br/> (a.media.averageMinuteAudience) </li> <li> **Gegevensfeed:**<br/> videoaverageminutepubliek </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.averageMinuteAudience) </li> </ul> |

### Seconden sinds laatste Vraag

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Tekst:**<br/> nummer </li> <li> **Verzonden met:**<br/> Media Sluiten </li> <li> **Min. SDK-versie:** Willekeurige </li> <li> **Samplewaarde:**<br/> 600</li> <li> **Beschrijving:**<br/> De seconden sinds laatste vraag metrisch is 0 als de stroom met een volledige gebeurtenis of met een eindgebeurtenis werd gesloten, en is gewoonlijk 600 als het wegens onderbreking werd gesloten. Deze metrisch heeft geen oplossingsvariabele en autoverwerkingsregels, zodat moet u een regel van de douaneverwerking tot stand brengen om het te bewaren.</li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> n.v.t. </li> </ul> | <ul> <li> **Beschikbaar:aangepaste verwerkingsregel**<br/> gebruiken </li> <li> **Gereserveerde variabele:**<br/> n.v.t. </li> <li> **Rapportnaam:**<br/> Aangepast</li> <li> **Contextgegevens:**<br/> (a.media.secondsSinceLastCall) </li> <li> **Gegevensfeed:**<br/> videoseconsincelastcall </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.secondsSinceLastCall) </li> </ul> |

### Federale gegevens

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Type:**<br/> boolean </li> <li> **Verzonden met:**<br/> Media Sluiten </li> <li> **Min. SDK-versie:** Willekeurige </li> <li> **Samplewaarde:**<br/> true  </li> <li> **Beschrijving:**<br/> Ingesteld op waar wanneer de hit wordt gefedereerd (d.w.z. ontvangen door de klant als onderdeel van een gefederaliseerde gegevensuitwisseling, in plaats van hun eigen implementatie). </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> n.v.t. </li> </ul> | <ul> <li> **Beschikbaar:aangepaste verwerkingsregel**<br/> gebruiken </li> <li> **Gereserveerde variabele:**<br/> n.v.t. </li> <li> **Rapportnaam:**<br/> n.v.t. </li> <li> **Contextgegevens:**<br/> (a.media.federated) </li> <li> **Gegevensfeed:**<br/> n.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.federated) </li> </ul> |

### Geschatte stromen

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Tekst:**<br/> nummer </li> <li> **Verzonden met:**<br/> Media Sluiten </li> <li> **Min. SDK-versie:** Willekeurige </li> <li> **Samplewaarde:**<br/> 1 - Voor een afspelen van 19 minuten;  <br/>2 - gedurende 31 minuten afspelen;  <br/>3 - Voor 78 minuten afspelen. </li> <li> **Beschrijving:**<br/> Het geschatte aantal video- of audiostreams per afzonderlijke inhoud. Deze waarde wordt verhoogd voor elke 30 minuten afspeeltijd (inhoud + advertenties). De klanten moeten hun eigen verwerkingsregels tot stand brengen om de waarde voor rapportering beschikbaar te hebben. <br/><br/>Een stream wordt elke 30 minuten geteld, op basis van de  `ms_s` (of totalTimePlayed = Video Total Time), ongeveer als volgt:  <br/> `estimatedStreams = ` <br/>   `FLOOR(ms_s/1800) + 1` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> n.v.t. </li> </ul> | <ul> <li> **Beschikbaar:aangepaste verwerkingsregel**<br/> gebruiken </li> <li> **Gereserveerde variabele:**<br/> n.v.t. </li> <li> **Rapportnaam:**<br/> Aangepast </li> <li> **Contextgegevens:**<br/> (a.media.estimatedStreams) </li> <li> **Gegevensfeed:**<br/> n.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.estimatedStreams) </li> </ul> |

### Gepauzeerde beïnvloede stromen

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media Sluiten </li> <li> **Min. SDK-versie:** 1.5.6 </li> <li> **Samplewaarde:**<br/> TRUE </li> <li> **Beschrijving:**<br/> Deze waarde is waar of onwaar. Het is waar als een of meer pauzes zijn opgetreden tijdens het afspelen van één media-item.  <br/> **Belangrijk:** dit kan alleen waar zijn als het is ingesteld. Als deze niet is ingesteld, wordt geen waarde geretourneerd.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Heartbeats:**<br/> (:event:<br/>stype=pause) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> gebeurtenis </li> <li> **Rapportnaam:**<br/> Gepauzeerde beïnvloed stroom </li> <li> **Contextgegevens:**<br/> (a.media.pause) </li> <li> **gegevensfeed:**<br/> videopauze </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pause) </li> </ul> |

### Gebeurtenissen pauzeren

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Tekst:**<br/> nummer </li> <li> **Verzonden met:**<br/> Media Sluiten </li> <li> **Min. SDK-versie:** 1.5.6 </li> <li> **Samplewaarde:**<br/> 2 </li> <li> **Beschrijving:**<br/> Deze metrische waarde wordt berekend als een telling van pauzeperioden die tijdens een playbackzitting voorkwamen.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Heartbeats:**<br/> (:event:<br/>stype=pause) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> gebeurtenis </li> <li> **rapportnaam:gebeurtenissen**<br/> pauzeren </li> <li> **Contextgegevens:**<br/> (a.media.pauseCount) </li> <li> **gegevensfeed:**<br/> videopausecount </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pauseCount) </li> </ul> |

### Totale pauzeduur

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Tekst:**<br/> nummer </li> <li> **Verzonden met:**<br/> Media Sluiten </li> <li> **Min. SDK-versie:** 1.5.6 </li> <li> **Samplewaarde:**<br/> 190 </li> <li> **Beschrijving:**<br/> geeft een overzicht van de duur (in seconden) van alle gebeurtenissen van het type PAUSE. De waarde zal in het tijdformaat (HH:MM:SS) in Analysis Workspace en Rapporten &amp; Analytics worden getoond. In de Diervoeders van Gegevens, Data Warehouse, en Rapporterende APIs zullen de waarden in seconden worden getoond. <br/> **Releasedatum: 13-09-18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> n.v.t. </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> gebeurtenis </li> <li> **Rapportnaam:**<br/> Totale pauzeduur </li> <li> **Contextgegevens:**<br/> (a.media.pauseTime) </li> <li> **Gegevensfeed:**<br/> (videoTime) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pauseTime) </li> </ul> |

### Inhoudsresultaten

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> automatisch instellen </li> <li> **API-sleutel:**<br/> **media.resume** </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media Sluiten </li> <li> **Min. SDK-versie:** 1.5.6 </li> <li> **Samplewaarde:**<br/> TRUE </li> <li> **Beschrijving:**<br/> Een hervatten wordt geteld voor elke playback die na meer dan 30 minuten van buffer, pauze, of stallperiode OF hervat als deze waarde door de speler op VideoInfo trackPlay wordt geplaatst.  <br/> **Belangrijk:** dit kan alleen waar zijn als het is ingesteld. Als deze niet is ingesteld, wordt geen waarde geretourneerd.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Heartbeats:**<br/> (:event:<br/>stype=resume) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> gebeurtenis </li> <li> **Rapportnaam:**<br/> Inhoudsresultaten </li> <li> **Contextgegevens:**<br/> (a.media.resume) </li> <li> **Gegevensfeed:**<br/> videoresume </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.resume) </li> </ul> |

### Weergaven van inhoudssegmenten

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> automatisch instellen </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Type:**<br/> tekenreeks </li> <li> **Verzonden met:**<br/> Media Sluiten </li> <li> **Min. SDK-versie:** Willekeurige </li> <li> **Samplewaarde:**<br/> TRUE </li> <li> **Beschrijving:**<br/> Het aantal weergaven van de hoofdinhoud. Een weergave van een inhoudssegment wordt geteld wanneer er ten minste één bekeken frame is.  <br/> **Belangrijk:** dit kan alleen waar zijn als het is ingesteld. Als deze niet is ingesteld, wordt geen waarde geretourneerd. </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> n.v.t. </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> gebeurtenis </li> <li> **rapportnaam:**<br/> inhoudssegmentweergaven </li> <li> **Contextgegevens:**<br/> (a.media.segmentView) </li> <li> **gegevensfeed:**<br/> videocodeteweergaven </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.segmentView) </li> </ul> |


### Aantal advertenties

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> N.v.t. </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Tekst:**<br/> nummer </li> <li> **Verzonden met:**<br/> Media Sluiten </li> <li> **Min. SDK-versie:** Willekeurige </li> <li> **Samplewaarde:**<br/> 2 </li> <li> **Beschrijving:**<br/> het aantal advertenties dat tijdens de mediasessie is gestart.    <br/> </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> n.v.t. </li> </ul> | <ul> <li> **Beschikbaar:aangepaste verwerkingsregel**<br/> gebruiken </li> <li> **Gereserveerde variabele:**<br/> n.v.t. </li> <li> **Rapportnaam:**<br/> Aangepast </li> <li> **Contextgegevens:**<br/> (a.media.adCount) </li> <li> **Gegevensfeed:**<br/> n.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.adCount) </li> </ul> |

### Hoofdstuk tellen

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> N.v.t. </li> <li> **API-sleutel:**<br/> N.v.t. </li> <li> **Tekst:**<br/> nummer </li> <li> **Verzonden met:**<br/> Media Sluiten </li> <li> **Min. SDK-versie:** Willekeurige </li> <li> **Samplewaarde:**<br/> 2 </li> <li> **Beschrijving:**<br/> het aantal hoofdstukken dat tijdens de mediasessie is gestart.    <br/> </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N.v.t. </li> <li> **Hartmaten:**<br/> n.v.t. </li> </ul> | <ul> <li> **Beschikbaar:aangepaste verwerkingsregel**<br/> gebruiken </li> <li> **Gereserveerde variabele:**<br/> n.v.t. </li> <li> **Rapportnaam:**<br/> Aangepast </li> <li> **Contextgegevens:**<br/> (a.media.chapterCount) </li> <li> **Gegevensfeed:**<br/> n.v.t. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapterCount) </li> </ul> |


## California Consumer Privacy Act (CCPA) Parameters {#ccpa-params}

### Server-side doorsturen uitschakelen

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> N.v.t. </li> <li> **API-sleutel:**<br/> analytics.optOutServerSideForwarding </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> boolean </li> <li> **Verzonden met:Start**<br/> media </li> <li> **Min. SDK-versie:** n.v.t. </li> <li> **Samplewaarde:**<br/> true </li> <li>**Beschrijving:**<br/> Instellen op true wanneer de eindgebruiker heeft besloten geen gegevens meer te delen tussen Adobe Analytics en andere Experience Cloud-oplossingen (bijvoorbeeld Audience Manager). </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (opt.dmp) </li> <li> **Hartmaten:**<br/> (:meta:scm.ssf) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> BIJ BEZOEK </li> <li> **Rapportnaam:**<br/> n.v.t. </li> <li> **contextgegevens:**<br/> n.v.t. </li> <li> **Gegevensfeed:**<br/> n.v.t. </li> <li> **Audience Manager:**<br/> N.v.t. </li> </ul> |

### Delen uitschakelen

|   Implementatie   | Netwerkparameters | Rapportage |
| --- | --- | --- |
| <ul> <li> **SDK-sleutel:**<br/> N.v.t. </li> <li> **API-sleutel:**<br/> analytics.optOutShare </li> <li> **Vereist:**<br/> Nee </li> <li> **Type:**<br/> boolean </li> <li> **Verzonden met:Start**<br/> media </li> <li> **Min. SDK-versie:** n.v.t. </li> <li> **Samplewaarde:**<br/> true </li> <li>**Beschrijving:**<br/> Instellen op true wanneer de eindgebruiker heeft opgegeven dat zijn gegevens niet zijn gefedereerd (bijvoorbeeld naar andere Adobe Analytics-clients). </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (opt.oos) </li> <li> **hartslagen:**<br/> (:meta:scm.oos) </li> </ul> | <ul> <li> **Beschikbaar:**<br/> Ja </li> <li> **Gereserveerde variabele:**<br/> eVar </li> <li> **Verlopen:**<br/> BIJ BEZOEK </li> <li> **Rapportnaam:**<br/> n.v.t. </li> <li> **contextgegevens:**<br/> n.v.t. </li> <li> **Gegevensfeed:**<br/> n.v.t. </li> <li> **Audience Manager:**<br/> N.v.t. </li> </ul> |

## Verwante API&#39;s {#section_Related_APIs}

### createMediaObject-API&#39;s {#create-media-object}

* Android - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)
* iOS - [createMediaObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)
* JavaScript - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)
* Chromecast - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

### MediaHeartboneConfig-API&#39;s {#config-media-object}

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartboneConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html)
