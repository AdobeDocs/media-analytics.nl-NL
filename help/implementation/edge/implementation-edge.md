---
title: Adobe-streaming mediaservices implementeren met de Edge Network
description: Leer hoe Adobe streaming media services kunnen worden geïmplementeerd met Experience Platform Edge.
feature: Streaming Media
role: User, Admin, Developer
exl-id: dfdb1415-105e-4c41-bedc-ecb85ed1b1d9
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '2152'
ht-degree: 0%

---

# Implementeer de verzameling Streaming Media met de Edge Network

Met Adobe Experience Platform Edge Network kunt u gegevens die bestemd zijn voor meerdere producten naar een gecentraliseerde locatie verzenden. De ervaring met Edge geeft de juiste informatie door aan de gewenste producten. Met dit concept kunt u de implementatie-inspanningen consolideren, met name voor het overspannen van meerdere gegevensoplossingen.

In de volgende afbeelding ziet u hoe de invoegtoepassing voor het streamen van media-verzamelingen kan worden geïmplementeerd om Experience Platform Edge te gebruiken om gegevens beschikbaar te maken in Analysis Workspace, in Adobe Analytics of Customer Journey Analytics:

![&#x200B; het werkschema van CJA &#x200B;](assets/streaming-media-edge.png)

Voor een overzicht van alle implementatieopties, met inbegrip van implementatiemethodes die Experience Platform Edge niet gebruiken, zie [&#x200B; het stromen media diensten voor Adobe Analytics of Customer Journey Analytics uitvoeren &#x200B;](/help/implementation/overview.md).

Ongeacht of u de Adobe Experience Platform Web SDK, Adobe Experience Platform Mobile SDK, Adobe Experience Platform Roku SDK, of API gebruikt om de het stromen Media Inzameling met Ervaring Edge uit te voeren, moet u eerst de volgende secties voltooien:

## Schema instellen in Adobe Experience Platform

Om gegevensinzameling voor gebruik over toepassingen te standaardiseren die hefboomwerking Adobe Experience Platform, heeft Adobe de open en openbaar gedocumenteerde norm, het Model van de Gegevens van de Ervaring (XDM) gecreeerd.

Een schema maken en instellen:

1. In Adobe Experience Platform, begin creërend het schema zoals die in [&#x200B; wordt beschreven creeer en geef schema&#39;s in UI &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=nl-NL) uit.

1. Op de pagina van de details van het Schema wanneer het creëren van het schema, kies {de Gebeurtenis van de 0} Ervaring [!UICONTROL **wanneer het kiezen van de basisklasse voor het schema.**]

   ![&#x200B; Toegevoegde gebiedsgroepen &#x200B;](assets/schema-experience-event.png)

1. Selecteer [!UICONTROL **daarna**].

1. Specificeer een naam en een beschrijving van de schemavertoning, dan uitgezochte [!UICONTROL **Afwerking**].

1. In het [!UICONTROL **gebied van de Samenstelling**], in de [!UICONTROL **3&rbrace; sectie van de Groepen van het Gebied &lbrace;, uitgezocht**] voeg [!UICONTROL **toe, dan onderzoek naar en voeg de volgende nieuwe gebiedsgroepen aan het schema toe:**]
   * `End User ID Details`
   * `Implementation Details`
   * `MediaAnalytics Interaction Details`

   Nadat u de gebiedsgroepen toevoegt, zouden zij in de [!UICONTROL **sectie van de Groepen van het Gebied**], als volgt moeten tonen:

   ![&#x200B; Toegevoegde gebiedsgroepen &#x200B;](assets/schema-field-groups-added.png)

1. Selecteer [!UICONTROL **sparen**] om uw veranderingen te bewaren.

1. (Optioneel) U kunt bepaalde velden verbergen die niet worden gebruikt door de Media Edge API. Het verbergen van deze gebieden maakt het schema gemakkelijker te lezen en te begrijpen, maar het wordt niet vereist. Deze velden verwijzen alleen naar de velden in de veldgroep `MediaAnalytics Interaction Details` .

   +++ Vouw hier uit om instructies weer te geven voor velden die u kunt verbergen.

   1. Op het [!UICONTROL **gebied van de Structuur**], selecteer het `Media Collection Details` gebied, dan uitgezocht [!UICONTROL **beheer verwante gebieden**].

      ![&#x200B; leiden-verwant-gebieden &#x200B;](assets/manage-related-fields.png)

   1. Laat de optie toe om [!UICONTROL **vertoningsnamen voor gebieden**] te tonen, dan het schema als volgt bij te werken:

      * Verberg in het veld `Media Collection Details` > `Advertising Details` de volgende rapportvelden: `Ad Completed` , `Ad Started` en `Ad Time Played` .

      * Verberg het volgende rapportveld in het veld `Media Collection Details` > `Advertising Pod Details` : `Ad Break ID`

      * Verberg in het veld `Media Collection Details` > `Chapter Details` de volgende rapportvelden: `Chapter Completed` , `Chapter ID` , `Chapter Started` en `Chapter Time Played` .

      * Verberg het veld `Media Collection Details` in het veld `List Of States` .

        ![&#x200B; verbergt media inzamelingsstaten &#x200B;](assets/schema-hide-media-collection-states.png)

      * Verberg in het veld `Media Collection Details` > `List Of States End` en `Media Collection Details` > `List Of States Start` de volgende rapportvelden: `Player State Count` , `Player State Set` en `Player State Time` .

        ![&#x200B; te verbergen gebieden &#x200B;](assets/schema-hide-listofstates.png)

      * Verberg in het veld `Media Collection Details` > `Qoe Data Details` de volgende rapporteringsvelden: `Average Bitrate` , `Average Bitrate Bucket`, `Bitrate Change Impacted Streams` , `Bitrate Changes`, `Buffer Impacted Streams` , `Buffer Events`, `Dropped Frame Impacted Streams`, `Drops Before Starts`, `Errors`, `External Error IDs`, `Error Impacted Streams`, `Media SDK Error IDs`, `Player SDK Error IDs`, `Stalling Impacted Streams`, `Stalling Events`, `Total Buffer Duration` en `Total Stalling Duration` 8&rbrace;.

      * Verberg in het veld `Media Collection Details` > `Session Details` de volgende rapporteringsvelden: `10% Progress Marker` , `25% Progress Marker`, `50% Progress Marker` , `75% Progress Marker`, `95% Progress Marker` , `Ad Count`, `Average Minute Audience`, `Content Completes`, `Chapter Count`, `Content Starts`, `Content Time Spent`, `Estimated Streams`, `Federated Data`, `Media Segment Views`, `Media Downloaded Flag`, `Media Starts`, `Media Session ID` 8&rbrace;, `Media Session Server Timeout`, `Media Time Spent`, `Pause Events`, `Pause Impacted Streams`, `Pev3`, `Pccr`, `Total Pause Duration`, `Unique Time Played` en `Video Segment` .

   1. Selecteer [!UICONTROL **bevestigen**] om uw veranderingen te bewaren.

   1. Op het [!UICONTROL **gebied van de Structuur**], laat de optie toe [!UICONTROL **vertoningsnamen voor gebieden**] tonen, dan het `List Of Media Collection Downloaded Content Events` gebied selecteren.

   1. Selecteer [!UICONTROL **beheer verwante gebieden**], dan werk het schema als volgt bij:


      * Verberg in het veld `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Details` de volgende rapportvelden: `Ad Completed` , `Ad Started` en `Ad Time Played` .

      * Verberg het volgende rapportveld in het veld `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Pod Details` : `Ad Break ID`

      * Verberg in het veld `List Of Media Collection Downloaded Content Events` > `Media Details` > `Chapter Details` de volgende rapportvelden: `Chapter Completed` , `Chapter ID` , `Chapter Started` en `Chapter Time Played` .

      * Verberg het veld `List Of Media Collection Downloaded Content Events` in het veld `Media Details` > `List Of States` .

      * Verberg in het veld `List Of Media Collection Downloaded Content Events` > `Media Details` > `List Of States End` en `Media Collection Details` > `List Of States Start` de volgende rapportvelden: `Player State Count`, `Player State Set` en `Player State Time` .

      * Verberg in het veld `List Of Media Collection Downloaded Content Events` > `Media Details` > `Qoe Data Details` de volgende rapporteringsvelden: `Average Bitrate`, `Average Bitrate Bucket`, `Bitrate Change Impacted Streams`, `Bitrate Changes`, `Buffer Events`, `Buffer Impacted Streams`, `Drops Before Starts`, `Dropped Frame Impacted Streams`, `Error Impacted Streams`, `Errors`, `External Error IDs`, `Media SDK Error IDs`, `Player SDK Error IDs`, `Stalling Events`, `Stalling Impacted Streams`, `Total Buffer Duration` 8&rbrace; en `Total Stalling Duration` .

      * Verberg in het veld `List Of Media Collection Downloaded Content Events` > `Media Details` > `Session Details` de volgende rapporteringsvelden: `10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Ad Count`, `Average Minute Audience`, `Chapter Count`, `Content Completes`, `Content Starts`, `Content Time Spent`, `Estimated Streams`, `Federated Data`, `Media Downloaded Flag`, `Media Segment Views`, `Media Session ID` 8&rbrace;, `Media Session Server Timeout`, `Media Starts`, `Media Time Spent`, `Pause Events`, `Pause Impacted Streams`, `Pccr`, `Pev3`, `Total Pause Duration`, `Unique Time Played` en `Video Segment` .

      * Verberg het veld `List Of Media Collection Downloaded Content Events` in het veld `Media Details` > `Media Session ID` .

   1. Selecteer [!UICONTROL **bevestigen**] om uw veranderingen te bewaren.

   1. Op het [!UICONTROL **gebied van de Structuur**], selecteer het `Media Reporting Details` gebied, uitgezocht [!UICONTROL **beheer verwante gebieden**].

   1. Laat de optie toe om [!UICONTROL **vertoningsnamen voor gebieden**] te tonen, dan het schema als volgt bij te werken:

      * Verberg in het veld `Media Reporting Details` de volgende velden: `Error Details` , `List Of States End` , `List of States Start` en `Media Session ID` .

   1. Selecteer [!UICONTROL **bevestigen**] > [!UICONTROL **sparen**] om uw veranderingen te bewaren.

   +++

1. (Optioneel) U kunt aangepaste metagegevens toevoegen aan uw schema. Op deze manier kunt u aanvullende, door de gebruiker gedefinieerde metagegevens opnemen die u kunt aanpassen aan specifieke behoeften of contexten. Deze flexibiliteit is handig in situaties waarin bestaande schema&#39;s de gewenste gegevenspunten niet dekken. (U kunt ook werken met aangepaste metagegevens met Media Edge API&#39;s. Voor meer informatie, zie [&#x200B; douanemetagegevens met Media Edge APIs &#x200B;](https://developer.adobe.com/cja-apis/docs/endpoints/media-edge/custom-metadata/) creëren.)

   +++ Vouw hier uit om instructies weer te geven over het toevoegen van aangepaste metagegevens aan uw schema.

   1. Bepaal de plaats van de naam van de huurder van de org door [!UICONTROL **Info van de Rekening**] > [!UICONTROL **Toegewezen organen**] > [!UICONTROL _**organnaam**_] > [!UICONTROL **huurder**] te selecteren.

      Deze aangepaste velden worden via dit pad ontvangen. (Bijvoorbeeld naam huurder: _dcbl → myCustomField path: _dcbl.myCustomField.)

   1. Voeg een aangepaste veldgroep toe aan het door u gedefinieerde mediaschema.

      ![&#x200B; toe:voegen-douane-meta-gegevens &#x200B;](assets/add-custom-metadata-fieldgroup.png)

   1. Voeg aangepaste velden die u wilt bijhouden toe aan de veldgroep.

      ![&#x200B; toe:voegen-douane-meta-gegevens &#x200B;](assets/add-custom-fields.png)

   1. [&#x200B; Gebruik de weg die &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-platform/xdm/ui/fields/overview#type-specific-properties) voor het douanegebied in uw verzoeklading wordt geproduceerd.

      ![&#x200B; toe:voegen-douane-meta-gegevens &#x200B;](assets/custom-fields-path.png)

   +++

1. Ga met [&#x200B; verder creeer een dataset in Adobe Experience Platform &#x200B;](#create-a-dataset-in-adobe-experience-platform).

## Een gegevensset maken in Adobe Experience Platform

1. Zorg ervoor dat u opstelling een schema zoals die in [&#x200B; wordt beschreven opstelling het Schema in Adobe Experience Platform &#x200B;](#set-up-the-schema-in-adobe-experience-platform).

1. In Adobe Experience Platform, begin creërend de dataset zoals die in [&#x200B; wordt beschreven gids UI van Datasets &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=nl-NL#create).

   Wanneer het selecteren van een schema voor uw dataset, kies het schema dat u eerder creeerde, zoals die in [&#x200B; wordt beschreven Opstelling het Schema in Adobe Experience Platform &#x200B;](#set-up-the-schema-in-adobe-experience-platform).

1. Ga met [&#x200B; verder vormen een gegevensstroom in Customer Journey Analytics &#x200B;](#configure-a-datastream-in-adobe-experience-platform).

## Een gegevensstroom configureren in Adobe Experience Platform

1. Zorg ervoor dat u een dataset zoals die in [&#x200B; wordt beschreven creeerde een dataset in Adobe Experience Platform &#x200B;](#create-a-dataset-in-adobe-experience-platform).

1. Creeer een nieuwe gegevensstroom zoals die in [&#x200B; wordt beschreven vormt een datastream &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=nl-NL).

   Zorg er bij het maken van de gegevensstroom voor dat u de volgende configuratieselecties maakt:

   * Op het [!UICONTROL **Schema van de Gebeurtenis**] gebied wanneer het creëren van de gegevensstroom, zorg ervoor dat u het schema selecteert dat u in [&#x200B; opstelling het schema in Adobe Experience Platform &#x200B;](#set-up-the-schema-in-adobe-experience-platform) creeerde. Selecteer [!UICONTROL **sparen**].

     >[!IMPORTANT]
     >
     >Selecteer niet [!UICONTROL **sparen en voeg Toewijzing**] toe omdat het doen dit in afbeeldingsfouten voor het gebied van de Chronologie zal resulteren.

     ![&#x200B; creeer gegevensstroom en selecteer schema &#x200B;](assets/datastream-create-schema.png)

   * Voeg een van de volgende services toe aan de gegevensstroom, afhankelijk van of u Adobe Analytics of Customer Journey Analytics gebruikt:

      * [!UICONTROL **Adobe Analytics**] (als het gebruiken van Adobe Analytics)

        Als u Adobe Analytics gebruikt, zorg ervoor u een rapportreeks bepaalt, zoals die in [&#x200B; wordt beschreven creeer een rapportreeks &#x200B;](https://experienceleague.adobe.com/nl/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/t-create-a-report-suite).

      * [!UICONTROL **Adobe Experience Platform**] (als het gebruiken van Customer Journey Analytics)

     Voor informatie over hoe te om de dienst aan een datastream toe te voegen, zie de &quot;diensten aan een datastream&quot;sectie in [&#x200B; een datastream &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=nl-NL#view-details) vormen.

     ![&#x200B; voeg de dienst van Adobe Analytics &#x200B;](assets/datastream-add-service.png) toe

      * Breid [!UICONTROL **Geavanceerde Opties**] uit, dan laat de [!UICONTROL **Analytics van Media**] optie toe.

     ![&#x200B; de optie van Analytics van Media &#x200B;](assets/datastream-media-check.png)

1. U bent nu klaar om [&#x200B; Media Edge API &#x200B;](/help/implementation/edge/implementation-edge-api.md) of [&#x200B; Media Edge SDK &#x200B;](/help/implementation/edge/edge-mobile-sdk.md) uit te voeren om media analysegegevens te beginnen verzamelen.

   Nadat u wat gegevens hebt verzameld, kunt u [&#x200B; een verbinding in Customer Journey Analytics &#x200B;](#create-a-connection-in-customer-journey-analytics) tot stand brengen.

## Verbinding maken in Customer Journey Analytics

>[!NOTE]
>
>De volgende procedure is alleen vereist als u Customer Journey Analytics gebruikt.

1. Zorg ervoor dat u een gegevensstroom zoals die in [&#x200B; wordt beschreven vormde een gegevensstroom in Customer Journey Analytics &#x200B;](#configure-a-datastream-in-adobe-experience-platform).

1. In Customer Journey Analytics, creeer een verbinding zoals die in [&#x200B; wordt beschreven creeer een verbinding &#x200B;](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-connections/create-connection.html?lang=nl-NL).

   Wanneer u de verbinding maakt, zijn de volgende configuratieselecties vereist voor de implementatie van de streamingmedia-verzameling:

   1. Selecteer de dataset die u eerder creeerde, zoals die in [&#x200B; wordt beschreven creeer een dataset in Adobe Experience Platform &#x200B;](#create-a-dataset-in-adobe-experience-platform).

   1. Zorg ervoor dat de [!UICONTROL **Invoer alle nieuwe gegevens**] het plaatsen wordt toegelaten.

1. Ga met [&#x200B; verder creeer een gegevensmening in Customer Journey Analytics &#x200B;](#create-a-new-data-view-in-customer-journey-analytics).

## Een gegevensweergave maken in Customer Journey Analytics

>[!NOTE]
>
>De volgende procedure is alleen vereist als u Customer Journey Analytics gebruikt.

1. Zorg ervoor dat u een verbinding in Customer Journey Analytics zoals die in [&#x200B; wordt beschreven creeerde een verbinding in Customer Journey Analytics &#x200B;](#create-a-connection-in-customer-journey-analytics).

1. In de Analtyics van de Reis van de Klant, creeer een gegevensmening zoals die in [&#x200B; wordt beschreven creeer of geef een gegevensmening &#x200B;](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html?lang=nl-NL) uit.

   Bij het maken van de gegevensweergave zijn de volgende configuratieselecties vereist voor de implementatie van de Streaming Media Collection:

   1. Op het [!UICONTROL **gebied van de Verbinding**], selecteer de verbinding die u eerder creeerde, zoals die in [&#x200B; wordt beschreven creeer een verbinding in Customer Journey Analytics &#x200B;](#create-a-connection-in-customer-journey-analytics).

      Het kan 15 minuten duren voordat de verbinding die u hebt gemaakt beschikbaar is om te selecteren.

   1. Op het [!UICONTROL **lusje van Componenten**], in de [!UICONTROL **gebieden van het Schema**] sectie, onderzoek naar elke component die in de lijsten hieronder wordt vermeld en sleep het in het [!UICONTROL **Metriek**] paneel. Als er meerdere velden met dezelfde naam bestaan, gebruikt u het XDM-pad om te controleren of dit het juiste veld is.

      **Belangrijkste inhoud - de metriek van de Inhoud**

      | Componentnaam | XDM-pad |
      |----------|---------|
      | Start media | mediaReporting.sessionDetails.isViewed |
      | Weergaven van mediasegment | mediaReporting.sessionDetails.hasSegmentView |
      | Inhoud start | mediaReporting.sessionDetails.isPlayed |
      | Inhoud voltooid | mediaReporting.sessionDetails.isCompleted |
      | Tijd van inhoud besteed | mediaReporting.sessionDetails.timePlayed |
      | Tijd besteed aan media | mediaReporting.sessionDetails.totalTimePlayed |
      | Unieke afgespeelde tijd | mediaReporting.sessionDetails.uniqueTimePlayed |
      | Voortgangsmarkering 10% | mediaReporting.sessionDetails.hasProgress10 |
      | Gemiddeld aantal minuten publiek | mediaReporting.sessionDetails.averageMinuteAudience |


      **Hoofdstuk &amp; Advertenties - Hoofdstuk &amp; de metriek van Advertenties**

      | Componentnaam | XDM-pad |
      |----------|---------|
      | Hoofdstuk gestart | mediaReporting.chapterDetails.isStarted |
      | Hoofdstuk voltooid | mediaReporting.chapterDetails.isCompleted |
      | Afspeeltijd van hoofdstuk | mediaReporting.chapterDetails.timePlayed |
      | Advertentie gestart | mediaReporting.advertisingDetails.isStarted |
      | Advertentie voltooid | mediaReporting.advertisingDetails.isCompleted |
      | Ad-tijd afgespeeld | mediaReporting.advertisingDetails.timePlayed |


      **QoE - QoE metriek**

      | Componentnaam | XDM-pad |
      |----------|---------|
      | Te starten tijd | mediaReporting.qoeDataDetails.timeToStart |
      | Drops voordat wordt gestart | mediaReporting.qoeDataDetails.isDroppedBeforeStart |
      | Door buffer beïnvloede stromen | mediaReporting.qoeDataDetails.hasBufferImpactedStreams |
      | Door bitsnelheidwijziging beïnvloede stromen | mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams |
      | Wijzigingen in bitsnelheid | mediaReporting.qoeDataDetails.bitrateChangeCount |
      | Gemiddelde bitsnelheid | mediaReporting.qoeDataDetails.bitrateAverage |
      | Gedropte frames | mediaReporting.qoeDataDetails.droppedFrames |
      | Fouten | mediaReporting.qoeDataDetails.errorCount |
      | Fout beïnvloede stromen | mediaReporting.qoeDataDetails.hasErrorImpactedStreams |
      | Gedropte framestromen | mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams |


      **staat van de Speler - de staatsmetriek van de Speler**

      | Componentnaam | XDM-pad |
      |----------|---------|
      | Set spelerstatussen | mediaReporting.states.isSet |
      | Aantal statussen van speler | mediaReporting.states.count |
      | Frametijd van speler | mediaReporting.states.time |


   1. Werk de etiketten (in het [!UICONTROL **drop-down menu van de Context labels**]) voor de componenten in de volgende lijst bij. Zoek naar componenten en sleep om het even welke componenten die nog niet in het metriekpaneel in het paneel zijn.

      | Componentnaam | Contextlabel |
      |---------|----------|
      | Tijdslimiet mediasessie | Media: Seconden sinds laatste vraag |
      | Tijd besteed aan media | Media: media-tijd besteed |
      | Totale bufferduur | Media: totale bufferduur |
      | Te starten tijd | Media: Te starten tijd |
      | Totale pauzeduur | Media: totale pauzeduur |

   1. Om onderverdelingen aan uw project van Customer Journey Analytics toe te voegen, voeg de volgende afmetingen aan het [!UICONTROL **paneel van Dimensies**] toe:

      | XDM-pad | Componentnaam |
      |---------|----------|
      | mediaReporting.states.name | Framenaam van speler |
      | mediaReporting.sessionDetails.ID | Mediasessie-id |

      Naast de afmetingen in deze tabel kunt u alle andere afmetingen toevoegen die u beschikbaar wilt maken om gegevens te filteren op basis van Customer Journey Analytics-projecten.

1. Selecteer [!UICONTROL **sparen en ga**] > [!UICONTROL **&#x200B;**] verder sparen en beëindigen om uw veranderingen te bewaren.

1. Ga met [&#x200B; verder creeer en vorm een project in Customer Journey Analytics &#x200B;](#create-and-configure-a-project-in-customer-journey-analytics).

## Een project maken en configureren in Customer Journey Analytics

1. Zorg ervoor dat u een gegevensmening in Customer Journey Analytics zoals die in [&#x200B; wordt beschreven creeerde een gegevensmening in Customer Journey Analytics &#x200B;](#create-a-new-data-view-in-customer-journey-analytics).

1. In Customer Journey Analytics, in het [!UICONTROL **Workspace**] lusje, in het [!UICONTROL **gebied van Projecten**], uitgezocht [!UICONTROL **creeer project**].

1. Selecteer [!UICONTROL **Leeg project**] > [!UICONTROL **creëren**].

1. Selecteer in het nieuwe project de gegevensweergave die u eerder hebt gemaakt.

   Wanneer het creëren van panelen in uw project, kunt u om het even welke componenten gebruiken die u aan uw gegevensmening toevoegde, zoals die in [&#x200B; wordt beschreven creeer een gegevensmening in Customer Journey Analytics &#x200B;](#create-a-new-data-view-in-customer-journey-analytics).

   De volgende vier deelvensters zijn voorbeelden van deelvensters die u kunt maken:

   ![&#x200B; Belangrijkste paneel van de Inhoud &#x200B;](assets/main-content-panel.png)

   ![&#x200B; Hoofdstuk en advertenties paneel &#x200B;](assets/chapter-and-ads-panel.png)

   ![&#x200B; QoE paneel &#x200B;](assets/qoe-panel.png)

   ![&#x200B; Plater staatspaneel &#x200B;](assets/player-state-panel.png)

1. Selecteer het **pictogram van Panelen** in het linkerspoor, dan belemmering in het [!UICONTROL **gelijktijdige kijkers van Media**] paneel en de [!UICONTROL **doorgebrachte tijd van de media playback**] paneel.

   De twee deelvensters moeten er als volgt uitzien:

   ![&#x200B; Medium gezamenlijke kijkers paneel &#x200B;](assets/media-concurrent-viewers-panels.png)

   ![&#x200B; de playbacktijd van media bestede paneel &#x200B;](assets/media-playback-time-spent-panels.png)

1. (Voorwaardelijk) als u douanemetagegevens aan uw schema toevoegde, zoals die in Stap 8 van [&#x200B; worden beschreven opstelling het schema in Adobe Experience Platform &#x200B;](#set-up-the-schema-in-adobe-experience-platform), dan moet u de persistentie voor de douanegebieden plaatsen, zoals die in [&#x200B; de montages van de componenten van de Persistentie &#x200B;](https://experienceleague.adobe.com/nl/docs/analytics-platform/using/cja-dataviews/component-settings/persistence) in de gids van Customer Journey Analytics wordt beschreven.

   Wanneer gegevens in Customer Journey Analytics worden ontvangen, is de dimensie Aangepaste gebruikersnaam beschikbaar.

   ![&#x200B; opstelling-douane-meta-gegevens &#x200B;](assets/custom-metadata-dimension.png)

   >[!NOTE]
   >
   >Als u Adobe Analytics instelt als een upstream voor uw gegevensstroom, zijn de aangepaste metagegevens ook aanwezig in ContextData, met de naam die u instelt in het schema (zonder het voorvoegsel van de huurder, bijvoorbeeld myCustomField). Dit maakt het mogelijk om alle eigenschappen van Adobe Analytics beschikbaar voor ContextData, zoals [&#x200B; te gebruiken creërend een verwerkingsregel &#x200B;](https://experienceleague.adobe.com/nl/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/processing-rules).

1. Deel het project zoals die in [&#x200B; wordt beschreven de projecten van het Aandeel &#x200B;](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/curate-share/share-projects.html?lang=nl-NL).

   >[!NOTE]
   >
   >   Als de gebruikers waarmee u wilt delen niet beschikbaar zijn, zorgt u ervoor dat gebruikers en beheerders toegang hebben tot Customer Journey Analytics in de Adobe Admin Console.


1. Ga met [&#x200B; verder verzenden gegevens naar Experience Platform Edge &#x200B;](#send-data-to-experience-platform-edge).

## Gegevens verzenden naar Experience Platform Edge

Afhankelijk van het type gegevens dat u naar Experience Platform Edge wilt verzenden, kunt u een van de volgende methoden gebruiken:

### Web: De Adobe Experience Platform Web SDK gebruiken

* [&#x200B; begonnen worden &#x200B;](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/)

* [Webgegevens naar Edge verzenden met de Adobe Experience Platform Web SDK](/help/implementation/edge/edge-web-sdk.md)

* [&#x200B; Migreer aan Adobe Streaming Media voor de uitbreiding van Edge Network &#x200B;](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/migration-guide/)

### Mobiel: Adobe Experience Platform Mobile SDK gebruiken

Gebruik de volgende documentatiebronnen om de implementatie voor zowel iOS als Android te voltooien:

* [&#x200B; begonnen worden &#x200B;](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/)

* [&#x200B; API verwijzing &#x200B;](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/api-reference/)

* [&#x200B; Migreer aan Adobe Streaming Media voor de uitbreiding van Edge Network &#x200B;](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/migration-guide/)

### Roku: Adobe Experience Platform Roku SDK

* [&#x200B; begonnen worden &#x200B;](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/)

* [&#x200B; Adobe Experience Platform Roku SDK &#x200B;](https://github.com/adobe/aepsdk-roku/tree/main)

* [&#x200B; Migreer aan Adobe Streaming Media voor de uitbreiding van Edge Network &#x200B;](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/migration-guide/) <!-- is the information here also applicable for Roku? -->

### API: Web en andere

De API is momenteel de enige ondersteunde manier om webgegevens naar Experience Platform Edge te verzenden.

De API is ook beschikbaar als u een aangepaste implementatie van de Edge API&#39;s wilt gebruiken.

Zie de volgende bronnen voor meer informatie over de media Edge API:

* [&#x200B; het overzicht van Edge API van Media &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/overview.html)

* [&#x200B; Aan de slag Edge API van Media &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/getting-started.html)

* [&#x200B; het oplossen van problemengids van Edge API van Media &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/troubleshooting.html)

* [&#x200B; Gebruikend het Open API specificatiedossier voor Media Edge APIs &#x200B;](https://developer.adobe.com/data-collection-apis/docs/api/media-edge/)
