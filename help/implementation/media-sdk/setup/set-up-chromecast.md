---
title: Hoe te opstelling SDK van Media voor Chromecast
description: Voer de volgende stappen uit om de Media SDK-toepassing in Chromecast in te stellen.
uuid: d664e394-02a2-4985-bbad-be1bcc44fb2b
exl-id: 5dfe3407-2858-48c0-a70c-8ea87967ac47
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---

# Mobiele SDK v3.x instellen voor Chromecast {#set-up-chromecast}

In deze sectie worden de voorwaarden beschreven voor het instellen van een Chromecast-installatie voor streamingmedia.

## Vereisten

* **Geldige configuratieparameters verkrijgen**

   Deze parameters kunt u verkrijgen van een Adobe-medewerker nadat u uw account voor mediacontrole hebt ingesteld.
* **De volgende API&#39;s opnemen in uw mediaspeler**

   * *Een API die zich moet abonneren op spelergebeurtenissen* - De SDK van Media vereist dat u een set eenvoudige API&#39;s oproept wanneer gebeurtenissen in de speler plaatsvinden.
   * *Een API die spelerinformatie biedt* - Deze informatie bevat details zoals de medianaam en de positie van de afspeelkop.

Adobe Mobile-services bieden een nieuwe gebruikersinterface waarin mobiele marketingmogelijkheden voor mobiele toepassingen uit de hele Adobe Marketing Cloud worden samengebracht. Aanvankelijk biedt de Mobile-service een naadloze integratie van analysemogelijkheden voor apps en doelgerichte functionaliteit voor de Adobe Analytics- en Adobe Target-oplossingen. Meer informatie vindt u op [Adobe Mobile Services-documentatie.](https://experienceleague.adobe.com/docs/mobile-services/using/home.html)

Met de Adobe Mobile Library for Chromecast v3.x for Experience Cloud Solutions kunt u Chromecast-toepassingen die zijn geschreven in JavaScript meten, gegevens over het publiek verzamelen en benutten via publieksbeheer en de betrokkenheid van video&#39;s meten.

## Implementatie van mobiele bibliotheek / SDK

1. Voeg uw gedownloade Chromecast-bibliotheek toe aan uw project.

   1. De `AdobeMobileLibrary-Chromecast-[version]` ZIP-bestand bestaat uit de volgende softwareonderdelen:

      * `adbmobile-chromecast.min.js`:

         Dit bibliotheekbestand wordt opgenomen in de bronmap van de Chromecast-app.

      * `ADBMobileConfig` config

         Dit SDK-configuratiebestand is aangepast voor uw app. Een monster `ADBMobileConfig` de implementatie wordt geleverd bij de SDK (onder `samples/`). Verkrijg de juiste montages van een vertegenwoordiger van de Adobe.
   1. Het bibliotheekbestand toevoegen aan uw `index.html` en maak de `ADBMobileConfig` globale variabele als volgt (de globale variabele die wordt gebruikt om Adobe Mobile voor de Analyse van Media te vormen heeft een exclusieve sleutel genoemd `mediaHeartbeat`):

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
      >Indien `mediaHeartbeat` wordt verkeerd gevormd, gaat de media module een foutenstaat in en zal ophouden verzendend volgende vraag.

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

   De dienst van identiteitskaart van de Bezoeker van Experience Cloud verstrekt universele Bezoeker identiteitskaart over de oplossingen van Experience Cloud. De service voor bezoekers-id is vereist voor Media Analytics en andere Marketing Cloud-integraties.

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
