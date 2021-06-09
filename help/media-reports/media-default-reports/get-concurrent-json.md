---
title: JSON-rapportgegevens voor gelijktijdige viewers ophalen
description: JSON-rapportgegevens voor gelijktijdige viewers ophalen
uuid: 9168f114-2459-4951-a06c-57b735d09dc0
source-git-commit: 0d5edcae0a80357247ada7f61daece9840d5c4b5
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 4%

---


# Hiermee worden JSON-rapportgegevens voor gelijktijdige viewers opgehaald{#get-concurrent-viewers-json-report-data}

U kunt de gegevens van het gelijktijdig kijkersrapport verkrijgen gebruikend _*1.4 versie*_ van Analytics APIs:
* [API&#39;s voor Analytics](https://github.com/AdobeDocs/analytics-1.4-apis)
* [Swagger](https://adobedocs.github.io/analytics-1.4-apis/swagger-docs.html#/Report/Report.Get)

1. Filter de gegevens gebruikend om het even welk segment dat op UI bouwde. Maak een nieuw segment om te filteren op een specifieke inhoud-id.
1. Stel de `elements` -> `id` in de hoofdtekst van de aanvraag in op `videoconcurrentviewers`.
1. Een voldoende hoeveelheid gegevens aanvragen. Adobe raadt 3200 gegevenspunten aan om ervoor te zorgen dat de gegevens geen leemten bevatten.

   * Het gegevensbereik dat u in het rapport opgeeft, verzamelt alle gelijktijdige viewergegevens _op het moment dat de videosessie werd beëindigd._
U moet dus rekening houden met sessies die op een dag beginnen en na middernacht eindigen (dus de volgende dag).

   * Vraag meer dan één dag gegevens aan, maar gebruik in uw analyse _*slechts de eerste dag van de gegevens.*_

Een lading van het steekproefverzoek voor dit scenario zou als dit kijken:

```
{
  "reportDescription":{
    "reportSuiteID":"[YOUR_RSID]",
    "dateFrom":"2018-07-01",
    "dateTo":"2018-07-02",
    "metrics":[
      {
        "id":"instances"
      }
    ],
    "elements":[
      {
        "id":"videoconcurrentviewers",
        "top":"3200"
      }
    ],
    "segments":[
      {
        "id":"s1234_58ca4fc7e4b0abc238707bb9"                                         
      }
    ],
    "sortBy":"instances",
    "locale":"en_US"
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

        * `reportSuiteID` - For info on reports suites: [Report Suites](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/report-suites-admin.html)
        
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
