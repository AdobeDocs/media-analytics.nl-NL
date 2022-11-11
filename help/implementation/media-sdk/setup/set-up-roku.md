---
title: Hoe te opstelling SDK van Media voor Roku
description: Voer de volgende stappen uit om de Media SDK-toepassing in te stellen op Roku.
uuid: 904dfda0-4782-41da-b4ab-212e81156633
exl-id: b8de88d0-3a93-4776-b372-736bf979ee26
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 1%

---

# Mobiele SDK v2.x instellen voor Roku {#set-up-roku}

## Vereisten {#roku-prerequisites}

* **Geldige configuratieparameters verkrijgen voor Media Analytics**

   Deze parameters kunt u verkrijgen van een Adobe-medewerker nadat u uw account voor mediacontrole hebt ingesteld.
* **De volgende API&#39;s opnemen in uw mediaspeler**

   * _Een API die zich moet abonneren op spelergebeurtenissen_ - De SDK van Media vereist dat u een set eenvoudige API&#39;s oproept wanneer gebeurtenissen in de speler plaatsvinden.
   * _Een API die spelerinformatie biedt_ - Deze informatie bevat details zoals de medianaam en de positie van de afspeelkop.

Met Roku SDK 2.x voor Experience Cloud Solutions kunt u Roku-toepassingen die in BrightScript zijn geschreven, meten, gegevens voor het publiek gebruiken en verzamelen via publieksbeheer en de betrokkenheid van video&#39;s meten via videogebeurtenissen.

## Implementatie van mobiele bibliotheek / SDK

1. Voeg uw [gedownload](/help/getting-started/download-sdks.md) Bibliotheek uitvoeren naar uw project.

   1. De `AdobeMobileLibrary-2.*-Roku.zip` Het downloadbestand bestaat uit de volgende softwarecomponenten:

      * `adbmobile.brs`: Dit bibliotheekbestand wordt opgenomen in de bronmap van de Roku-app.

      * `ADBMobileConfig.json`: Dit SDK-configuratiebestand is aangepast voor uw app.
   1. Voeg het bibliotheekbestand en het JSON-configuratiebestand toe aan uw projectbron.

      De JSON die wordt gebruikt om Adobe Mobile te configureren, heeft een exclusieve sleutel voor mediaveralytics die `mediaHeartbeat`. Dit is waar de configuratieparameters voor de media analyses behoren.

      >[!TIP]
      >
      >Een monster `ADBMobileConfig` Het JSON-bestand wordt bij het pakket geleverd. Neem voor de instellingen contact op met de Adobe-vertegenwoordigers.

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
      >Indien `mediaHeartbeat` wordt verkeerd gevormd, gaat de media module (VHL) een foutenstaat in en zal ophouden verzendend volgende vraag.


