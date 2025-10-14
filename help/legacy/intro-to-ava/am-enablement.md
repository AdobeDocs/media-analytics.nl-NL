---
title: Wat is Adobe Audience Manager ingeschakeld?
description: Leer hoe u handelingen van toepassingen koppelt aan gegevens voor mediatracering zonder dat u extra verwerkingsregels en aangepaste variabelen nodig hebt.
exl-id: c0d73bc2-4713-498a-8882-ff66c7f3dd50
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---

# Audience Manager-activering{#audience-manager-enablement}

Met Adobe Audience Manager (AAM), een platform voor gegevensbeheer (DMP), kunt u uw publieksgegevens samenbrengen, zodat u eenvoudig commercieel relevante informatie over sitebezoekers kunt verzamelen, verhandelbare segmenten kunt maken en doelgerichte advertenties en inhoud aan het juiste publiek kunt leveren.

Met AAM ben je niet gebonden aan een gegevensverkoper, -uitwisseling of -platform. Bovendien is AAM volkomen onbehagen als het gaat om de gegevensmiddelen van uw partners. Met toegang tot meerdere gegevensbronnen biedt AAM digitale uitgevers de mogelijkheid om een groot aantal gegevens van derden te gebruiken. Meer over AAM leren, zie de documentatie van AAM [&#x200B; de Documentatie van het Product van Audience Manager &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html?lang=nl-NL).

**VA aan de gegevensoverdracht van AAM -** voor zowel video inhoud als videoreclame, kunnen de metriek en de metriek die door (gereserveerde) oplossingsvariabelen worden verzameld automatisch worden verzonden naar AAM. De gegevensoverdracht is beschikbaar op alle platforms, inclusief desktopcomputers, mobiele apparaten en OTT. Als u deze gegevensoverdracht aan de serverzijde wilt inschakelen, moet u contact opnemen met de Adobe Client Care en vragen of deze feed is ingeschakeld.

>[!IMPORTANT]
>
>Voor een soepele gegevensoverdracht naar AAM moet u beschikken over de nieuwste versies van de Media SDK-bibliotheken.

Federated Data biedt volledige ondersteuning voor het delen van gegevens naar AAM. Werk samen met uw Adobe-team voor bevestiging van de instellingen voor Federale gegevens.

## OTT/AAM-methoden {#ott-aam-methods}

U kunt deze methoden gebruiken om signalen te verzenden en bezoekerssegmenten op te halen uit Audience Manager:

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
  ADBMobile.audienceManager.setDpidAndDpuuid("myDpid", "myDpuuid");
  ```

* `submitSignal() -`

  Verzendt publieksbeheer een signaal met eigenschappen.

  ```js
  ADBMobile.audienceManager.submitSignal({"sampleTrait":"sampleValue"});
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
  traitData = {}
  traitData["sampleTrait"] = "sampleValue"
  ADBMobile().audienceSubmitSignal(traitData)
  ```
