---
title: Media-rapporten inschakelen
description: Meer informatie over de mediarapportsuite voor het verzamelen van mediummetriek.  Voer de volgende stappen uit om mediapporten te configureren voordat mediagegevens worden verzonden.
uuid: d306068d-a308-4b6e-8a72-742dda0de428
exl-id: 686d88a5-79b6-4936-ba9e-8f834ef330d1
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---

# Media-rapporten inschakelen{#media-reports-enablement}

Elke rapportsuite die mediametriek verzamelt, moet worden geconfigureerd voordat mediagegevens worden verzonden.

De gevorderde klanten kunnen de media panelen in Analysis Workspace gebruiken slechts nadat de Kern van Media wordt toegelaten en het volgen wordt toegelaten voor [ Kwaliteit van Ervaring ](/help/use-cases/track-qos/track-qos-overview.md).

>[!TIP]
>
>Om uit nieuwe mogelijkheden voordeel te halen, zouden de bestaande het stromen media klanten media het volgen voor hun RSIDs opnieuw moeten toelaten.

1. In [ Rapporten &amp; Analytics ](https://my.omniture.com/login/) klik **[!UICONTROL Admin > Report Suites].**
1. Selecteer de rapportsuite(s) waar u mediagegevens verzamelt en klik op **[!UICONTROL Edit Settings > Media Management > Media Reporting].**

   ![](assets/media-reporting.png)

1. Voor de **[!UICONTROL Media Reporting]** pagina, laat **[!UICONTROL Media Core],** toe en naar keuze laat **[!UICONTROL Media Ads],** **[!UICONTROL Media Chapters],** en **[!UICONTROL Media Quality]toe.**

   Mediameting omvat de volgende modules:

   * **Kern van Media**

     De meting van de kernmedia wordt gebruikt voor media inhoud. Dit zal Oplossing (of Aangepast) eVars gebruiken om spoor van Inhoud, Type van Inhoud, de Naam van de Speler van de Inhoud, en het Kanaal van de Inhoud te houden. De (of Aangepaste) gebeurtenissen van de oplossing zullen voor Media worden gebruikt begint, de Begint van de Inhoud, de Voltooiing van de Inhoud, en de Tijd van de Inhoud.

   * **Media Adds**

     Media en metingen worden gebruikt voor het meten van advertenties in de media-inhoud. Dit zal de eVars van de Oplossing gebruiken om Advertentie, de Naam van de Speler van de Advertentie, Advertentiepod, en Advertentie in Pod te meten. De gebeurtenissen van de oplossing zullen voor Ad Begin, Ad voltooit, Ad Tijd bestede, en VideoTijd besteed worden gebruikt.

   * **Hoofdstukken van Media**

     Videohoofdstukken worden gemeten voor het meten van hoofdstukken. Een hoofdstuk is een onderverdeling van inhoud in één medium. Dit zal een Oplossing eVar gebruiken om Hoofdstuk ID op te slaan. De gebeurtenissen van de oplossing zullen voor Hoofdstukbeginnen, de Voltooiingen van het Hoofdstuk, en de Tijd van het Hoofdstuk worden gebruikt. Aanvullende hoofdstukmetagegevens van de hoofdstuknaam en hoofdstukpositie worden verstrekt als classificaties van Hoofdstuk ID.

   * **Kwaliteit van Media**

     De videokwaliteit wordt gemeten om de kwaliteit van de inhoudsplayback te meten. Dit zal OplossingseVars gebruiken om tijd aan Begin op te slaan, de Gebeurtenissen van de Buffer, de Totale Duur van de Buffer, de Schakelaars van de Bitsnelheid, Gemiddelde Bitsnelheid, Fouten, en gelaten vallen Kaders. De gebeurtenissen van de oplossing zullen voor Tijd aan Begin worden gebruikt, vallen vóór Begin, buffer beïnvloede stromen, buffergebeurtenissen, totale bufferduur, Bitsnelheidverandering beïnvloede stromen, Bitsnelheidveranderingen, Avg Bitrate stromen, Fout beïnvloede stromen, de Gebeurtenissen van de Fout, Geleide stromen van het Kader, en gelaten vallen kaders.

   * **Video &amp; Video en Metagegevens van de Advertentie**

     Metagegevens kunnen aan een media en/of een advertentie worden gekoppeld om die media/advertentie nader te beschrijven en te categoriseren. Gestandaardiseerde media en advertentiemetagegevens worden verzameld via oplossingsvariabelen en classificaties. Waarden die moeten worden opgenomen: Show, Season, Episode, Asset ID, Genre, First Air Date, First Digital Date, Content Rating, Originator, Network, Show Type, Ad Loads, MVPD, Authorized, Day Part, Media Session ID, Advertiser, Campagne ID, and Creative ID.

   * **Audio &amp; Audio en Metagegevens van de Advertentie**

     Metagegevens kunnen worden gekoppeld aan audio en/of een advertentie om die audio/advertentie nader te beschrijven en te categoriseren. Gestandaardiseerde audio- en advertentiemetagegevens worden verzameld via oplossingsvariabelen en classificaties. Waarden die moeten worden opgenomen: Artiest, Album, Label, Auteur, Uitgever, Station, Show, Season, Episode, Asset ID, Genre, First Air Date, First Digital Date, Content Rating, Originator, Show Type, Ad Loads, Day Part, Media Session ID, Advertiser, Campagne ID, and Creative ID.

   Als u elke module inschakelt, wordt een set variabelen gereserveerd en wordt een nieuwe set rapporten gemaakt. Met uitzondering van Kwaliteit, zullen er geen gegevens in rapporten zijn tenzij de overeenkomstige implementatie is voltooid. Het uitvoeren van de module van de Kern voert ook de module van de Kwaliteit uit als u het toelaat.

   Als u nog geen advertenties, hoofdstukken of afspeelkwaliteit bijhoudt, kunt u op elk gewenst moment aanvullende opties inschakelen.

1. Klik op **[!UICONTROL Save].**

   Als deze rapportsuite al is geconfigureerd voor het verzamelen van mediagegevens, wordt na het klikken op **[!UICONTROL Save]** een extra configuratiepagina weergegeven. Ga door met de volgende stap als de pagina **[!UICONTROL Media Core measurement]** wordt weergegeven.

1. (Voorwaardelijk) Op de pagina **[!UICONTROL Media Core measurement]** kiest u of u aangepaste variabelen wilt blijven gebruiken of oplossingvariabelen wilt gebruiken.

   | Optie | Notities |
   | --- | --- |
   | Doorgaan met aangepaste variabelen | Pros en kons:<ul> <li> **Pros:** De trending van de Inhoud blijft na migratie werken. </li> <li> **Kons:** vereist u om twee douaneVars en drie douanegebeurtenissen te houden die aan media worden toegewezen. U kunt één aangepaste eVar en één aangepaste gebeurtenis opnieuw gebruiken. </li> </ul> Aangepaste variabelen blijven gebruiken: <ol> <li>Selecteer **[!UICONTROL Use Custom Variables,]** en klik op **[!UICONTROL Save.]** </li> <li>Wijs desgevraagd uw aangepaste gebeurtenissen en gebeurtenissen toe en klik op **[!UICONTROL Save:]** </li> </ol> |
   | Migreren naar oplossingsvariabelen | Pros en kons:<ul> <li> **Pros:** u herkrijgt gebruik van drie douaneVars en vier douanegebeurtenissen. </li> <li> **Kons:** u verliest **alle** historische trending en vergelijking voor media rapporten. Dit betekent dat u de weergave van inhoud of de tijd van de inhoud die wordt afgespeeld voor geen van de datums kunt veranderen voordat u naar hartslagen migreerde. </li> </ul> **Beperking:** migreer niet aan oplossingsvariabelen tenzij u zeker bent dat u niet dit het trending wilt bewaren. Alle klanten zouden oplossingsvariabelen en verwerkingsregels moeten gebruiken om media gegevens in bestaande steunen en eVars te zetten, slechts als zij historische continuïteit moeten bewaren. Als u wilt migreren naar oplossingsvariabelen: selecteer **[!UICONTROL Use Solution Variables]** en klik op **[!UICONTROL Save].** <br><br> BELANGRIJK: Het migreren aan oplossingsvariabelen veroorzaakt u om **alle** historische trending en vergelijking voor media rapporten te verliezen. |

>[!IMPORTANT]
>
>Verander niet de classificatienamen voor om het even welke die variabelen in de Metriek en meta-gegevenslijsten (b.v., [ Audio en videoparameters ](/help/implementation/variables/audio-video-parameters.md) worden vermeld die daar onder het Melden/Gereserveerde Variabele als &quot;classificatie&quot;worden beschreven. De mediaclassificaties worden gedefinieerd wanneer een rapportsuite is ingeschakeld voor het bijhouden van media. Van tijd tot tijd, voegt Adobe nieuwe eigenschappen toe, en wanneer dit voorkomt, moeten de klanten hun rapportsuites opnieuw toelaten om toegang tot de nieuwe media eigenschappen te krijgen. Tijdens het updateproces bepaalt Adobe of de classificaties worden toegelaten door de namen van de variabelen te controleren. Als een van de ontbrekende elementen ontbreekt, voegt Adobe de ontbrekende opnieuw toe.
