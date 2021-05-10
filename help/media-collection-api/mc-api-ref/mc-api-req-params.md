---
title: Parameters aanvragen
description: null
uuid: f83e9ef1-803d-4152-a6c7-acaa325036b9
exl-id: a70025ec-1418-46f1-b41f-433d09f024e1
translation-type: tm+mt
source-git-commit: 64a91795bd2f9120991be2a67e68c645dc24c8d1
workflow-type: tm+mt
source-wordcount: '1205'
ht-degree: 5%

---

# Parameters aanvragen{#request-parameters}

## Analysegegevens

| Aanvraagsleutel  | Vereist | Instellen op... |  Beschrijving  |
| --- | :---: | :---: | --- |
| `analytics.trackingServer` | Y | `sessionStart` | De URL van uw Adobe Analytics-server |
| `analytics.reportSuite` | Y | `sessionStart` | De id die uw analysegegevens identificeert |
| `analytics.enableSSL` | N | `sessionStart` | Waar of onwaar voor het inschakelen van SSL |
| `analytics.visitorId` | N | `sessionStart` | De Adobe-bezoeker-id is een aangepaste id die u kunt gebruiken in meerdere Adobe-toepassingen. De hartslag `visitorId` is gelijk aan de Analytics `VID.` |

## Bezoekersgegevens

| Aanvraagsleutel  | Vereist | Instellen op... |  Beschrijving  |
| --- | :---: | :---: | --- |
| `visitor.marketingCloudOrgId` | Y | `sessionStart` | de Experience Cloud Organisatie-id; identificeert uw organisatie binnen het ecosysteem van Adobe Experience Cloud |
| `visitor.marketingCloudUserId` | N | `sessionStart` | Dit is de Experience Cloud-gebruikersnaam (ECID). In de meeste gevallen is dit de id die u moet gebruiken om een gebruiker te identificeren. De hartslag `marketingCloudUserId` is gelijk aan `MID` in Adobe Analytics. Hoewel deze parameter technisch niet vereist is, is deze vereist voor toegang tot de Experience Cloud-reeks apps. |
| `visitor.aamLocationHint` | N | `sessionStart` | Biedt Adobe Audience Manager Edge-gegevens — Als geen waarde wordt ingevoerd, is de waarde null. |
| `appInstallationId` | N | `sessionStart` | De appInstallationId identificeert de app en het apparaat op unieke wijze |

## Inhoudsgegevens

| Aanvraagsleutel  | Vereist | Instellen op... |  Beschrijving  |
| --- | :---: | :---: | --- |
| `media.id` | Y | `sessionStart` | Unieke id voor de inhoud |
| `media.name` | N | `sessionStart` | Menselijke leesbare naam voor de inhoud |
| `media.length` | Y | `sessionStart` | Lengte van inhoud (seconden) |
| `media.contentType` | Y | `sessionStart` | Indeling van de stream (kan elke tekenreeks zijn, een aantal aanbevolen waarden zijn &quot;Live&quot;, &quot;VOD&quot; of &quot;Lineair&quot;) |
| `media.playerName` | Y | `sessionStart` | De naam van de speler die verantwoordelijk is voor het renderen van de inhoud |
| `media.channel` | Y | `sessionStart` | Het distributiekanaal van de inhoud. Dit kan een mobiele toepassingsnaam of een websitenaam, eigenschapsnaam zijn |
| `media.resume` | N | `sessionStart` | Geeft aan of een gebruiker een vorige sessie hervat (in tegenstelling tot het starten van een nieuwe sessie) |
| `media.sdkVersion` | N | `sessionStart` | De SDK-versie die door de speler wordt gebruikt |

## Metagegevens inhoudstandaard

