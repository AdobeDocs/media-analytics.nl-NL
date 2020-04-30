---
title: Roku instellen
description: Installatie van de Media SDK-toepassing voor implementatie op Roku.
uuid: 904dfda0-4782-41da-b4ab-212e81156633
translation-type: tm+mt
source-git-commit: ccdc3e170d125a76d798be7ce1fa5c12eef1f76a

---


# Roku instellen{#set-up-roku}

## Vereisten

* **Verkrijg geldige configuratieparameters voor Heartbeats**. Deze parameters kunnen bij een vertegenwoordiger van Adobe worden verkregen nadat u uw account voor mediaanalyse hebt ingesteld.
* **Biedt de volgende mogelijkheden in uw mediaspeler:**
   * _Een API die zich moet abonneren op spelergebeurtenissen_ - De Media SDK vereist dat u een set eenvoudige API&#39;s aanroept wanneer gebeurtenissen in de speler plaatsvinden.
   * _Een API die spelerinformatie_ verschaft - Deze informatie bevat details zoals de medianaam en de positie van de afspeelkop.

Adobe Mobile-services biedt een nieuwe gebruikersinterface waarin mobiele marketingmogelijkheden voor mobiele toepassingen vanuit de volledige Adobe Marketing Cloud worden samengebracht. In eerste instantie biedt de Mobile-service naadloze integratie van toepassingsanalyses en doelgerichte functies voor de Adobe Analytics- en Adobe Target-oplossingen.

Meer informatie vindt u in de documentatie van [Adobe Mobile Services.](https://docs.adobe.com/content/help/en/mobile-services/using/home.html)

Met Roku SDK 2.x for Experience Cloud Solutions kunt u Roku-toepassingen die in BrightScript zijn geschreven, gebruiken en gegevens van het publiek verzamelen via publieksbeheer en de videobetrokkenheid meten via videohartslagen.

## SDK-implementatie

1. Voeg uw [gedownloade](/help/sdk-implement/download-sdks.md#download-2x-sdks) bibliotheek van Roku aan uw project toe.

   1. Het `AdobeMobileLibrary-2.*-Roku.zip` downloadbestand bestaat uit de volgende softwarecomponenten:

      * `adbmobile.brs`: Dit bibliotheekbestand wordt opgenomen in de bronmap van de Roku-app.

      * `ADBMobileConfig.json`: Dit SDK-configuratiebestand is aangepast voor uw app.
   1. Voeg het bibliotheekbestand en het JSON-configuratiebestand toe aan uw projectbron.

      De JSON die wordt gebruikt om Adobe Mobile te configureren, heeft een exclusieve sleutel voor mediagelettertypen `mediaHeartbeat`. Dit is waar de configuratieparameters voor media hartslagen horen.

      >[!TIP]
      >
      >Het pakket bevat een voorbeeld van een JSON- `ADBMobileConfig` bestand. Neem voor de instellingen contact op met uw Adobe-vertegenwoordigers.

      Bijvoorbeeld:

      ```
      {
        "version":"1.0", 
        "analytics":{
          "rsids":"",
          "server":"",
          "charset":"UTF-8", 
          "ssl":false, 
          "offlineEnabled":false, 
          "lifecycleTimeout":30, 
          "batchLimit":50, 
          "privacyDefault":"optedin", 
          "poi":[ ]
      },
      "marketingCloud":{
        "org":""
      },
      "target":{ 
        "clientCode":"", 
        "timeout":5
      },
      "audienceManager":{ 
        "server":""
      },
      "acquisition":{ 
        "server":"example.com",
        "appid":"sample-app-id"
      },
      
      "mediaHeartbeat":{ 
         "server":"example.com", 
         "publisher":"sample-publisher", 
         "channel":"sample-channel", 
         "ssl":false,
         "ovp":"sample-ovp", 
         "sdkVersion":"sample-sdk", 
         "playerName":"roku"
         }    
      }
      ```

      | Configuratieparameter | Beschrijving     |
      | --- | --- |
      | `server` | Tekenreeks die de URL van het volgende eindpunt op de achtergrond vertegenwoordigt. |
      | `publisher` | Tekenreeks die de unieke id van de uitgever van de inhoud vertegenwoordigt. |
      | `channel` | Tekenreeks die de naam van het distributiekanaal van de inhoud vertegenwoordigt. |
      | `ssl` | Booleaanse waarde die aangeeft of SSL moet worden gebruikt voor het bijhouden van aanroepen. |
      | `ovp` | Tekenreeks die de naam van de videospelerprovider vertegenwoordigt. |
      | `sdkversion` | Tekenreeks die de huidige versie van de app/SDK vertegenwoordigt. |
      | `playerName` | Tekenreeks die de naam van de speler vertegenwoordigt. |

      >[!IMPORTANT]
      >
      >Als `mediaHeartbeat` verkeerd wordt gevormd, gaat de media module (VHL) een foutenstaat in en zal ophouden verzendend volgende vraag.


1. Geniet-id voor Experience Cloud Visitor configureren.

   De Experience Cloud Visitor ID-service biedt een universele bezoeker-id voor alle Experience Cloud-oplossingen. De service voor bezoekers-id is vereist voor Video-hartslag en andere integraties in de marketingcloud.

   Verifieer dat uw `ADBMobileConfig` config uw `marketingCloud` organisatieID bevat.

   ```
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

   |  Methode   | Beschrijving |
   | --- | --- |
   | `visitorMarketingCloudID` | Haalt de Experience Cloud-bezoekersidentiteitskaart op van de bezoekersidentiteitsservice.  <br/><br/>`ADBMobile().visitorMarketingCloudID()` |
   | `visitorSyncIdentifiers` | Met de Experience Cloud Visitor-id kunt u aanvullende klant-id&#39;s instellen die aan elke bezoeker kunnen worden gekoppeld. De bezoeker-API accepteert meerdere klant-id&#39;s voor dezelfde bezoeker en een id voor het klanttype om het bereik van de verschillende klant-id&#39;s te scheiden. Deze methode komt overeen met `setCustomerIDs`. Bijvoorbeeld: <br/><br/>`identifiers={}` <br/>`identifiers["idType"]="idValue"` <br/>`ADBMobile().visitorSyncIdentifiers(identifiers)` |
   | `setAdvertisingIdentifier` | Wordt gebruikt om de Roku-id voor advertentie (RIDA) in te stellen op de SDK. Bijvoorbeeld: <br/><br/> `ADBMobile().setAdvertisingIdentifier(`<br/>  `"<sample_roku_identifier_for_advertising>")` <br/><br/><br/>Haal de Roku-id voor advertentie (RIDA) op met de Roku SDK [getRIDA()](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic) -API. |

   <!--
    Roku Api Reference: 
    * [Integrating the Roku Advertising Framework](https://sdkdocs.roku.com/display/sdkdoc/Integrating+the+Roku+Advertising+Framework)  
    * [GetRIDA()](https://sdkdocs.roku.com/display/sdkdoc/ifDeviceInfo#ifDeviceInfo-GetRIDA())
    -->

<!--    **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://docs.adobe.com/content/help/en/mobile-services/using/manage-app-settings-ug/configuring-app/signals.html) -->
