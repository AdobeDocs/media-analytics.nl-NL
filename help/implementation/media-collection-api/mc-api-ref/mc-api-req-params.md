---
title: API voor streaming Media Services � aanvraagparameters
description: Wat zijn de de verzoekparameters van de Inzameling van Media, verzoeksleutels, en beschrijvingen.
uuid: f83e9ef1-803d-4152-a6c7-acaa325036b9
exl-id: a70025ec-1418-46f1-b41f-433d09f024e1
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 4%

---

# Parameters aanvragen{#request-parameters}

## Analysegegevens

| Aanvraagsleutel  | Vereist | Sleutel aanvraagtype | Instellen op... |  Beschrijving  |
| --- | :---: | :---: | :---: | --- |
| `analytics.trackingServer` | Y | string | `sessionStart` | De URL van uw Adobe Analytics-server |
| `analytics.reportSuite` | Y | string | `sessionStart` | De id die uw analysegegevens identificeert |
| `analytics.enableSSL` | N | boolean | `sessionStart` | Waar of onwaar voor het inschakelen van SSL |
| `analytics.visitorId` | N | string | `sessionStart` | De Adobe-bezoeker-id is een aangepaste id die u kunt gebruiken in meerdere Adobe-toepassingen. De hartslag `visitorId` is gelijk aan de analyse `VID.` |

## Bezoekersgegevens

| Aanvraagsleutel  | Vereist | Sleutel aanvraagtype | Instellen op... |  Beschrijving  |
| --- | :---: | :---: | :---: | --- |
| `visitor.marketingCloudOrgId` | Y | string | `sessionStart` | De Experience Cloud-organisatie-id; identificeert uw organisatie binnen het Adobe Experience Cloud-ecosysteem |
| `visitor.marketingCloudUserId` | N | string | `sessionStart` | Dit is de Experience Cloud-gebruikersnaam (ECID). In de meeste gevallen is dit de id die u moet gebruiken om een gebruiker te identificeren. De hartslag `marketingCloudUserId` is gelijk aan de `MID` in Adobe Analytics. Hoewel deze parameter technisch niet vereist is, is deze nodig voor toegang tot de Experience Cloud-reeks met apps. |
| `visitor.aamLocationHint` | N | integer | `sessionStart` | Biedt Adobe Audience Manager Edge-gegevens: als geen waarde wordt ingevoerd, is de waarde null. |
| `appInstallationId` | N | string | `sessionStart` | De appInstallationId identificeert de app en het apparaat op unieke wijze |

## Inhoudsgegevens

| Aanvraagsleutel  | Vereist | Sleutel aanvraagtype | Instellen op... |  Beschrijving  |
| --- | :---: | :---: | :---: | --- |
| `media.id` | Y | string | `sessionStart` | Unieke id voor de inhoud |
| `media.name` | N | string | `sessionStart` | Menselijke leesbare naam voor de inhoud |
| `media.length` | Y | getal | `sessionStart` | Lengte van inhoud (seconden) |
| `media.contentType` | Y | string | `sessionStart` | Indeling van de stream (kan elke tekenreeks zijn, een aantal aanbevolen waarden zijn &quot;Live&quot;, &quot;VOD&quot; of &quot;Lineair&quot;) |
| `media.playerName` | Y | string | `sessionStart` | De naam van de speler die verantwoordelijk is voor het renderen van de inhoud |
| `media.channel` | Y | string | `sessionStart` | Het distributiekanaal van de inhoud. Dit kan een mobiele toepassingsnaam of een websitenaam, eigenschapsnaam zijn |
| `media.resume` | N | boolean | `sessionStart` | Geeft aan of een gebruiker een vorige sessie hervat (in tegenstelling tot het starten van een nieuwe sessie) |
| `media.sdkVersion` | N | string | `sessionStart` | De SDK-versie die door de speler wordt gebruikt |

## Metagegevens inhoudstandaard