| Aanvraagsleutel  | Vereist | Instellen op... |  Beschrijving  |
| --- | :---: | :---: | --- |
| `media.streamFormat` | N | `sessionStart` | Stroomindeling, bijvoorbeeld &quot;HD&quot; |
| `media.show` | N | `sessionStart` | De naam van het programma of de serie |
| `media.season` | N | `sessionStart` | Het seizoensnummer waartoe de show of serie behoort |
| `media.episode` | N | `sessionStart` | Het nummer van de episode |
| `media.assetId` | N | `sessionStart` | De unieke id voor de inhoud van het video-element, zoals de aflevering-id van de tv-reeks, de id van het filmelement of de livegebeurtenis. Deze id&#39;s zijn doorgaans afgeleid van metagegevensautoriteiten zoals EIDR, TMS/Gracenote of Rovi. Deze id&#39;s kunnen ook afkomstig zijn van andere bedrijfseigen of interne systemen. |
| `media.genre` | N | `sessionStart` | Het type inhoud zoals gedefinieerd door de inhoudproducent |
| `media.firstAirDate` | N | `sessionStart` | De datum waarop de inhoud voor het eerst op televisie werd uitgezonden |
| `media.firstDigitalDate` | N | `sessionStart` | De datum waarop de inhoud voor het eerst is verzonden op een digitaal platform |
| `media.rating` | N | `sessionStart` | De rating zoals gedefinieerd in de TV Parental Guidelines |
| `media.originator` | N | `sessionStart` | De maker van de inhoud |
| `media.network` | N | `sessionStart` | De naam van het netwerk/kanaal |
| `media.showType` | N | `sessionStart` | Het type inhoud, uitgedrukt als een geheel getal tussen 0 en 3: <ul> <li>0 - Volledige aflevering </li> <li>1 - Voorvertoning </li> <li>2 - Clip </li> <li>3 - Overige </li> </ul> |
| `media.adLoad` | N | `sessionStart` | Het type geladen advertentie |
| `media.pass.mvpd` | N | `sessionStart` | MVPD verstrekt door de authentificatie van de Adobe |
| `media.pass.auth` | N | `sessionStart` | Geeft aan dat de gebruiker is geautoriseerd via Adobe-verificatie (kan alleen waar zijn als deze is ingesteld) |
| `media.dayPart` | N | `sessionStart` | De tijd van de dag waarop de inhoud werd uitgezonden |
| `media.feed` | N | `sessionStart` | Het type diervoeder, bijvoorbeeld &quot;West-HD&quot; |

## Advertentiegegevens

| Aanvraagsleutel  | Vereist | Instellen op... |  Beschrijving  |
| --- | :---: | :---: | --- |
| `media.ad.podFriendlyName` | N | `adBreakStart` | Vriendschappelijke naam van het advertentiepad |
| `media.ad.podIndex` | Y | `adBreakStart` | De index van de advertentiepod in de video |
| `media.ad.podSecond` | Y | `adBreakStart` | De tweede waarmee de pod is gestart |
| `media.ad.podPosition` | Y | `adStart` | De index van de advertentie binnen het advertentiespoor dat bij 1 begint |
| `media.ad.name` | N | `adStart` | Vriendelijke naam van de advertentie |
| `media.ad.id` | Y | `adStart` | Naam van de advertentie |
| `media.ad.length` | Y | `adStart` | Lengte van de video en in seconden |
| `media.ad.playerName` | Y | `adStart` | De naam van de speler die verantwoordelijk is voor het renderen van de advertentie |

## Standaardmetagegevens toevoegen

| Aanvraagsleutel  | Vereist | Instellen op... |  Beschrijving  |
| --- | :---: | :---: | --- |
| `media.ad.advertiser` | N | `adStart` | De onderneming of het merk waarvan het product in de advertentie voorkomt |
| `media.ad.campaignId` | N | `adStart` | De id van de advertentiecampagne |
| `media.ad.creativeId` | N | `adStart` | De id van de advertentie is creatief |
| `media.ad.siteId` | N | `adStart` | De id van de advertentiesite |
| `media.ad.creativeURL` | N | `adStart` | De URL van de advertentie |
| `media.ad.placementId` | N | `adStart` | De plaatsings-id van de advertentie |

## Hoofdgegevens

| Aanvraagsleutel  | Vereist | Instellen op... |  Beschrijving  |
| --- | :---: | :---: | --- |
| `media.chapter.index` | Y | `chapterStart` | Hiermee wordt de positie van het hoofdstuk in de inhoud aangegeven |
| `media.chapter.offset` | Y | `chapterStart` | De tweede functie in het afspelen waar het hoofdstuk begint |
| `media.chapter.length` | Y | `chapterStart` | De lengte van het hoofdstuk in seconden |
| `media.chapter.friendlyName` | N | `chapterStart` | De mensvriendelijke naam van het hoofdstuk |

## Kwaliteitsgegevens

| Aanvraagsleutel  | Vereist | Instellen op... |  Beschrijving  |
| --- | :---: | :---: | --- |
| `media.qoe.bitrate` | N | Alle | De bitsnelheid van de stream |
| `media.qoe.droppedFrames` | N | Alle | Het aantal gedropte frames in de stream |
| `media.qoe.framesPerSecond` | N | Alle | Het aantal frames per seconde |
| `media.qoe.timeToStart` | N | Alle | De hoeveelheid tijd (in milliseconden) die wordt doorgegeven tussen het moment dat de gebruiker in aanraking komt met afspelen en het moment waarop de inhoud wordt geladen en het moment waarop wordt begonnen met afspelen |

## California Consumer Privacy Act (CCPA) Parameters {#ccpa-params}

