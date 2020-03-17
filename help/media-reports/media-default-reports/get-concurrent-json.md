---
title: JSON-rapportgegevens voor gelijktijdige viewers ophalen
description: null
uuid: 9168f114-2459-4951-a06c-57b735d09dc0
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# JSON-rapportgegevens voor gelijktijdige viewers ophalen{#get-concurrent-viewers-json-report-data}

U kunt de rapportgegevens van gelijktijdige viewers ophalen met versie _**_ 1.4 van de API&#39;s voor analyse:
* [Analyse-API&#39;s](https://github.com/AdobeDocs/analytics-1.4-apis)
* [Swagger](https://adobedocs.github.io/analytics-1.4-apis/swagger-docs.html#/Report/Report.Get)

1. Filter de gegevens gebruikend om het even welk segment dat op UI bouwde. Maak een nieuw segment om te filteren op een specifieke inhoud-id.
1. Stel de optie `elements` -> `id` in de aanvraaginstantie in op `videoconcurrentviewers`.
1. Een voldoende hoeveelheid gegevens aanvragen. Adobe raadt 3200 gegevenspunten aan om ervoor te zorgen dat de gegevens geen hiaten bevatten.

   * Het gegevensbereik dat u in het rapport opgeeft, verzamelt alle gelijktijdige viewergegevens _op het moment dat de videosessie werd beëindigd._
U moet dus rekening houden met sessies die op een dag beginnen en na middernacht eindigen (dus de volgende dag).

   * Vraag meer dan één dag gegevens aan, maar _*gebruik in uw analyse slechts de eerste dag van de gegevens.*_

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

1. Navigate to: [https://marketing.adobe.com/developer/api-explorer.](https://marketing.adobe.com/developer/api-explorer)
1. Select and enter the following information in the API Explorer form:

    * **API -** Select "Report".
    * **Method -** Select "Queue".
    * **Environment -** Select your data center.
    * Request JSON - Specify the following:

        * `reportSuiteID` - For info on reports suites: [Report Suites](https://marketing.adobe.com/resources/help/en_US/sc/implement/ref-reports-report-suites.html)
        
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