1. Experience Cloud-bezoeker-id configureren.

   De dienst van identiteitskaart van de Bezoeker van Experience Cloud verstrekt universele Bezoeker identiteitskaart over de oplossingen van Experience Cloud. De service voor bezoekers-id is vereist voor videogebeurtenissen en andere Marketing Cloud-integratie.

   Controleer of uw `ADBMobileConfig` config bevat uw `marketingCloud` organisatie-id.

   ```
   "marketingCloud": {
       "org": "YOUR-MCORG-ID"
   }
   ```

   De organisatie-id&#39;s van Experience Cloud identificeren uniek elk clientbedrijf in de Adobe Marketing Cloud en lijken ongeveer op de volgende waarde te lijken: `016D5C175213CCA80A490D05@AdobeOrg`.

   >[!IMPORTANT]
   >
   >Zorg ervoor dat u `@AdobeOrg`.

   Nadat de configuratie volledig is, wordt een identiteitskaart van de Bezoeker van de Experience Cloud geproduceerd en inbegrepen op alle treffers. Andere bezoeker-id&#39;s, zoals `custom` en `automatically-generated`, blijft bij elke treffer worden verzonden.

   **Service-methoden voor Experience Cloud-bezoeker-id**

   >[!TIP]
   >
   >De methoden voor de Experience Cloud-bezoeker-id worden vooraf bepaald met `visitor`.

   |  Methode   | Beschrijving |
   | --- | --- |
   | `visitorMarketingCloudID` | Haalt de Experience Cloud-bezoeker-id op van de bezoeker-id-service.  <br/><br/>`ADBMobile().visitorMarketingCloudID()` |
   | `visitorSyncIdentifiers` | Met de Experience Cloud-bezoeker-id kunt u aanvullende klant-id&#39;s instellen die aan elke bezoeker kunnen worden gekoppeld. De bezoeker-API accepteert meerdere klant-id&#39;s voor dezelfde bezoeker en een id voor het klanttype om het bereik van de verschillende klant-id&#39;s te scheiden. Deze methode komt overeen met `setCustomerIDs`. Bijvoorbeeld: <br/><br/>`identifiers={}` <br/>`identifiers["idType"]="idValue"` <br/>`ADBMobile().visitorSyncIdentifiers(identifiers)` |
   | `setAdvertisingIdentifier` | Wordt gebruikt om de Roku-id voor advertentie (RIDA) in te stellen op de SDK. Bijvoorbeeld: <br/><br/> `ADBMobile().setAdvertisingIdentifier(`<br/>  `"<sample_roku_identifier_for_advertising>")` <br/><br/><br/>Haal de Roku-id voor adverteren (RIDA) op met de Roku-SDK [getRIDA()](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic) API. |
   | `getAllIdentifiers` | Retourneert een lijst met alle id&#39;s die door de SDK zijn opgeslagen, inclusief Analytics, Visitor, Audience Manager en aangepaste id&#39;s. <br/><br/> `identifiers = ADBMobile().getAllIdentifiers()` |
   <!--
    Roku Api Reference:
    * [Integrating the Roku Advertising Framework](https://sdkdocs.roku.com/display/sdkdoc/Integrating+the+Roku+Advertising+Framework)  
    * [GetRIDA()](https://sdkdocs.roku.com/display/sdkdoc/ifDeviceInfo#ifDeviceInfo-GetRIDA())
    -->

   **Aanvullende openbare API&#39;s**

   **DebugLogging**

   |  Methode   | Beschrijving |
   | --- | --- |
   | `setDebugLogging` | Gebruikt om te toelaten of onbruikbaar te maken zuivert registreren voor SDK.  <br/><br/>`ADBMobile().setDebugLogging(true)` |
   | `getDebugLogging` | Retourneert true als de logboekregistratie voor foutopsporing is ingeschakeld.  <br/><br/>`isDebugLoggingEnabled = ADBMobile().getDebugLogging()` |

   **PrivacyStatus**

   |  Constante   | Beschrijving |
   | --- | --- |
   | `PRIVACY_STATUS_OPT_IN` | Constante die moet worden doorgegeven tijdens het aanroepen van setPrivacyStatus voor aanmelden. <br/><br/>`optInString = ADBMobile().PRIVACY_STATUS_OPT_IN` |
   | `PRIVACY_STATUS_OPT_OUT` | Constante die moet worden doorgegeven terwijl setPrivacyStatus wordt aangeroepen om te weigeren. <br/><br/>`optOutString = ADBMobile().PRIVACY_STATUS_OPT_OUT` |

   |  Methode   | Beschrijving |
   | --- | --- |
   | `setPrivacyStatus` | Hiermee stelt u de privacystatus van de SDK in.  <br/><br/>`ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)` |
   | `getPrivacyStatus` | Haalt de huidige privacystatus op die is ingesteld op de SDK.  <br/><br/>`privacyStatus = ADBMobile().getPrivacyStatus()` |

   >[!IMPORTANT]
   >
   >Zorg ervoor dat u roept `processMessages` en `processMediaMessages` functie in de hoofdgebeurtenislijn om de 250 ms om ervoor te zorgen dat SDK pingelt behoorlijk verzendt.

   |  Methode   | Beschrijving |
   | --- | --- |
   | `processMessages` | Verantwoordelijk om de gebeurtenissen van de Analytics tot SDK over te gaan die moeten worden behandeld.  <br/><br/>`ADBMobile().processMessages()` |
   | `processMediaMessages` | Verantwoordelijk om de gebeurtenissen van Media tot SDK over te gaan die moeten worden behandeld. <br/><br/>`ADBMobile().processMediaMessages()` |


<!--    **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://experienceleague.adobe.com/docs/mobile-services/using/manage-app-settings-ug/configuring-app/signals.html) -->
