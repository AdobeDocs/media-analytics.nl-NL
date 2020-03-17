---
title: Auditiebeheer inschakelen
description: null
uuid: 8a7f9343-ebc3-4087-9d7e-5972640d2455
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Auditiebeheer inschakelen{#audience-manager-enablement}

Met Adobe Audience Manager (AAM), een DMP-platform (Data Management Platform), kunt u uw middelen voor publieksgegevens samenbrengen, zodat u eenvoudig commercieel relevante informatie over sitebezoekers kunt verzamelen, verhandelbare segmenten kunt maken en doelgerichte reclame en inhoud aan het juiste publiek kunt leveren.

Met AAM bent u niet gebonden aan een gegevensverkoper, -uitwisseling of -platform. Bovendien, is AAM volledig agnostisch wanneer het op de gegevensactiva van uw partners komt. Met toegang tot meerdere gegevensbronnen biedt AAM digitale uitgevers de mogelijkheid om een grote verscheidenheid aan gegevens van derden en onze persoonlijke gegevens te gebruiken. Meer over AAM leren, zie de Documentatie van het Product van de Manager van het [publiek van AAM.](https://docs-author.corp.adobe.com/content/help/en/audience-manager/user-guide/aam-home.html)

**VA naar AAM gegevensoverdracht -** Voor zowel video-inhoud als video-advertenties kunnen de gegevens en metagegevens die met (gereserveerde) oplossingsvariabelen zijn verzameld, automatisch naar AAM worden verzonden. De gegevensoverdracht is beschikbaar op alle platforms, inclusief desktopcomputers, mobiele apparaten en OTT. Als u deze gegevensoverdracht aan de serverzijde wilt inschakelen, moet u contact opnemen met de klantenservice van Adobe en vragen of deze feed is ingeschakeld.

>[!IMPORTANT]
>
>Om de vlotte overdracht van gegevens aan AAM te verzekeren, zou u op de recentste versies van de bibliotheken van SDK van Media moeten zijn.

Federale Gegevens steunen volledig gegevens die aan AAM delen. Werk samen met uw Adobe-team voor bevestiging van de instellingen voor Federale gegevens.

## OTT/AAM-methoden {#ott-aam-methods}

U kunt deze methodes gebruiken om signalen te verzenden en bezoekerssegmenten van de Manager van het Publiek terug te winnen:

### Chromecast {#am-chromecast}

* `getVisitorProfile() -`

   Retourneert het bezoekersprofiel dat het laatst is verkregen. Retourneert een leeg object als er nog geen signaal is verzonden.

   ```js
   ADBMobile.audienceManager.getVisitorProfile();
   ```

* `getDpid() -`

   Retourneert het bezoekersprofiel dat het laatst is verkregen. Retourneert een leeg object als er nog geen signaal is verzonden.

   ```js
   ADBMobile.audienceManager.getDpid();
   ```

* `getDpuuid() -`

   Retourneert de huidige DPUUID.

   ```js
   ADBMobile.audienceManager.getDpuuid();
   ```

* `setDpidAndDpuuid() -`

   Hiermee stelt u de DPID en DPUUID in. Als DPID en DPUUID worden geplaatst, zullen zij met elk signaal worden verzonden.

   ```js
   ADBMobile.audienceManager.SetDpidAndDpuuid("myDpid", "myDpuuid");
   ```

* `submitSignal() -`

   Verzendt publieksbeheer een signaal met eigenschappen.

   ```js
   ADBMobile.audienceManager.SubmitSignal();
   ```

### Roku {#am-roku}

* `audienceVisitorProfile -`

   Retourneert het bezoekersprofiel dat het laatst is verkregen. Retourneert een leeg object als er nog geen signaal is verzonden.

   ```js
   ADBMobile().audienceVisitorProfile()
   ```

* `audienceDpid -`

   Retourneert het bezoekersprofiel dat het laatst is verkregen. Retourneert een lege obje t als er nog geen signaal is verzonden.

   ```js
   ADBMobile().audienceDpid()
   ```

* `audienceDpuuid -`

   Retourneert de huidige DPUUID.

   ```js
   ADBMobile().audienceDpuuid()
   ```

* `audienceSetDpidAndDpuuid -`

   Hiermee stelt u de DPID en DPUUID in. Als DPID en DPUUID worden geplaatst, zullen zij met elk signaal worden verzonden.

   ```js
   ADBMobile().audienceSetDpidAndDpuuid("myDpid", "myDpuuid")
   ```

* `audienceSubmitSignal -`

   Verzendt publieksbeheer een signaal met eigenschappen.

   ```js
   ADBMobile().audienceSubmitSignal()
   ```

