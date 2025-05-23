---
title: Media SDK instellen voor Roku
description: Voer de volgende stappen uit om de Media SDK-toepassing in te stellen op Roku.
uuid: 904dfda0-4782-41da-b4ab-212e81156633
exl-id: b8de88d0-3a93-4776-b372-736bf979ee26
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 1%

---

# Mobiele SDK v2.x instellen voor Roku {#set-up-roku}

## Vereisten {#roku-prerequisites}

* **verkrijg geldige configuratieparameters voor de Streaming Inzameling van Media**

  Deze parameters kunt u verkrijgen van een Adobe-medewerker nadat u uw account voor het streamen van Adobe-media verzameling hebt ingesteld.
* **omvat volgende APIs in uw media speler**

   * _API om aan spelergebeurtenissen_ in te tekenen - de Media SDK vereist dat u een reeks eenvoudige APIs roept wanneer de gebeurtenissen in uw speler voorkomen.
   * _API die spelerinformatie_ verstrekt - Deze informatie omvat details zoals de media naam en de positie van het spelhoofd.

Met Roku SDK 2.x for Experience Cloud Solutions kunt u Roku-toepassingen die in BrightScript zijn geschreven, gebruiken en gegevens van het publiek verzamelen via publieksbeheer en de betrokkenheid van video&#39;s meten via videogebeurtenissen.

## Implementatie van mobiele bibliotheek / SDK

1. Voeg uw [ gedownloade ](/help/getting-started/download-sdks.md) bibliotheek van Roku aan uw project toe.

   1. Het `AdobeMobileLibrary-2.*-Roku.zip` -downloadbestand bestaat uit de volgende softwarecomponenten:

      * `adbmobile.brs`: Dit bibliotheekbestand wordt opgenomen in de bronmap van de Roku-app.

      * `ADBMobileConfig.json`: Dit SDK-configuratiebestand wordt aangepast voor uw app.

   1. Voeg het bibliotheekbestand en het JSON-configuratiebestand toe aan uw projectbron.

      JSON die wordt gebruikt om Adobe Mobile te vormen heeft een exclusieve sleutel voor media analyse genoemd `mediaHeartbeat`. Dit is waar de configuratieparameters voor media analyses behoren.

      >[!TIP]
      >
      >Het pakket bevat een voorbeeld van een JSON-bestand van het type `ADBMobileConfig` . Neem voor de instellingen contact op met de Adobe.

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
      | `publisher` | String that represents the content publisher unique identifier. |
      | `channel` | Tekenreeks die de naam van het distributiekanaal van de inhoud vertegenwoordigt. |
      | `ssl` | Boolean die aangeeft of SSL moet worden gebruikt voor het bijhouden van aanroepen. |
      | `ovp` | Tekenreeks die de naam van de videospelerprovider vertegenwoordigt. |
      | `sdkversion` | Tekenreeks die de huidige versie van de app/SDK vertegenwoordigt. |
      | `playerName` | Tekenreeks die de naam van de speler vertegenwoordigt. |

      >[!IMPORTANT]
      >
      >Als `mediaHeartbeat` verkeerd wordt gevormd, gaat de media module (VHL) een foutenstaat in en zal ophouden verzendend volgende vraag.

