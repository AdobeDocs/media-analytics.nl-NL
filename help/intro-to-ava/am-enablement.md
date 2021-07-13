---
title: Wat is Adobe Audience Manager ingeschakeld?
description: Leer hoe u handelingen van toepassingen koppelt aan gegevens voor mediatracering zonder dat u extra verwerkingsregels en aangepaste variabelen nodig hebt.
exl-id: c0d73bc2-4713-498a-8882-ff66c7f3dd50
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# Audience Manager inschakelen{#audience-manager-enablement}

Met Adobe Audience Manager (AAM), een DMP-Platform (Data Management ), kunt u uw publieksgegevens samenbrengen, zodat u eenvoudig commercieel relevante informatie over sitebezoekers kunt verzamelen, verhandelbare segmenten kunt maken en doelgerichte reclame en inhoud aan het juiste publiek kunt leveren.

Met AAM bent u niet gebonden aan een gegevensverkoper, -uitwisseling of -platform. Bovendien, is AAM volledig agnostisch wanneer het op de gegevensactiva van uw partners komt. Met toegang tot meerdere gegevensbronnen biedt AAM digitale uitgevers de mogelijkheid om een grote verscheidenheid aan gegevens van derden en onze persoonlijke datacommunicatie te gebruiken. Voor meer informatie over AAM, zie de AAM documentatie [de Documentatie van het Product van de Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html).

**VA naar AAM gegevensoverdracht -** Voor zowel video-inhoud als video-advertenties kunnen de gegevens en metagegevens die met behulp van (gereserveerde) oplossingsvariabelen zijn verzameld, automatisch naar AAM worden verzonden. De gegevensoverdracht is beschikbaar op alle platforms, inclusief desktopcomputers, mobiele apparaten en OTT. Om deze server-zijgegevensoverdracht toe te laten, moet u uit naar de Zorg van de Adobe Cliënt reiken en om deze voer vragen worden toegelaten.

>[!IMPORTANT]
>
>Voor een vloeiende overdracht van gegevens naar AAM moet u zich op de meest recente versies van de mediaSDK-bibliotheken bevinden.

Federale gegevens bieden volledige ondersteuning voor het delen van gegevens naar AAM. Werk samen met uw Adobe-team voor bevestiging van de instellingen voor gegevens van Federated.

## OTT-/AAM-methoden {#ott-aam-methods}

U kunt deze methodes gebruiken om signalen te verzenden en bezoekerssegmenten van Audience Manager terug te winnen:

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
