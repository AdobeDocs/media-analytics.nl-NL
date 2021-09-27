---
title: Hoe te opstelling SDK van Media voor Roku
description: Voer de volgende stappen uit om de Media SDK-toepassing in te stellen op Roku.
uuid: 904dfda0-4782-41da-b4ab-212e81156633
exl-id: b8de88d0-3a93-4776-b372-736bf979ee26
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: e10f705e135cc6b9c630059596994d12fc787866
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 2%

---

# Roku instellen{#set-up-roku}

## Vereisten

* **Verkrijg geldige configuratieparameters voor**
HeartbeatsDeze parameters kunnen bij een vertegenwoordiger van Adobe worden verkregen nadat u uw media analytics-account hebt ingesteld.
* **Biedt de volgende mogelijkheden in uw mediaspeler:**
   * _Een API die zich moet abonneren op spelergebeurtenissen_ . De Media SDK vereist dat u een set eenvoudige API&#39;s aanroept wanneer gebeurtenissen in de speler plaatsvinden.
   * _Een API die spelerinformatie_  verschaft. Deze informatie bevat details zoals de medianaam en de positie van de afspeelkop.

Adobe Mobile-services bieden een nieuwe gebruikersinterface waarin mobiele marketingmogelijkheden voor mobiele toepassingen uit de hele Adobe Marketing Cloud worden samengebracht. Aanvankelijk biedt de Mobile-service een naadloze integratie van analysemogelijkheden voor apps en doelgerichte functionaliteit voor de Adobe Analytics- en Adobe Target-oplossingen.