| Aanvraagsleutel  | Vereist | Sleutel aanvraagtype | Instellen op... |  Beschrijving  |
| --- | :---: | :---: | :---: | --- |
| `media.streamFormat` | N | string | `sessionStart` | Stream-indeling, bijvoorbeeld &quot;HD&quot; |
| `media.show` | N | string | `sessionStart` | De naam van het programma of de serie |
| `media.season` | N | string | `sessionStart` | Het seizoensnummer waartoe de show of serie behoort |
| `media.episode` | N | string | `sessionStart` | Het nummer van de episode |
| `media.assetId` | N | string | `sessionStart` | De unieke id voor de inhoud van het video-element, zoals de aflevering-id van de tv-reeks, de id van het filmelement of de livegebeurtenis. Deze id&#39;s zijn doorgaans afgeleid van metagegevensautoriteiten zoals EIDR, TMS/Gracenote of Rovi. Deze id&#39;s kunnen ook afkomstig zijn van andere bedrijfseigen of interne systemen. |
| `media.genre` | N | string | `sessionStart` | Het type inhoud zoals gedefinieerd door de inhoudproducent |
| `media.firstAirDate` | N | string | `sessionStart` | De datum waarop de inhoud voor het eerst op televisie werd uitgezonden |
| `media.firstDigitalDate` | N | string | `sessionStart` | De datum waarop de inhoud voor het eerst is verzonden op een digitaal platform |
| `media.rating` | N | string | `sessionStart` | De rating zoals gedefinieerd in de TV Parental Guidelines |
| `media.originator` | N | string | `sessionStart` | De maker van de inhoud |
| `media.network` | N | string | `sessionStart` | De naam van het netwerk/kanaal |
| `media.showType` | N | string | `sessionStart` | Het type inhoud, uitgedrukt als een geheel getal tussen 0 en 3: <ul> <li>0 - Volledige aflevering </li> <li>1 - Voorvertoning </li> <li>2 - Clip </li> <li>3 - Overige </li> </ul> |
| `media.adLoad` | N | string | `sessionStart` | Het type geladen advertentie |
| `media.pass.mvpd` | N | string | `sessionStart` | MVPD geleverd door Adobe-verificatie |
| `media.pass.auth` | N | string | `sessionStart` | Geeft aan dat de gebruiker is geautoriseerd door Adobe-verificatie (kan alleen waar zijn als deze is ingesteld) |
| `media.dayPart` | N | string | `sessionStart` | De tijd van de dag waarop de inhoud werd uitgezonden |
| `media.feed` | N | string | `sessionStart` | Het type diervoeder, bijvoorbeeld &quot;West-HD&quot; |

## Advertentiegegevens

| Aanvraagsleutel  | Vereist | Sleutel aanvraagtype | Instellen op... |  Beschrijving  |
| --- | :---: | :---: | :---: | --- |
| `media.ad.podFriendlyName` | N | string | `adBreakStart` | Vriendschappelijke naam van het advertentiepad |
| `media.ad.podIndex` | Y | integer | `adBreakStart` | De index van de advertentiepod in de video |
| `media.ad.podSecond` | Y | getal | `adBreakStart` | De tweede waarmee de pod is gestart |
| `media.ad.podPosition` | Y | integer | `adStart` | De index van de advertentie binnen het advertentiespoor dat bij 1 begint |
| `media.ad.name` | N | string | `adStart` | Vriendelijke naam van de advertentie |
| `media.ad.id` | Y | string | `adStart` | Naam van de advertentie |
| `media.ad.length` | Y | getal | `adStart` | Lengte van de video en in seconden |
| `media.ad.playerName` | Y | string | `adStart` | De naam van de speler die verantwoordelijk is voor het renderen van de advertentie |

## Standaardmetagegevens toevoegen

