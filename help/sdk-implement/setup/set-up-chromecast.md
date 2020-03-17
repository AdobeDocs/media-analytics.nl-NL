---
title: Chromecast instellen
description: De toepassingsopstelling van SDK van media voor implementatie op Chromecast.
uuid: d664e394-02a2-4985-bbad-be1bcc44fb2b
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Chromecast instellen{#set-up-chromecast}

## Veelgestelde vragen

_Moet ik de Chromecast JavaScript SDK gebruiken of kan ik de Standaard JavaScript SDK gebruiken?_

Het juiste antwoord is &quot;Chromecast&quot;, om de volgende redenen:
* De API-bibliotheken van AppMeasurement en Visitor in de standaard JS SDK zijn niet gecertificeerd voor gebruik op OTT-platforms. In Chromecast JS SDK, zijn de Video Heartbeats Bibliotheek (VHL), Analytics, en VisitorAPI allen ingebouwde aan enige, verenigde, verklaarde-voor-Chromecast SDK.
* De Chromecast SDK is veel lichter dan de standaard JS SDK. Dit is zeer essentieel voor de onderste-eindhardware die door OTT platforms wordt gebruikt.

## Vereisten

* **Verkrijg geldige configuratieparameters voor Heartbeats**. Deze parameters kunnen bij een vertegenwoordiger van Adobe worden verkregen nadat u uw account voor mediaanalyse hebt ingesteld.
* **Biedt de volgende mogelijkheden in uw mediaspeler:**
   * *Een API die zich moet abonneren op spelergebeurtenissen* - De Media SDK vereist dat u een set eenvoudige API&#39;s aanroept wanneer gebeurtenissen in de speler plaatsvinden.
   * *Een API die spelerinformatie* verschaft - Deze informatie bevat details zoals de medianaam en de positie van de afspeelkop.

Adobe Mobile-services biedt een nieuwe gebruikersinterface waarin mobiele marketingmogelijkheden voor mobiele toepassingen vanuit de volledige Adobe Marketing Cloud worden samengebracht. In eerste instantie biedt de Mobile-service naadloze integratie van toepassingsanalyses en doelgerichte functies voor de Adobe Analytics- en Adobe Target-oplossingen. Meer informatie vindt u in de documentatie van [Adobe Mobile Services.](https://marketing.adobe.com/resources/help/en_US/mobile/)

Met Chromecast SDK 2.x for Experience Cloud Solutions kunt u Chromecast-toepassingen die in JavaScript zijn geschreven, gebruiken en gegevens van het publiek verzamelen via publieksbeheer en de betrokkenheid van video&#39;s meten via videohartslagen.

## SDK-implementatie

1. Voeg uw [gedownloade](/help/sdk-implement/download-sdks.md#download-2x-sdks) Chromecast-bibliotheek toe aan uw project.

   1. Het `AdobeMobileLibrary-Chromecast-[version]` ZIP-bestand bestaat uit de volgende softwarecomponenten:

      * `adbmobile-chromecast.min.js`:

         Dit bibliotheekbestand wordt opgenomen in de bronmap van de Chromecast-app.

      * `ADBMobileConfig` config

         Dit SDK-configuratiebestand is aangepast voor uw app. De SDK beschikt over een voorbeeldimplementatie (onder `ADBMobileConfig` `samples/`). Verkrijg de juiste montages van een vertegenwoordiger van Adobe.
   1. Voeg het bibliotheekbestand toe aan uw `index.html` bestand en maak de `ADBMobileConfig` algemene variabele als volgt (de algemene variabele die wordt gebruikt om Adobe Mobile voor hartslagen te configureren, heeft een exclusieve sleutel met de naam `mediaHeartbeat`):

      ```js
      <script> 
          var ADBMobileConfig = { 
            "marketingCloud": { 
              "org": "972C898555E9F7BC7F000101@AdobeOrg" 
            }, 
            "target": { 
              "clientCode": "", 
              "timeout": 5 
            }, 
            "audienceManager": { 
              "server": "obumobile5.demdex.net" 
            }, 
            "analytics": { 
              "rsids": "mobile5vhl.sample.player", 
              "server": "obumobile5.sc.omtrdc.net", 
              "ssl": false, 
              "offlineEnabled": false, 
              "charset": "UTF-8", 
              "lifecycleTimeout": 300, 
              "privacyDefault": "optedin", 
              "batchLimit": 0, 
              "timezone": "MDT", 
              "timezoneOffset": -360, 
              "referrerTimeout": 0, 
              "poi": [] 
            }, 
            "mediaHeartbeat": { 
              "server": "obumobile5.hb.omtrdc.net", 
              "publisher": "972C898555E9F7BC7F000101@AdobeOrg", 
              "channel": "test-channel-chromecast", 
              "ssl": false, 
              "ovp": "chromecast-player", 
              "sdkVersion": "chromecast-sdk", 
              "playerName": "Chromecast" 
            } 
          }; 
        </script> 
      <script type="text/javascript" src="script/lib/adbmobile-chromecast.min.js"></script>
      ```

      >[!IMPORTANT]
      >
      >Als `mediaHeartbeat` verkeerd wordt gevormd, gaat de media module (VHL) een foutenstaat in en zal ophouden verzendend volgende vraag.

      ADBMobile Config-parameters voor de MediaHeartbeat-sleutel:
   | Configuratieparameter | Beschrijving |
   | --- | --- |
   | `server` | Tekenreeks die de URL van het volgende eindpunt op de achtergrond vertegenwoordigt. |
   | `publisher` | Tekenreeks die de unieke id van de uitgever van de inhoud vertegenwoordigt. |
   | `channel` | Tekenreeks die de naam van het distributiekanaal van de inhoud vertegenwoordigt. |
   | `ssl` | Booleaanse waarde die aangeeft of SSL moet worden gebruikt voor het bijhouden van aanroepen. |
   | `ovp` | Tekenreeks die de naam van de videospelerprovider vertegenwoordigt. |
   | `sdkversion` | Tekenreeks die de huidige versie van de app/SDK vertegenwoordigt. |
   | `playerName` | Tekenreeks die de naam van de speler vertegenwoordigt. |


1. Geniet-id voor Experience Cloud Visitor configureren.

   De Experience Cloud Visitor ID-service biedt een universele bezoeker-id voor alle Experience Cloud-oplossingen. De service voor bezoekers-id is vereist voor Video-hartslag en andere integraties in de marketingcloud.

   Verifieer dat uw `ADBMobileConfig` config uw `marketingCloud` organisatieID bevat.

   ```js
   "marketingCloud": { 
       "org": YOUR-MCORG-ID" 
   }
   ```

   Ervaar de organisatie-id&#39;s van de cloud die uniek zijn voor elk clientbedrijf in de Adobe Marketing Cloud en die er ongeveer als volgt uitzien: `016D5C175213CCA80A490D05@AdobeOrg`.

   >[!IMPORTANT]
   >
   >Zorg ervoor dat u dit ook doet `@AdobeOrg`.

   Nadat de configuratie is voltooid, wordt een Experience Cloud Visitor-id gegenereerd en opgenomen in alle hits. Andere bezoeker-id&#39;s, zoals `custom` en `automatically-generated`, worden bij elke treffer verzonden.

   **Ervaar de Methoden van de Dienst van de Bezoeker van de Wolk**

   >[!TIP]
   >
   >De methoden Experience Cloud Visitor ID zijn vooraf ingesteld op `visitor`.

   | Methode | Beschrijving |
   | --- | --- |
   | `getMarketingCloudID()` | Haalt de Experience Cloud Visitor ID op van de Bezoeker ID-service.  <br/><br/>`ADBMobile.visitor.getMarketingCloudID();` |
   | `syncIdentifiers()` | Met de Experience Cloud Visitor-id kunt u aanvullende klant-id&#39;s instellen die aan elke bezoeker kunnen worden gekoppeld. De bezoeker-API accepteert meerdere klant-id&#39;s voor dezelfde bezoeker en een id voor het klanttype om het bereik van de verschillende klant-id&#39;s te scheiden. Deze methode komt overeen met `setCustomerIDs()` in de JavaScript-bibliotheek.  Bijvoorbeeld: <br/><br/>`var identifiers = {};` <br/><br/>`identifiers["idType"] = "idValue";` <br/><br/>`ADBMobile.visitor.syncIdentifiers(identifiers);` |


<!--   **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://marketing.adobe.com/resources/help/en_US/mobile/signals_.html) -->

