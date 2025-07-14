---
title: Gelijktijdige gebruikers JSON-rapportgegevens ophalen met API's van Analytics 2.0
description: Leer hoe u gelijktijdige viewers rapportgegevens verkrijgt met de API's Analytics 2.0. Bekijk een voorbeeldverzoek en een antwoord.
uuid: 9168f114-2459-4951-a06c-57b735d09dc0
exl-id: f84f63d3-b0d0-45fe-95a7-159f22d60660
feature: "Streaming Media, Workspace Basics"
role: User, Admin, Data Engineer
source-git-commit: 67f1fa8194fa58b2c513e3136d2bc7880f9cb06b
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---


# Gelijktijdige gebruikers JSON-rapportgegevens ophalen met API&#39;s van Analytics 2.0{#get-concurrent-viewers-json-report-data}

U kunt gezamenlijke kijkers rapportgegevens verkrijgen gebruikend [_*Analytics 2.0 APIs*_ ](https://www.adobe.io/apis/experiencecloud/analytics/docs.html).

1. Filter de gegevens gebruikend om het even welk segment dat op UI wordt voortgebouwd. Maak een nieuw segment om te filteren op een specifieke inhoud-id.
1. Stel `elements` -> `id` in de hoofdtekst van de aanvraag in op `metrics/concurrent_viewers_visitors` .
1. Een voldoende hoeveelheid gegevens aanvragen.

   * De gegevenswaaier u in het rapport specificeert verzamelt alle gezamenlijke kijkersgegevens _op het tijdstip dat de videozitting beëindigde._
U moet uw account opgeven voor sessies die op een dag beginnen en eindigen na middernacht, de volgende dag.

   * Vraag één meer dag van gegevens aan uw voorgenomen periode in uw verzoek, maar in uw analyse _*gebruik slechts de voorgenomen gegevens.*_

Een lading van het steekproefverzoek voor één dag van gegevens zou als het volgende voorbeeld kijken. Het verzoek wordt gedurende twee opeenvolgende dagen uitgevoerd, maar in de rapportage wordt u alleen de eerste dag gebruikt.

## Voorbeeldverzoek

```json
{
    "rsid": "[YOUR_RSID]",
    "locale": "en_US",
    "dimension": "variables/daterangeminute",
    "globalFilters": [
        {
            "dateRange": "2020-09-02T00:00/2020-09-03T00:00",
            "type": "dateRange"
        }
    ],
    "metricContainer": {
        "metrics": [
            {
                "columnId": "column1",
                "id": "metrics/concurrent_viewers_visitors"
            }
        ]
    },
    "settings": {
        "dimensionSort": "asc",
        "limit": "2000",
        "page": 0
  }
}
```

## Samplereactie

```JSON
{
   "totalPages":1,
   "firstPage":true,
   "lastPage":true,
   "numberOfElements":1440,
   "number":0,
   "totalElements":1440,
   "columns":{
      "dimension":{
         "id":"variables/daterangeminute",
         "type":"time"
      },
      "columnIds":[
         "column1"
      ]
   },
   "rows":[
      {
         "itemId":"12008020000",
         "value":"00:00 2020-09-02",
         "data":[
            123.0
         ]
      },
      {
         "itemId":"12008020001",
         "value":"00:01 2020-09-02",
         "data":[
            143.0
         ]
      },
      {
         "itemId":"12008020002",
         "value":"00:02 2020-09-02",
         "data":[
            167.0
         ]
      },

      ...
      {
         "itemId":"12008022359",
         "value":"23:59 2020-09-02",
         "data":[
            768.0
         ]
      }
   ],
   "summaryData":{
      "filteredTotals":[
         17124.0
      ],
      "totals":[
         18453.0
      ]
   }
}
```


<!--
You can extract the concurrent viewers report data using the Experience Cloud API Explorer as follows.

1. Navigate to: [https://www.adobe.io.](https://www.adobe.io)
1. Select and enter the following information in the API Explorer form:

    * **API -** Select "Report".
    * **Method -** Select "Queue".
    * **Environment -** Select your data center.
    * Request JSON - Specify the following:

        * `reportSuiteID` - For info on reports suites: [Report Suites](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/report-suites-admin.html?lang=nl-NL)

        * `dateTo` - End date of the report.         

          >[!NOTE]
          >
          >The maximum time period supported is two days.

        * `dateFrom` - Start date of the report.
        * `elements : id` - Set to `"videoconcurrentviewers"`

        * `elements : top` - Specify the number of entries to be returned.

      Sample request body:

      ```    
      {
          "reportDescription": {
              "reportSuiteID": "[Your Report Suite ID]",
              "dateTo": "2017-09-07",
              "dateFrom": "2017-09-07"
              "metrics": [
                  {
                      "id": "instances"
                  }
              ],
              "elements": [
                  {
                      "id": "videoconcurrentviewers",
                      "top": 2880
                  }
              ]
              "locale": "en_US"
          }
      }

      ```

      >[!TIP]
      >
      >Some sessions are ended on the next day, and at that point the data will be available for reporting. In that case the best approach is to select 2 days (2880 minutes) of data, and use only the data for the first day (1440 minutes).

1. Click **Get Response**.

   In the Response field, you should get a `reportID`.
1. In the form, change **Method** to "Get".
1. Enter the value of the `reportID` you received in Step 3, and click **Get Response**.

   The concurrent viewers report data, in JSON format, is presented in the Response field.

   For example:

   ![](assets/api_helper_2.png)

   ![](assets/api_helper_1.png)

-->