| Aanvraagsleutel  | Vereist | Sleutel aanvraagtype | Instellen op... |  Beschrijving  |
| --- | :---: | :---: | :---: | --- |
| `media.ad.advertiser` | N | string | `adStart` | De onderneming of het merk waarvan het product in de advertentie voorkomt |
| `media.ad.campaignId` | N | string | `adStart` | De id van de advertentiecampagne |
| `media.ad.creativeId` | N | string | `adStart` | De id van de advertentie is creatief |
| `media.ad.siteId` | N | string | `adStart` | De id van de advertentiesite |
| `media.ad.creativeURL` | N | string | `adStart` | De URL van de advertentie |
| `media.ad.placementId` | N | string | `adStart` | De plaatsings-id van de advertentie |

## Hoofdgegevens

| Aanvraagsleutel  | Vereist | Sleutel aanvraagtype | Instellen op... |  Beschrijving  |
| --- | :---: | :---: | :---: | --- |
| `media.chapter.index` | Y | integer | `chapterStart` | Hiermee wordt de positie van het hoofdstuk in de inhoud aangegeven |
| `media.chapter.offset` | Y | getal | `chapterStart` | De tweede functie in het afspelen waar het hoofdstuk begint |
| `media.chapter.length` | Y | getal | `chapterStart` | De lengte van het hoofdstuk in seconden |
| `media.chapter.friendlyName` | N | string | `chapterStart` | De mensvriendelijke naam van het hoofdstuk |

## Kwaliteitsgegevens

| Aanvraagsleutel  | Vereist | Sleutel aanvraagtype | Instellen op... |  Beschrijving  |
| --- | :---: | :---: | :---: | --- |
| `media.qoe.bitrate` | N | integer | Alle | De gemiddelde bitsnelheid (in bps). De gemiddelde bitsnelheid wordt berekend als het gewogen gemiddelde van alle bitsnelheidwaarden die betrekking hebben op de afspeelduur die tijdens een afspeelsessie is opgetreden. |
| `media.qoe.droppedFrames` | N | integer | Alle | Het aantal gedropte frames in de stream |
| `media.qoe.framesPerSecond` | N | integer | Alle | Het aantal frames per seconde |
| `media.qoe.timeToStart` | N | integer | Alle | De hoeveelheid tijd (in milliseconden) die wordt doorgegeven tussen het moment dat de gebruiker in aanraking komt met afspelen en het moment waarop de inhoud wordt geladen en het moment waarop wordt begonnen met afspelen |

## California Consumer Privacy Act (CCPA) Parameters {#ccpa-params}

| Aanvraagsleutel  | Vereist | Sleutel aanvraagtype | Instellen op... |  Beschrijving  |
| --- | :---: | :---: | :---: | --- |
| `analytics.optOutServerSideForwarding` | N | boolean | `sessionStart` | Ingesteld op true wanneer de eindgebruiker ervoor heeft gekozen geen gegevens meer te delen tussen Adobe Analytics en andere Experience Cloud-oplossingen (bijvoorbeeld Audience Manager) |
| `analytics.optOutShare` | N | boolean | `sessionStart` | Wordt ingesteld op true wanneer de eindgebruiker heeft opgegeven dat zijn gegevens niet meer worden gefedereerd (bijvoorbeeld aan andere Adobe Analytics-clients). |

## Aanvullende details {#additional-details}

### visitor.marketingCloudUserId

Geef de Experience Cloud Gebruiker - identiteitskaart (ook genoemd geworden `MID` of `MCID`) op de `sessionStart` vraag door het binnen de `params` kaart te omvatten gebruikend de volgende sleutel: **bezoekor.marketingCloudUserId**. Dit is een handige functie als u al met andere Experience Cloud-producten hebt geïntegreerd en de MCID al hebt verkregen.

>[!NOTE]
>
>Media Analytics (MA) is geïntegreerd met de Experience Cloud-serie apps (Adobe Analytics, Audience Manager, Target, enzovoort). U hebt een Experience Cloud-id nodig om deze apps te openen. _ECID is wat u zou moeten gebruiken om gebruikers in de meeste scenario&#39;s te identificeren._

### appInstallationId

