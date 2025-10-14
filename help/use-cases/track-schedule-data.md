---
title: Upload planningsgegevens naar live-inhoud
description: Leer hoe u planningsgegevens uploadt om live-inhoud bij te houden.
feature: Streaming Media
role: User, Admin, Data Engineer
hide: true
hidefromtoc: true
source-git-commit: e38a83853e85418611e17015b661d8592a7c95a1
workflow-type: tm+mt
source-wordcount: '1334'
ht-degree: 0%

---

# Upload planningsgegevens naar live-inhoud

U kunt planningsgegevens van eerder live streaming media-inhoud uploaden om de viewer van live inhoud eenvoudiger en nauwkeuriger bij te houden. U kunt het viewerschap bijhouden voor afzonderlijke programma&#39;s en zelfs voor specifieke onderwerpen of programmasegmenten.

Hieronder volgen voorbeelden van live-inhoud die wordt ondersteund met het uploaden van planningsgegevens:

* SNELLE (Free Ad Supported TV) platforms

* Lokale streams

* Levende sport

* Nieuws of actuele programmering

## Mogelijkheden

Er zijn verschillende mogelijkheden beschikbaar wanneer u uploads van planningsgegevens van eerder live streaming media-inhoud gebruikt. In deze sectie worden enkele belangrijke mogelijkheden beschreven die u helpen de prestaties van het programma te analyseren.

Deze mogelijkheden zijn beschikbaar ongeacht de manier waarop u de Verzameling van de Media van de Streaming uitvoerde.

* **Accurate programma&#39;s van het spoorprogramma**: Identificeer de begin en eindtijden van elk individueel programma in de levende stroom voor de periode die u wilt analyseren. Met nauwkeurige begin- en eindtijden wordt de exacte uitvoeringstijd correct weerspiegeld en kan deze worden geanalyseerd voor elke viewersessie.

  De exacte begin- en eindtijd zijn bijvoorbeeld niet altijd bekend voor een live sportevenement totdat de gebeurtenis voorbij is. Met geüploade planningsgegevens kunt u een nauwkeurige rapportage krijgen door de begin- en eindtijd na afloop van het programma bij te werken.

* **de individuele onderwerpen of programmasegmenten van het Spoor**: Creeer nieuwe op tijd-gebaseerde afmetingen voor specifieke onderwerpen of programmasegmenten (tijdgroeven) binnen een bepaald programma. Met deze op tijd gebaseerde dimensies kunt u de viewerstatus van een programma op een specifieker niveau analyseren, zodat u inzicht kunt krijgen in welke onderwerpen of programmasegmenten het beste op de achtergrond hebben gereageerd.

  Wanneer u bijvoorbeeld een live sportevenement analyseert, zoals een voetbalwedstrijd, kunt u aparte afmetingen maken voor de eerste helft, de halve tijd en de tweede helft. Het volgen van specifieke onderwerpen of segmenten binnen een programma op deze manier staat voor gedetailleerdere onderverdelingen van kijkersgedrag toe.

* **bouwt gebruikersreizen in Journey Optimizer**: Spoor dat een persoon in een bepaalde zitting (of zelfs die onderwerpen of programmasegmenten de bekeken persoon) bekeken, dan gebruik deze gegevens in Adobe Journey Optimizer om gebruikersreizen voor klanten te bouwen die op een bepaald programma keken of die interesse in een bepaald onderwerp toonden.

## Begrijp hoe planningsgegevens werken voor het streamen van media

De functionaliteit voor het plannen van gegevens voor het stromen van Media werkt op de volgende manier:

1. Leest van de dataset van het programmaprogramma voor de verslagen van het programmaprogramma, filtrerend door de datum van het programma.

   Werkt alleen voor programma&#39;s die in het verleden 24 tot 48 uur hebben plaatsgevonden.

