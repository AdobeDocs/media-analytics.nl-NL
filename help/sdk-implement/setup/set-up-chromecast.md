---
title: Hoe te opstelling media SKD voor Chromecast
description: Voer de volgende stappen uit om de Media SDK-toepassing in Chromecast in te stellen.
uuid: d664e394-02a2-4985-bbad-be1bcc44fb2b
exl-id: 5dfe3407-2858-48c0-a70c-8ea87967ac47
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 270dc48152dd77d7ceff8ce1ea9fbead0d1ce9be
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 1%

---

# Chromecast instellen{#set-up-chromecast}

## Veelgestelde vragen

_Moet ik de Chromecast JavaScript SDK gebruiken of kan ik de Standaard JavaScript SDK gebruiken?_

Het juiste antwoord is &quot;Chromecast&quot;, om de volgende redenen:
* De API-bibliotheken van AppMeasurement en Visitor in de standaard JS SDK zijn niet gecertificeerd voor gebruik op OTT-platforms. In Chromecast JS SDK, zijn de Video Heartbeats Bibliotheek (VHL), Analytics, en VisitorAPI allen ingebouwde aan enige, verenigde, verklaarde-voor-Chromecast SDK.
* De Chromecast SDK is veel lichter dan de standaard JS SDK. Dit is zeer essentieel voor de onderste-eindhardware die door OTT platforms wordt gebruikt.

## Vereisten

* **Verkrijg geldige configuratieparameters voor**
HeartbeatsDeze parameters kunnen bij een vertegenwoordiger van Adobe worden verkregen nadat u uw media analytics-account hebt ingesteld.
* **Biedt de volgende mogelijkheden in uw mediaspeler:**
   * *Een API die zich moet abonneren op spelergebeurtenissen* . De Media SDK vereist dat u een set eenvoudige API&#39;s aanroept wanneer gebeurtenissen in de speler plaatsvinden.
   * *Een API die spelerinformatie*  verschaft. Deze informatie bevat details zoals de medianaam en de positie van de afspeelkop.

Adobe Mobile-services bieden een nieuwe gebruikersinterface waarin mobiele marketingmogelijkheden voor mobiele toepassingen uit de hele Adobe Marketing Cloud worden samengebracht. Aanvankelijk biedt de Mobile-service een naadloze integratie van analysemogelijkheden voor apps en doelgerichte functionaliteit voor de Adobe Analytics- en Adobe Target-oplossingen. Meer informatie vindt u in de [Adobe Mobile Services-documentatie.](https://experienceleague.adobe.com/docs/mobile-services/using/home.html)

Met Chromecast SDK 2.x voor Experience Cloud Solutions kunt u Chromecast-toepassingen meten die in JavaScript zijn geschreven, publieksgegevens benutten en verzamelen via publieksbeheer en de videobetrokkenheid meten via videohartslagen.

## SDK-implementatie

1. Voeg uw [gedownloade ](/help/sdk-implement/download-sdks.md#download-2x-sdks) Chromecast bibliotheek aan uw project toe.

   1. Het ZIP-bestand `AdobeMobileLibrary-Chromecast-[version]` bestaat uit de volgende softwarecomponenten:

      * `adbmobile-chromecast.min.js`:

         Dit bibliotheekbestand wordt opgenomen in de bronmap van de Chromecast-app.

      * `ADBMobileConfig` config

         Dit SDK-configuratiebestand is aangepast voor uw app. Bij de SDK wordt een voorbeeld van `ADBMobileConfig`-implementatie geleverd (onder `samples/`). Verkrijg de juiste montages van een vertegenwoordiger van de Adobe.
   1. Voeg het bibliotheekbestand toe aan uw `index.html`-bestand en maak de globale variabele `ADBMobileConfig` als volgt (de algemene variabele die wordt gebruikt om Adobe Mobile voor hartslagen te configureren heeft een exclusieve sleutel met de naam `mediaHeartbeat`):

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
              "ssl": true,
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
              "ssl": true,
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
   | Configuratieparameter | Beschrijving     |
   | --- | --- |
   | `server` | Tekenreeks die de URL van het volgende eindpunt op de achtergrond vertegenwoordigt. |
   | `publisher` | Tekenreeks die de unieke id van de uitgever van de inhoud vertegenwoordigt. |
   | `channel` | Tekenreeks die de naam van het distributiekanaal van de inhoud vertegenwoordigt. |
   | `ssl` | Booleaanse waarde die aangeeft of SSL moet worden gebruikt voor het bijhouden van aanroepen. |
   | `ovp` | Tekenreeks die de naam van de videospelerprovider vertegenwoordigt. |
   | `sdkversion` | Tekenreeks die de huidige versie van de app/SDK vertegenwoordigt. |
   | `playerName` | Tekenreeks die de naam van de speler vertegenwoordigt. |


1. Experience Cloud-bezoeker-id configureren.

   De dienst van identiteitskaart van de Bezoeker van Experience Cloud verstrekt universele Bezoeker identiteitskaart over de oplossingen van Experience Cloud. De service voor bezoekers-id is vereist voor Video-hartslag en andere Marketing Cloud-integratie.

   Verifieer dat uw `ADBMobileConfig` config uw `marketingCloud` organisatie ID bevat.

   ```js
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

   | Methode | Beschrijving |
   | --- | --- |
   | `getMarketingCloudID()` | Haalt de Experience Cloud Bezoeker-id op van de Bezoeker-id-service.  <br/><br/>`ADBMobile.visitor.getMarketingCloudID();` |
   | `syncIdentifiers()` | Met de Experience Cloud-bezoeker-id kunt u aanvullende klant-id&#39;s instellen die aan elke bezoeker kunnen worden gekoppeld. De bezoeker-API accepteert meerdere klant-id&#39;s voor dezelfde bezoeker en een id voor het klanttype om het bereik van de verschillende klant-id&#39;s te scheiden. Deze methode komt overeen met `setCustomerIDs()` in de JavaScript-bibliotheek.  Bijvoorbeeld: <br/><br/>`var identifiers = {};` <br/><br/>`identifiers["idType"] = "idValue";` <br/><br/>`ADBMobile.visitor.syncIdentifiers(identifiers);` |

1. Implementeer het MediaDelegate-protocol voor het bijhouden van media

   ```js
    var delegate = {
      // Replace <currentPlaybackTime> with the video player current playback time
      getCurrentPlaybackTime = function() {
        return <currentPlaybackTime>;
      },
      // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames> with the current playback QoS values.
      getQoSObject = function() {
         return ADBMobile.media.createQoSObject(<bitrate>, <startupTime>, <fps>, <droppedFrames>);
      }
    }
   
    ADBMobile.media.setDelegate(delegate);
   }
   ```

<!--   **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://experienceleague.adobe.com/docs/mobile-services/using/manage-app-settings-ug/configuring-app/signals.html) -->