* **als u *niet* een `appInstallationId` waarde -** het achterste eind van MA niet meer MCID zal produceren, maar in plaats daarvan op Adobe Analytics zal vertrouwen om dit te doen. De aanbeveling van Adobe is om een MCID te verzenden als deze beschikbaar is, of een `appInstallationId` (samen met de nog steeds verplichte `marketingCloudOrgId` ), zodat de Media Collection-API de MCID genereert en deze op alle aanroepen verzendt.

* **als u &#x200B;** `appInstallationId` waarde **&#x200B; overgaat MCID &#x200B;** kan worden geproduceerd door het achterste eind van MA, als u waarden voor `appInstallationId` en (vereiste) `marketingCloudOrgId` parameters overgaat. Als u `appInstallationId` zelf doorgeeft, moet u de waarde ervan aan de clientzijde behouden. De toepassing moet uniek zijn voor de toepassing op een apparaat en moet blijvend zijn zolang de toepassing niet opnieuw wordt geïnstalleerd.

>[!NOTE]
>
>`appInstallationId` identificeert uniek app *en het apparaat*. De klasse moet uniek zijn voor elke toepassing op elk apparaat, d.w.z. twee gebruikers die dezelfde versie van dezelfde app op verschillende apparaten gebruiken, moeten elk een andere (unieke) `appInstallationId` verzenden.

<!-- Initially, there were no browser-based customers. In future this will be part of a two-bullet list, one bullet for Native Apps, the other for Browser apps. The .
\<ul id="ul_iwc_fqt_pbb"\>
 \<li\>For Browser Apps, this should be a first-party cookie that is persistent for as long as the user stays in the same browser. If clients have multiple websites, they need to have different cookies for each site.</li>
</ul> -->

### visitor.marketingCloudOrgId

Naast noodzakelijk voor generatie MCID wanneer dat niet wordt verstrekt, wordt deze parameter ook gebruikt als waarde voor uitgevers identiteitskaart (die op wordt gebaseerd die de Analyse van Media [&#x200B; aanpassing van de federatieregel uitvoert.](/help/use-cases/federated-media.md))

### Verouderde gebruikersnaam (hulp) en gedeclareerde gebruikers-id&#39;s (CustomerID&#39;s) voor analyse

* **analytics.aid:**

  De waarde van deze sleutel moet een tekenreeks zijn die de oude gebruikers-id voor Analytics vertegenwoordigt
* **bezoeker.customerIDs:**

  De waarde van deze sleutel moet een voorwerp van het volgende formaat zijn:

  ```js
  "<<insert your ID name here>>": {  
    "id": " <<insert your id here>>",  
     "authState": <<insert one of 0, 1, 2>>
  }
  ```

De waarde `visitor.customerIDs` kan een willekeurig aantal objecten in de weergegeven indeling hebben.

### visitor.aamLocationHint

Deze parameter geeft aan welke Adobe Audience Manager (AAM) Edge wordt getroffen wanneer Adobe Analytics de klantgegevens naar Audience Manager verzendt. Wanneer geen waarde wordt ingevoerd, is de waarde null. Dit is met name van belang wanneer eindgebruikers hun apparaten doorgaans gebruiken op geografisch afgelegen locaties (bijvoorbeeld VS-Oost, VS-West, Europa, Azië). Anders worden gebruikersgegevens verspreid over meerdere AAM-randen.

### media.resume

Als app bepaalt dat een zitting werd gesloten en dan op een recentere tijd hervat, b.v., verliet de gebruiker de video maar kwam uiteindelijk terug, en de speler hervat de video van playhead waar het werd tegengehouden, kunt u een facultatieve booleaanse **media.resume** parameter binnen het paramentenemmer van de `sessionStart` vraag verzenden.

<!--
| `media.uniqueTimePlayed` | N | Close | The value in seconds of the unique segments of content played during a session. Excludes time played on seek back scenarios in which a viewer is watching the same segment of the content multiple times.  |
-->