1. Vorm identiteitskaart van de Bezoeker van het Experience Cloud.

   De dienst van identiteitskaart van de Bezoeker van het Experience Cloud verstrekt een universele identiteitskaart van de Bezoeker over de oplossingen van het Experience Cloud. De service voor bezoekers-id is vereist voor videogebeurtenissen en andere Marketing Cloud-integratie.

   Controleer of de `ADBMobileConfig` config uw `marketingCloud` -organisatie-id bevat.

   ```
   "marketingCloud": {
       "org": "YOUR-MCORG-ID"
   }
   ```

   ID&#39;s van organisaties van Experiencen Cloud identificeren elk clientbedrijf in de Adobe Marketing Cloud op unieke wijze en lijken op de volgende waarde: `016D5C175213CCA80A490D05@AdobeOrg` .

   >[!IMPORTANT]
   >
   >Zorg ervoor dat u `@AdobeOrg` opneemt.

   Nadat de configuratie volledig is, wordt een identiteitskaart van de Bezoeker van het Experience Cloud geproduceerd en inbegrepen op alle treffers. Andere bezoeker-id&#39;s, zoals `custom` en `automatically-generated` , worden bij elke treffer verzonden.

   **Methoden van de Dienst van identiteitskaart van de Bezoeker van het Experience Cloud**

   >[!TIP]
   >
   >De methodes van identiteitskaart van de Bezoeker van het Experience Cloud worden vooraf bepaald met `visitor`.

   |  Methode   | Beschrijving |
   | --- | --- |
   | `visitorMarketingCloudID` | Haalt de bezoeker-id van het Experience Cloud op bij de bezoeker-id-service.  <br/><br/>`ADBMobile().visitorMarketingCloudID()` |
   | `visitorSyncIdentifiers` | Met de Experience Cloud Bezoeker-id kunt u extra klant-id&#39;s instellen die aan elke bezoeker kunnen worden gekoppeld. De bezoeker-API accepteert meerdere klant-id&#39;s voor dezelfde bezoeker en een id voor het klanttype om het bereik van de verschillende klant-id&#39;s te scheiden. Deze methode komt overeen met `setCustomerIDs` . Bijvoorbeeld: <br/><br/>`identifiers={}` <br/>`identifiers["idType"]="idValue"` <br/>`ADBMobile().visitorSyncIdentifiers(identifiers)` |
   | `setAdvertisingIdentifier` | Wordt gebruikt om de Roku-id voor Advertising (RIDA) in te stellen op de SDK. Bijvoorbeeld: <br/><br/> `ADBMobile().setAdvertisingIdentifier(`<br/>  `"<sample_roku_identifier_for_advertising>")` <br/><br/><br/> krijgt identiteitskaart van Roku voor Advertising (RIDA) gebruikend Roku SDK [ getRIDA () ](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic) API. |
   | `getAllIdentifiers` | Retourneert een lijst met alle id&#39;s die door de SDK zijn opgeslagen, inclusief Analytics, Visitor, Audience Manager en aangepaste id&#39;s. <br/><br/> `identifiers = ADBMobile().getAllIdentifiers()` |

   <!--
    Roku Api Reference:
    * [Integrating the Roku Advertising Framework](https://sdkdocs.roku.com/display/sdkdoc/Integrating+the+Roku+Advertising+Framework)  
    * [GetRIDA()](https://sdkdocs.roku.com/display/sdkdoc/ifDeviceInfo#ifDeviceInfo-GetRIDA())
    -->

   **Extra Openbare APIs**

   **DebugLogging**

   |  Methode   | Beschrijving |
   | --- | --- |
   | `setDebugLogging` | Wordt gebruikt om foutopsporingslogbestanden voor de SDK in of uit te schakelen. <br/><br/>`ADBMobile().setDebugLogging(true)` |
   | `getDebugLogging` | Retourneert true als de logboekregistratie voor foutopsporing is ingeschakeld.  <br/><br/>`isDebugLoggingEnabled = ADBMobile().getDebugLogging()` |

   **PrivacyStatus**

   |  Constante   | Beschrijving |
   | --- | --- |
   | `PRIVACY_STATUS_OPT_IN` | Constante die moet worden doorgegeven tijdens het aanroepen van setPrivacyStatus voor aanmelden. <br/><br/>`optInString = ADBMobile().PRIVACY_STATUS_OPT_IN` |
   | `PRIVACY_STATUS_OPT_OUT` | Constante die moet worden doorgegeven terwijl setPrivacyStatus wordt aangeroepen om te weigeren. <br/><br/>`optOutString = ADBMobile().PRIVACY_STATUS_OPT_OUT` |

   |  Methode   | Beschrijving |
   | --- | --- |
   | `setPrivacyStatus` | Stelt de privacystatus in op de SDK. <br/><br/>`ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)` |
   | `getPrivacyStatus` | Haalt de huidige privacystatus op die op de SDK is ingesteld. <br/><br/>`privacyStatus = ADBMobile().getPrivacyStatus()` |

   >[!IMPORTANT]
   >
   >Zorg ervoor dat u de `processMessages` - en `processMediaMessages` -functie om de 250 ms aanroept in de hoofdgebeurtenislus om ervoor te zorgen dat de SDK de pingelt correct verzendt.

   |  Methode   | Beschrijving |
   | --- | --- |
   | `processMessages` | Verantwoordelijk om de gebeurtenissen van de Analytics tot SDK over te gaan om worden behandeld.  <br/><br/>`ADBMobile().processMessages()` |
   | `processMediaMessages` | Verantwoordelijk om de Media-gebeurtenissen door te geven aan de SDK die moet worden afgehandeld. <br/><br/>`ADBMobile().processMediaMessages()` |


<!--    **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://experienceleague.adobe.com/docs/mobile-services/using/manage-app-settings-ug/configuring-app/signals.html?lang=nl-NL) -->
