---
title: De Media SDK instellen voor Chromecast
description: Voer de volgende stappen uit om de Media SDK-toepassing op Chromecast in te stellen.
uuid: d664e394-02a2-4985-bbad-be1bcc44fb2b
exl-id: 5dfe3407-2858-48c0-a70c-8ea87967ac47
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 0%

---

# Mobiele SDK v3.x instellen voor Chromecast {#set-up-chromecast}

In deze sectie worden de voorwaarden beschreven voor het instellen van een Chromecast-installatie voor Adobe-streaming-mediaservices.

## Vereisten

* **verkrijg geldige configuratieparameters**

  Deze parameters kunt u verkrijgen van een Adobe-medewerker nadat u uw account voor mediacontrole hebt ingesteld.
* **omvat volgende APIs in uw media speler**

   * *API om aan spelergebeurtenissen* in te tekenen - de Media SDK vereist dat u een reeks eenvoudige APIs roept wanneer de gebeurtenissen in uw speler voorkomen.
   * *API die spelerinformatie* verstrekt - Deze informatie omvat details zoals de media naam en de positie van het spelhoofd.

Adobe Mobile-services bieden een nieuwe gebruikersinterface waarin mobiele marketingmogelijkheden voor mobiele toepassingen uit de hele Adobe Marketing Cloud worden samengebracht. Aanvankelijk biedt de Mobile-service een naadloze integratie van analysemogelijkheden voor apps en doelgerichte functionaliteit voor de Adobe Analytics- en Adobe Target-oplossingen. Leer meer bij [ de Mobiele documentatie van de Diensten van Adobe.](https://experienceleague.adobe.com/docs/mobile-services/using/home.html)

Met de Adobe Mobile Library for Chromecast v3.x for Experience Cloud Solutions kunt u Chromecast-toepassingen die in JavaScript zijn geschreven, meten, publieksgegevens verzamelen en benutten via publieksbeheer en de betrokkenheid van video meten.

## Implementatie van mobiele bibliotheek / SDK

1. Voeg uw gedownloade Chromecast-bibliotheek toe aan uw project.

   1. Het ZIP-bestand van `AdobeMobileLibrary-Chromecast-[version]` bestaat uit de volgende softwarecomponenten:

      * `adbmobile-chromecast.min.js`:

        Dit bibliotheekbestand wordt opgenomen in de bronmap van de Chromecast-app.

      * `ADBMobileConfig` config

        Dit SDK-configuratiebestand is aangepast voor uw app. Bij de SDK wordt een voorbeeldimplementatie `ADBMobileConfig` geleverd (onder `samples/` ). Verkrijg de juiste montages van een vertegenwoordiger van Adobe.

   1. Voeg het bibliotheekbestand toe aan het `index.html` -bestand en maak de globale variabele `ADBMobileConfig` als volgt (de algemene variabele die wordt gebruikt om Adobe Mobile for Media Analytics te configureren heeft een exclusieve sleutel met de naam `mediaHeartbeat` ):

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
              "rsids": "example.sample.player",
              "server": "example.sc.omtrc.net",
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
              "server": "example.hb-api.omtrdc.net",
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
      >Als `mediaHeartbeat` verkeerd wordt gevormd, gaat de media module een foutenstaat in en zal ophouden verzendend volgende vraag.

      ADBMobile Config-parameters voor de MediaHeartbeat-sleutel:

   | Configuratieparameter | Beschrijving     |
   | --- | --- |
   | `server` | Tekenreeks die de URL van het volgende eindpunt op de achtergrond vertegenwoordigt. |
   | `publisher` | String that represents the content publisher unique identifier. |
   | `channel` | Tekenreeks die de naam van het distributiekanaal van de inhoud vertegenwoordigt. |
   | `ssl` | Boolean die aangeeft of SSL moet worden gebruikt voor het bijhouden van aanroepen. |
   | `ovp` | Tekenreeks die de naam van de videospelerprovider vertegenwoordigt. |
   | `sdkversion` | Tekenreeks die de huidige versie van de app/SDK vertegenwoordigt. |
   | `playerName` | Tekenreeks die de naam van de speler vertegenwoordigt. |


1. Experience Cloud-bezoeker-id configureren.

   De Experience Cloud Visitor ID-service biedt een universele bezoeker-id voor alle Experience Cloud-oplossingen. De service voor bezoekers-id is vereist voor Media Analytics en andere Marketing Cloud-integraties.

   Controleer of de `ADBMobileConfig` config uw `marketingCloud` -organisatie-id bevat.

   ```
   "marketingCloud": {
       "org": "YOUR-MCORG-ID"
   }
   ```

   Experience Cloud-organisatie-id&#39;s identificeren elk clientbedrijf op unieke wijze in de Adobe Marketing Cloud en lijken op de volgende waarde: `016D5C175213CCA80A490D05@AdobeOrg` .

   >[!IMPORTANT]
   >
   >Zorg ervoor dat u `@AdobeOrg` opneemt.

   Nadat de configuratie volledig is, wordt een identiteitskaart van de Bezoeker van Experience Cloud geproduceerd en inbegrepen op alle treffers. Andere bezoeker-id&#39;s, zoals `custom` en `automatically-generated` , worden bij elke treffer verzonden.

   **Methoden van de Dienst van identiteitskaart van de Bezoeker van Experience Cloud**

   >[!TIP]
   >
   >De methoden voor Experience Cloud Visitor ID worden vooraf ingesteld door `visitor` .

   | Methode | Beschrijving |
   | --- | --- |
   | `getMarketingCloudID()` | Haalt de Experience Cloud Visitor ID op van de Bezoeker ID-service.  <br/><br/>`ADBMobile.visitor.getMarketingCloudID();` |
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