2. Leest de media dichte gebeurtenissen van de media dataset, filtrerend door datum en door de weg XDM in de verslagen van het programmaprogramma.

3. Voor elke Media close-gebeurtenis wordt hetzelfde aantal start-gebeurtenissen van het mediaschema gegenereerd als dat er overlappingen waren met de mediasessie.

   Elke gebeurtenis van het media programma begin bevat de naam en de lengte van het programma.

   Ook, bevat nieuwe tijd metrisch genoemd **planningTimePlayed** het aantal seconden dat de media zitting met het geplande programma overlapte. Het tijdstempel van de gebeurtenis start van het schema is de tijdstempel van het moment waarop de show wordt gestart.

4. Schrijft de nieuwe gebeurtenissen van het programmabegin in de media dataset van AEP.

## Vereisten

Voor het uploaden van planningsgegevens van live-inhoud uit het verleden moet uw omgeving voor Streaming media aan de volgende voorwaarden voldoen:

* Het stromen de Inzameling van Media moet voor het volgen op de inhoud worden toegelaten waarvoor u planningsgegevens wilt uploaden, zoals die in [&#x200B; het Volgen overzicht &#x200B;](/help/use-cases/track-av-playback/track-core-overview.md) worden beschreven. <!--specifics??? -->

* Gebruik Streaming Media Collection met Customer Journey Analytics. De mogelijkheid om planningsgegevens te uploaden is niet beschikbaar bij Adobe Analytics.

## Een gegevensset voor een programmaschema maken in AEP

Voordat u de planningsinformatie kunt doorlopen, moet u een gegevensset voor het programmaschema in Experience Platform maken:

1. Creeer een schema dat op de **Media wordt gebaseerd Analytics Geplande klasse van het Programma** XDM.

   ![&#x200B; het Schema van het Programma van het Programma van de Analyse van Media van het Programma &#x200B;](assets/media_schedule_finish_schema_creation.png)

   Dit is de XDM definitie van de Media Analytics Gepland programmaklasse.

   [&#x200B; https://github.com/adobe/xdm/blob/master/components/fieldgroups/tv-schedule/media-analytics-scheduled-program.schema.json](https://github.com/adobe/xdm/blob/master/components/fieldgroups/tv-schedule/media-analytics-scheduled-program.schema.json)

1. Creeer een dataset die op het schema wordt gebaseerd dat u creeerde.

1. Ga met de volgende sectie, [&#x200B; Push programmainformatie &#x200B;](#push-schedule-information) verder.

## Informatie over pushschema

Nadat u [&#x200B; een dataset van het programma &#x200B;](#create-a-program-schedule-dataset-in-aep) creeert, kunt u planningsinformatie duwen:

1. Maak een .json-bestand met de planningsgegevens.

   Het .json dossier moet een serie van de voorwerpen van het Programma van het Programma, in overeenstemming met het XDM schema bevatten.

1. Upload het .json-bestand:

   >[!NOTE]
   >
   >In de cURL-voorbeelden in deze sectie worden de volgende variabelen gebruikt:
   >
   >* Voor verificatie met Adobe Developer:
   >     * CUSTOMER_API_KEY
   >     * AUTH_TOKEN
   >* organisatie-id: CUSTOMER_ORG_ID
   >* dataset id van de recorddataset die in de setup is gemaakt: DATASET_ID
   >* batch-id gemaakt in de eerste aanvraag die wordt gebruikt in de bestandsupload: BATCH_ID
   >* De naam van het bestand dat wordt gebruikt voor pushrecords: FILE_NAME

   1. Maak een nieuwe batch en ontvang de batch-id uit de reactie.

      Bekijk het volgende voorbeeld van het gebruik van cURL voor het maken van een nieuwe AEP-batch:

      ```
          curl -i 'https://platform.adobe.io/data/foundation/import/batches' \
          -X POST \
          -H 'Accept: application/json' \
          -H 'x-api-key: <CUSTOMER_API_KEY>' \
          -H 'x-gw-ims-org-id: <CUSTOMER_ORG_ID>' \
          -H 'Content-Type: application/json' \
          -H 'Authorization: Bearer <OAUTH_TOKEN>' \
          --data-raw '{"datasetId":"<DATASET_ID>","inputFormat":{"format":"json","isMultiLineJson":true},"tags":{"test":["2"]}}'
      
          HTTP/1.1 201 Created
          {
              "id": "BATCH_ID",
              "imsOrg": "CUSTOMER_ORG_ID",
              "updated": 1749838941763,
              "status": "loading",
              "created": 1749838941763,
              "relatedObjects": [
                  {
                      "type": "dataSet",
                      "id": "DATASET_ID"
                  }
              ],
              "version": "1.0.0",
              ............
          }
      ```

   1. Druk op het .json-bestand dat de gegevensrecords van het programma bevat met de batch-id.

      Om planningsinformatie te duwen zou u de partij APIs van AEP moeten gebruiken, zoals die in [&#x200B; wordt beschreven de opname API overzicht van de Partij &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-platform/ingestion/batch/overview).

      Bekijk het volgende voorbeeld van het gebruik van cURL om een bestand met de planningsrecords te duwen:

      ```
          curl -i 'https://platform.adobe.io/data/foundation/import/batches/<BATCH_ID>/datasets/<DATASET_ID>/files/<FILE_NAME>' \
          -X PUT \
          -H 'x-api-key: <CUSTOMER_API_KEY>' \
          -H 'x-gw-ims-org-id: <CUSTOMER_ORG_ID>' \
          -H 'Content-Type: application/json' \
          -H 'Authorization: Bearer <OAUTH_TOKEN>' \
          --upload-file ./schedule_21_05_2025.json`
      ```

   1. Voltooi de batch.

      Bekijk het volgende voorbeeld van het gebruik van cURL om de batch te voltooien:

      ```
          curl -i 'https://platform.adobe.io/data/foundation/import/batches/<BATCH_ID>?action=COMPLETE' \
          -X POST \
          -H 'x-api-key: <CUSTOMER_API_KEY>' \
          -H 'x-gw-ims-org-id: <CUSTOMER_ORG_ID>' \
          -H 'Content-Type: application/json' \
          -H 'Authorization: Bearer <OAUTH_TOKEN>'
      ```

1. Ga met de volgende sectie verder, [&#x200B; Logboek een steunkaartje met de Zorg van de Klant van Adobe &#x200B;](#log-a-support-ticket-with-adobe-customer-care).

## Een ondersteuningsticket aanmelden bij de klantenservice van Adobe

Log een ondersteuningsticket in bij de klantenservice van Adobe met de volgende informatie:

* **dataset van Media**: Specificeer dataset identiteitskaart van de dataset waarvan de gegevens van mediasessies worden gelezen.

* **dataset van het Programma**: Specificeer dataset identiteitskaart van de dataset waaraan de planningsverslagen worden geduwd.

* **de media dataset van de Output**: Specificeer dataset identiteitskaart van de dataset waaraan de gebeurtenissen van het programmabegin worden bewaard.

  Deze dataset ID kan zelfde dataset identiteitskaart zijn die voor de dataset van Media wordt gebruikt. Als het een verschillende dataset identiteitskaart is, zou het nog het zelfde schema XDM zoals de dataset van Media moeten hebben.

* **identiteitskaart van de Organisatie**: Specificeer uw organisatieidentiteitskaart

## Voorbeeld van een schema.json-bestand met twee records

Het volgende voorbeeld is van een programma.json- dossier met twee verslagen. Elk .json dossier zou alle geplande programma&#39;s voor een dag moeten bevatten.

```
   [
        {
            "_id": "any_identifier_as_id_1",
            "customMetadata": [
                {
                    "name": "Sample value",
                    "value": "Sample value"
                }
            ],
            "defaultMetadata": {
                "album": "Sample value",
                "artist": "Sample value",
                "assetID": "Sample value",
                "author": "Sample value",
                "cdn": "Sample value",
                "dayPart": "Sample value",
                "episode": "Sample value",
                "feed": "Sample value",
                "firstAirDate": "Sample value",
                "firstDigitalDate": "Sample value",
                "genreList": [
                    "Sample value"
                ],
                "label": "Sample value",
                "network": "Sample value",
                "originator": "Sample value",
                "publisher": "Sample value",
                "rating": "Sample value",
                "season": "Sample value",
                "show": "Sample value",
                "showType": "Sample value",
                "station": "Sample value",
                "streamFormat": "Sample value"
            },
            "mediaProgramDetails": {
                "length": 1800,
                "name": "Show Name",
                "startTimestamp": "2025-05-01T00:30:00+00:00"
            },
            "scheduleDate": "2025-05-01",
            "scheduleFilter": {
                "filterPath": "xdm.mediaReporting.sessionDetails.channel",
                "filterValue": "Channel Name"
            },
        },
        {
            "_id": "any_identifier_as_id_2",
            "customMetadata": [
                {
                    "name": "Sample value",
                    "value": "Sample value"
                }
            ],
            "defaultMetadata": {
                "album": "Sample value",
                "artist": "Sample value",
                "assetID": "Sample value",
                "author": "Sample value",
                "cdn": "Sample value",
                "dayPart": "Sample value",
                "episode": "Sample value",
                "feed": "Sample value",
                "firstAirDate": "Sample value",
                "firstDigitalDate": "Sample value",
                "genreList": [
                    "Sample value"
                ],
                "label": "Sample value",
                "network": "Sample value",
                "originator": "Sample value",
                "publisher": "Sample value",
                "rating": "Sample value",
                "season": "Sample value",
                "show": "Sample value",
                "showType": "Sample value",
                "station": "Sample value",
                "streamFormat": "Sample value"
            },
            "mediaProgramDetails": {
                "length": 3600,
                "name": "Show Name 2",
                "startTimestamp": "2025-05-01T01:00:00+00:00"
            },
            "scheduleDate": "2025-05-01",
            "scheduleFilter": {
                "filterPath": "xdm.mediaReporting.sessionDetails.channel",
                "filterValue": "Channel Name"
            }
        }
    ]
```

### Inzicht krijgen in de velden voor planningsprogramma&#39;s in het voorbeeld

1. **mediaProgramDetails**: zou de minimuminformatie moeten bevatten die wordt vereist om de gebeurtenis van het programmabegin tot stand te brengen:
   * **startTimestamp**: De tijd toen de show begon.
   * **naam**: De vriendschappelijke naam van de show.
   * **lengte**: Het aantal seconden de show bleef.

     >[!IMPORTANT]
     >
     >Als u meerdere aanvragen voor planningsgegevens hebt, kunnen deze geen overlappende begin- en eindtijd hebben.

1. **planningDate**: De datum waarop de show werd uitgezonden. De notatie moet YYYY-MM-DD zijn. Het wordt gebruikt om de planningsdataset te filtreren en alle programma&#39;s te krijgen waarvoor adobe programma begint.
1. **planningFilter**: Gebruikt om alle media zittingsgebeurtenissen te filtreren.
   * **filterPath**: Een weg XDM aan het gebied dat voor het filtreren wordt gebruikt.
   * **filterValue**: De waarde die voor het filtreren wordt gebruikt.
1. **customMetadata**: De meta-gegevens van de Douane die u aan de gebeurtenissen van het programmabegin wilt toevoegen. Deze meta-gegevens wordt gebruikt om de douanemetagegevens te beschrijven die op de zittingsdichte gebeurtenissen aanwezig zijn.
1. **defaultMetadata**: Een specifieke lijst van afmetingen die de standaardgegevens kunnen toevoegen of overschrijven die op de media sluiten vraag aanwezig zijn.

   Bekijk de volgende voorbeelden van afmetingen die u kunt maken en rapporteren in Customer Journey Analytics:

   * **[&quot;_naam van de Aflevering_&quot;](https://experienceleague.adobe.com/nl/docs/media-analytics/using/implementation/variables/audio-video-parameters#episode)**: Deze dimensie kon u helpen leren welke episodes in een bepaalde reeks best presteren.

   * **[identiteitskaart van Activa &#x200B;](https://experienceleague.adobe.com/nl/docs/media-analytics/using/implementation/variables/audio-video-parameters#asset-id)**

1. Ga met [&#x200B; verder analyseren gegevens in Customer Journey Analytics &#x200B;](#analyze-data-in-customer-journey-analytics).

## Gegevens analyseren in Customer Journey Analytics

Binnen één dag van het uploaden van uw gegevensdossier zoals die in [&#x200B; wordt beschreven Verzoek en upload het dossier van planningsgegevens &#x200B;](#request-and-upload-the-schedule-data-file), zijn uw gegevens klaar om in Customer Journey Analytics te rapporteren.

Rapporten over uw oude live streaming mediagegevens in Customer Journey Analytics:

1. Maak een nieuw project of open een bestaand project.

1. Ontwerp het project door tabellen of visualisaties te maken die u nodig hebt voor het analyseren van uw eerdere live streaming mediagegevens.

   Gebruik bij het uitbouwen van het project de informatie die u in het bestand met planningsgegevens hebt opgenomen en naar de klantenservice van Adobe hebt verzonden. Hieronder vallen de overeenkomende sleutel, afmetingen en eventuele aanvullende metagegevens. Voor meer informatie, zie [&#x200B; Verzoek en upload het dossier van planningsgegevens &#x200B;](#request-and-upload-the-schedule-data-file).




<!-- 

Extra

Things they need to upload:
Everything on that slide + other metadata
You can't overlap 2 schedules.
You can build a journey in AJO for the people who watch Mike, Mike, and Mike. e.g. 
This is recurring.
Available to all SKUs? "Increases cost for updated data by 22%, but included in the new higher tier Streaming Media SKU."

You can now upload schedule data of past live content to more easily and accurately track viewership. Live content includes content from FAST (Free Ad Supported TV) platforms or local streams.
You can track which programs a person viewed in a given session, or even which topics or program segments they viewed. These capabilities are available regardless of how you implemented Streaming Media Collection.
Previously, it was difficult to accurately tie a given session to specific programs when analyzing live content, and it wasn't possible to tie a given session to individual topics or program segments.
Schedule data uploads of live content in Streaming Media Collection includes the following capabilities:
Upload schedules for past live content, regardless of your Streaming Media Collection implementation.
Identify the start and end times of each individual program in the live stream for the period of time that you want to analyze. With accurate start and end times, the precise running time is accurately reflected and can be analyzed against each viewer session.
For example, precise beginning and end times are not always known for a live sporting event until the event is over. Schedule data uploads allow you to get accurate reporting by updating the start and end times after the program finishes.
Create new time-based dimensions for specific topics or program segments (time slots) within a given program. These time-based dimensions allow you to analyze viewership of a program at a more specific level, helping to gather insights about which topics or program segments resonated best.
For example, when analyzing a live sporting event, such as a soccer match, you can create separate dimensions for the first half, half time, and second half. This allows for more detailed breakdowns of viewer behavior for specific segments of a program.
These capabilities allow you to:
Analyze show viewership to understand performance.
Target users based on program viewership.
Analyze viewership based on metadata like topic, sports league, sponsorship, and so forth.
Target based on metadata viewership.
Correct media metrics for show dimensions of live sports/events for easier analysis at scale.
Increased ease of use for live sports

-->
