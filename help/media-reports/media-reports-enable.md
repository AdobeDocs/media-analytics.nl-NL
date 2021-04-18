---
title: Media-rapporten inschakelen
description: Media-rapporten inschakelen
uuid: d306068d-a308-4b6e-8a72-742dda0de428
exl-id: 686d88a5-79b6-4936-ba9e-8f834ef330d1
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 1%

---

# Inschakelen van mediapporten{#media-reports-enablement}

Elke rapportsuite die mediametriek verzamelt, moet worden geconfigureerd voordat mediagegevens worden verzonden.

>[!TIP]
>
>Om uit nieuwe mogelijkheden voordeel te halen, zouden de bestaande klanten van Media Analytics media het volgen voor hun RSIDs moeten re-toelaten.

1. Klik in [Rapporten &amp; Analytics](https://my.omniture.com/login/) op **[!UICONTROL Admin > Report Suites].**
1. Selecteer de rapportsuite(s) waar u mediadata verzamelt en klik op **[!UICONTROL Edit Settings > Media Management > Media Reporting].**

   ![](assets/media-reporting.png){width=&quot;400px&quot;}

1. Schakel op de pagina **[!UICONTROL Media Reporting]** **[!UICONTROL Media Core],** in en schakel **[!UICONTROL Media Ads],** **[!UICONTROL Media Chapters],** en **[!UICONTROL Media Quality]optioneel in.**

   Mediameting omvat de volgende modules:

   * **Media Core**

      De meting van de kernmedia wordt gebruikt voor media inhoud. Dit zal Oplossing (of Aangepast) eVars gebruiken om spoor van Inhoud, Type van Inhoud, de Naam van de Speler van de Inhoud, en het Kanaal van de Inhoud te houden. De (of Aangepaste) gebeurtenissen van de oplossing zullen voor Media worden gebruikt begint, de Begint van de Inhoud, de Voltooiing van de Inhoud, en de Tijd van de Inhoud.

   * **Media-advertenties**

      Media en metingen worden gebruikt voor het meten van advertenties in de media-inhoud. Dit zal de eVars van de Oplossing gebruiken om Advertentie, de Naam van de Speler van de Advertentie, Advertentiepod, en Advertentie in Pod te meten. De gebeurtenissen van de oplossing zullen voor Ad Begin, Ad voltooit, Ad Tijd bestede, en VideoTijd besteed worden gebruikt.

   * **Mediahoofdstukken**

      Videohoofdstukken worden gemeten voor het meten van hoofdstukken. Een hoofdstuk is een onderverdeling van inhoud in één medium. Dit zal een eVar van de Oplossing gebruiken om Hoofdstuk ID op te slaan. De gebeurtenissen van de oplossing zullen voor Hoofdstukbeginnen, de Voltooiingen van het Hoofdstuk, en de Tijd van het Hoofdstuk worden gebruikt. Extra hoofdstukmeta-gegevens van de Naam van het Hoofdstuk en de Positie van het Hoofdstuk zullen als classificaties van Hoofdstuk ID worden verstrekt.

   * **Mediakwaliteit**

      De videokwaliteit wordt gemeten om de kwaliteit van de inhoudsplayback te meten. Dit zal OplossingseVars gebruiken om tijd aan Begin op te slaan, de Gebeurtenissen van de Buffer, de Totale Duur van de Buffer, de Schakelaars van de Bitsnelheid, Gemiddelde Bitsnelheid, Fouten, en gelaten vallen Kaders. De gebeurtenissen van de oplossing zullen voor Tijd aan Begin worden gebruikt, vallen vóór Begin, buffer beïnvloede stromen, buffergebeurtenissen, totale bufferduur, Bitsnelheidverandering beïnvloede stromen, Bitsnelheidveranderingen, Avg Bitrate stromen, Fout beïnvloede stromen, de Gebeurtenissen van de Fout, Geleide stromen van het Kader, en gelaten vallen kaders.

   * **Video en video en metagegevens**

      Metagegevens kunnen aan een media en/of een advertentie worden gekoppeld om die media/advertentie nader te beschrijven en te categoriseren. Gestandaardiseerde media en advertentiemetagegevens worden verzameld via oplossingsvariabelen en classificaties. Waarden die moeten worden opgenomen: Show, Season, Episode, Asset ID, Genre, First Air Date, First Digital Date, Content Rating, Originator, Network, Show Type, Ad Loads, MVPD, Authorized, Day Part, Media Session ID, Advertiser, Campagne ID, and Creative ID.

   * **Audio en audio en metagegevens**

      Metagegevens kunnen worden gekoppeld aan audio en/of een advertentie om die audio/advertentie nader te beschrijven en te categoriseren. Gestandaardiseerde audio- en advertentiemetagegevens worden verzameld via oplossingsvariabelen en classificaties. Waarden die moeten worden opgenomen: Artiest, Album, Label, Auteur, Uitgever, Station, Show, Season, Episode, Asset ID, Genre, First Air Date, First Digital Date, Content Rating, Originator, Show Type, Ad Loads, Day Part, Media Session ID, Advertiser, Campagne ID, and Creative ID.
   Als u elke module inschakelt, wordt een set variabelen gereserveerd en wordt een nieuwe set rapporten gemaakt. Met uitzondering van Kwaliteit, zullen er geen gegevens in rapporten zijn tenzij de overeenkomstige implementatie is voltooid. Het uitvoeren van de module van de Kern voert ook de module van de Kwaliteit uit als u het toelaat.

   Als u nog geen advertenties, hoofdstukken of afspeelkwaliteit bijhoudt, kunt u op elk gewenst moment aanvullende opties inschakelen.

1. Klik op **[!UICONTROL Save].**

   Als deze rapportsuite al is geconfigureerd voor het verzamelen van mediagegevens, wordt na het klikken op **[!UICONTROL Save]** een extra configuratiepagina weergegeven. Ga door met de volgende stap als de pagina **[!UICONTROL Media Core measurement]** wordt weergegeven.

1. (Voorwaardelijk) op de **[!UICONTROL Media Core measurement]** pagina, verkies om het gebruiken van douanevariabelen voort te zetten of verkies om oplossingsvariabelen te gebruiken.

   | Optie | Notities |
   | --- | --- |
   | Doorgaan met aangepaste variabelen | Pros en kons:<ul> <li> **Pros:** Inhoud trending blijft werken na migratie. </li> <li> **Cons:** Vereist dat u twee aangepaste eVars en drie aangepaste gebeurtenissen toewijst aan media. U kunt één aangepaste eVar en één aangepaste gebeurtenis opnieuw gebruiken. </li> </ul> Aangepaste variabelen blijven gebruiken: <ol> <li>Selecteer **[!UICONTROL Use Custom Variables,]** en klik dan **[!UICONTROL Save.]** </li> <li>Wijs desgevraagd uw huidige aangepaste gebeurtenissen en gebeurtenissen toe en klik op **[!UICONTROL Save:]** </li> </ol> |
   | Migreren naar oplossingsvariabelen | Pros en kons:<ul> <li> **Pros:** U kunt weer drie aangepaste eVars en vier aangepaste gebeurtenissen gebruiken. </li> <li> **Cons:** U verliest  **** alle historische trending en vergelijking voor media rapporten. Dit betekent dat u de weergave van inhoud of de tijd van de inhoud die wordt afgespeeld voor geen van de datums kunt veranderen voordat u naar hartslagen migreerde. </li> </ul> **Beperking:**  ga niet naar oplossingsvariabelen tenzij u zeker bent dat u deze trending niet wilt bewaren. Alle klanten zouden oplossingsvariabelen en verwerkingsregels moeten gebruiken om media gegevens in bestaande steunen en eVars te zetten, slechts als zij historische continuïteit moeten bewaren. Migreren naar oplossingvariabelen: Selecteer **[!UICONTROL Use Solution Variables]** en klik **[!UICONTROL Save].** <br><br> BELANGRIJK: Door te migreren naar oplossingsvariabelen gaat u alle  **** historische trending en vergelijking voor mediapporten verloren. |

>[!IMPORTANT]
>
>Wijzig de classificatienamen niet voor variabelen die in de Metriek en meta-gegevenstabellen (b.v. [Audio en videoparameters](/help/metrics-and-metadata/audio-video-parameters.md)) worden vermeld die daar onder Rapportage/Gereserveerde Variabele als &quot;classificatie&quot; worden beschreven. De mediaclassificaties worden gedefinieerd wanneer een rapportsuite is ingeschakeld voor het bijhouden van media. Van tijd tot tijd, voegt Adobe nieuwe eigenschappen toe, en wanneer dit voorkomt, moeten de klanten hun rapportsuites opnieuw toelaten om toegang tot de nieuwe media eigenschappen te krijgen. Tijdens het updateproces bepaalt Adobe of de classificaties worden toegelaten door de namen van de variabelen te controleren. Als een van deze ontbrekende elementen ontbreekt, voegt Adobe de ontbrekende opnieuw toe.