Meer informatie vindt u in de [Adobe Mobile Services-documentatie.](https://experienceleague.adobe.com/docs/mobile-services/using/home.html)

Met Roku SDK 2.x voor Experience Cloud Solutions kunt u Roku-toepassingen meten die in BrightScript zijn geschreven, gegevens voor het publiek verzamelen en benutten via publieksbeheer en de videobetrokkenheid meten via videohartslagen.

## SDK-implementatie

1. Voeg uw [gedownloade ](/help/sdk-implement/download-sdks.md#download-2x-sdks) bibliotheek van Roku aan uw project toe.

   1. Het `AdobeMobileLibrary-2.*-Roku.zip`-downloadbestand bestaat uit de volgende softwarecomponenten:

      * `adbmobile.brs`: Dit bibliotheekbestand wordt opgenomen in de bronmap van de Roku-app.

      * `ADBMobileConfig.json`: Dit SDK-configuratiebestand is aangepast voor uw app.
   1. Voeg het bibliotheekbestand en het JSON-configuratiebestand toe aan uw projectbron.

      JSON die wordt gebruikt om Adobe Mobile te vormen heeft een exclusieve sleutel voor media hartslagen genoemd `mediaHeartbeat`. Dit is waar de configuratieparameters voor de media hartslagen horen.

      >[!TIP]
      >
      >Het pakket bevat een voorbeeld van het JSON-bestand `ADBMobileConfig`. Neem voor de instellingen contact op met de Adobe-vertegenwoordigers.

      Bijvoorbeeld:

      ```
      {
        "version":"1.0",
        "analytics":{
          "rsids":"",
          "server":"",
          "charset":"UTF-8",
          "ssl":true,
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
         "ssl":true,
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


1. Experience Cloud-bezoeker-id configureren.

   De dienst van identiteitskaart van de Bezoeker van Experience Cloud verstrekt universele Bezoeker identiteitskaart over de oplossingen van Experience Cloud. De service voor bezoekers-id is vereist voor Video-hartslag en andere Marketing Cloud-integratie.

   Verifieer dat uw `ADBMobileConfig` config uw `marketingCloud` organisatie ID bevat.

   ```
   "marketingCloud": {
       "org": YOUR-MCORG-ID"
   }
   ```

   De organisatie-id&#39;s van Experience Cloud identificeren uniek elk clientbedrijf in de Adobe Marketing Cloud en lijken ongeveer op de volgende waarde te lijken: `016D5C175213CCA80A490D05@AdobeOrg`.

   >[!IMPORTANT]
   >
   >Zorg ervoor dat u `@AdobeOrg` opneemt.

   Nadat de configuratie volledig is, wordt een identiteitskaart van de Bezoeker van de Experience Cloud geproduceerd en inbegrepen op alle treffers. Andere bezoeker-id&#39;s, zoals `custom` en `automatically-generated`, worden nog steeds bij elke treffer verzonden.

   **Service-methoden voor Experience Cloud-bezoeker-id**

   >[!TIP]
   >
   >De methodes van identiteitskaart van de Bezoeker van Experience Cloud worden vooraf bepaald met `visitor`.

   |  Methode   | Beschrijving |
   | --- | --- |
   | `visitorMarketingCloudID` | Haalt de Experience Cloud-bezoeker-id op van de bezoeker-id-service.  <br/><br/>`ADBMobile().visitorMarketingCloudID()` |
   | `visitorSyncIdentifiers` | Met de Experience Cloud-bezoeker-id kunt u aanvullende klant-id&#39;s instellen die aan elke bezoeker kunnen worden gekoppeld. De bezoeker-API accepteert meerdere klant-id&#39;s voor dezelfde bezoeker en een id voor het klanttype om het bereik van de verschillende klant-id&#39;s te scheiden. Deze methode komt overeen met `setCustomerIDs`. Bijvoorbeeld: <br/><br/>`identifiers={}` <br/>`identifiers["idType"]="idValue"` <br/>`ADBMobile().visitorSyncIdentifiers(identifiers)` |
   | `setAdvertisingIdentifier` | Wordt gebruikt om de Roku-id voor advertentie (RIDA) in te stellen op de SDK. Bijvoorbeeld: <br/><br/> `ADBMobile().setAdvertisingIdentifier(`<br/>  `"<sample_roku_identifier_for_advertising>")` <br/><br/><br/>Haal de Roku-id voor advertentie (RIDA) op met de Roku SDK  [getRIDA()](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic) API. |
   | `getAllIdentifiers` | Retourneert een lijst met alle id&#39;s die door de SDK zijn opgeslagen, inclusief Analytics, Visitor, Audience Manager en aangepaste id&#39;s. <br/><br/> `identifiers = ADBMobile().getAllIdentifiers()` |
   <!--
    Roku Api Reference:
    * [Integrating the Roku Advertising Framework](https://sdkdocs.roku.com/display/sdkdoc/Integrating+the+Roku+Advertising+Framework)  
    * [GetRIDA()](https://sdkdocs.roku.com/display/sdkdoc/ifDeviceInfo#ifDeviceInfo-GetRIDA())
    -->

   <br/><br/>

   **Aanvullende openbare API&#39;s**

   **DebugLogging**
| Methode   | Beschrijving | | — | — | |  `setDebugLogging` | Gebruikt om zuivert het registreren voor SDK toe te laten of onbruikbaar te maken.  <br/><br/>`ADBMobile().setDebugLogging(true)` | |  `getDebugLogging` | Retourneert true als de logboekregistratie voor foutopsporing is ingeschakeld.   <br/><br/>`isDebugLoggingEnabled = ADBMobile().getDebugLogging()` |

   <br/><br/>

   **PrivacyStatus**
| Constant   | Beschrijving | | — | — | |  `PRIVACY_STATUS_OPT_IN` | Constante die moet worden doorgegeven terwijl setPrivacyStatus wordt aangeroepen om aan te melden. <br/><br/>`optInString = ADBMobile().PRIVACY_STATUS_OPT_IN`| |  `PRIVACY_STATUS_OPT_OUT` | Constante die moet worden doorgegeven terwijl setPrivacyStatus wordt aangeroepen om te weigeren.  <br/><br/>`optOutString = ADBMobile().PRIVACY_STATUS_OPT_OUT`|

   <br/>

   |  Methode   | Beschrijving |
   | --- | --- |
   | `setPrivacyStatus` | Hiermee stelt u de privacystatus van de SDK in.  <br/><br/>`ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)` |
   | `getPrivacyStatus` | Haalt de huidige privacystatus op die is ingesteld op de SDK.  <br/><br/>`privacyStatus = ADBMobile().getPrivacyStatus()` |

   <br/><br/>
   >[!IMPORTANT]
   >
   >Zorg ervoor dat u `processMessages` en `processMediaMessages` functie in de belangrijkste gebeurtenislijn om de 250 ms roept om ervoor te zorgen dat SDK correct pingelt verzendt.

   |  Methode   | Beschrijving |
   | --- | --- |
   | `processMessages` | Verantwoordelijk om de gebeurtenissen van de Analytics tot SDK over te gaan die moeten worden behandeld.  <br/><br/>`ADBMobile().processMessages()` |
   | `processMediaMessages` | Verantwoordelijk om de gebeurtenissen van Media tot SDK over te gaan die moeten worden behandeld. <br/><br/>`ADBMobile().processMediaMessages()` |


<!--    **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://experienceleague.adobe.com/docs/mobile-services/using/manage-app-settings-ug/configuring-app/signals.html) -->