| Aanvraagsleutel  | Vereist | Instellen op... |  Beschrijving  |
| --- | :---: | :---: | --- |
| `analytics.optOutServerSideForwarding` | N | `sessionStart` | Ingesteld op true wanneer de eindgebruiker ervoor heeft gekozen geen gegevens meer te delen tussen Adobe Analytics en andere Experience Cloud-oplossingen (bijvoorbeeld Audience Manager) |
| `analytics.optOutShare` | N | `sessionStart` | Wordt ingesteld op true wanneer de eindgebruiker heeft opgegeven dat zijn gegevens niet meer worden gefedereerd (bijvoorbeeld aan andere Adobe Analytics-clients). |

## Aanvullende details {#additional-details}

### visitor.marketingCloudUserId

Geef de Experience Cloud gebruiker-id (ook wel `MID` of `MCID` genoemd) op de `sessionStart` vraag door het binnen de `params` kaart te omvatten gebruikend de volgende sleutel: **bezoeker.marketingCloudUserId**. Dit is een handige functie als u al met andere Experience Cloud-producten hebt geïntegreerd en de MCID al hebt verkregen.

>[!NOTE]
>
>Media Analytics (MA) is geïntegreerd met de Experience Cloud-reeks apps (Adobe Analytics, Audience Manager, Doel, enzovoort). U hebt een Experience Cloud-id nodig om deze apps te openen. _ECID is wat u zou moeten gebruiken om gebruikers in de meeste scenario&#39;s te identificeren._

### appInstallationId

* **Als u  *geen* waarde  `appInstallationId` doorgeeft - zal** het achterste eind van MA geen MCID meer produceren, maar in plaats daarvan op Adobe Analytics vertrouwen om dit te doen. Adobe om of een MCID te verzenden als beschikbaar, of `appInstallationId` (samen met nog verplicht `marketingCloudOrgId`) zodat de Inzameling API van Media MCID produceert en het op alle vraag verzendt.

* **Als u  ** overslaat  `appInstallationId` waarde -** MCID  *kan door het achterste eind van MA worden* geproduceerd, als u waarden voor  `appInstallationId` en de (vereiste)  `marketingCloudOrgId` parameters doorgeeft. Als u `appInstallationId` zelf doorgeeft, moet u de waarde ervan aan de clientzijde behouden. De toepassing moet uniek zijn voor de toepassing op een apparaat en moet blijvend zijn zolang de toepassing niet opnieuw wordt geïnstalleerd.

>[!NOTE]
>
>De `appInstallationId` identificeert uniek app *en het apparaat*. Deze moet uniek zijn voor elke toepassing op elk apparaat, d.w.z. twee gebruikers die dezelfde versie van dezelfde app op verschillende apparaten gebruiken, moeten elk een andere (unieke) `appInstallationId` verzenden.

<!-- Initially, there were no browser-based customers. In future this will be part of a two-bullet list, one bullet for Native Apps, the other for Browser apps. The .
\<ul id="ul_iwc_fqt_pbb"\>
 \<li\>For Browser Apps, this should be a first-party cookie that is persistent for as long as the user stays in the same browser. If clients have multiple websites, they need to have different cookies for each site.</li>
</ul> -->

### visitor.marketingCloudOrgId

Naast noodzakelijk voor MCID-generatie wanneer dat niet is opgegeven, wordt deze parameter ook gebruikt als de waarde voor de uitgevers-id (op basis waarvan Media Analytics [federation rule matching.](/help/federated-analytics.md) uitvoert).

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

De waarde `visitor.customerIDs` kan een willekeurig aantal objecten in de gepresenteerde indeling hebben.

### visitor.aamLocationHint

Deze parameter geeft aan welke Adobe Audience Manager (AAM) Edge wordt bereikt wanneer Adobe Analytics de klantgegevens naar de Audience Manager verzendt. Als u deze parameter niet overgaat, hardcodeert Adobe het aan 1. Dit is met name van belang wanneer eindgebruikers hun apparaten doorgaans gebruiken op geografisch afgelegen locaties (bijvoorbeeld VS-Oost, VS-West, Europa, Azië). Anders worden de gebruikersgegevens over meerdere AAM Randen verspreid.

### media.resume

Als de app bepaalt dat een sessie werd gesloten en vervolgens op een later tijdstip wordt hervat, bijvoorbeeld als de gebruiker de video heeft verlaten maar uiteindelijk is teruggekomen, en de speler de video heeft hervat vanaf de afspeelkop waar deze is gestopt, kunt u een optionele booleaanse parameter **media.resume** verzenden binnen het paramemenu van de `sessionStart`-aanroep.

<!--
| `media.uniqueTimePlayed` | N | Close | The value in seconds of the unique segments of content played during a session. Excludes time played on seek back scenarios in which a viewer is watching the same segment of the content multiple times.  |
-->
