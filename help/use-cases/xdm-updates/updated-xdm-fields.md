---
title: Update een analytische bronschakelaarimplementatie aan nieuwe gebieden XDM voor het stromen de media diensten
description: Meer informatie over het migreren van een analytische bronverbindingsimplementatie naar bijgewerkte XDM Streaming Media-velden
feature: Streaming Media
role: User, Admin, Developer
exl-id: d239b203-71ce-4307-884f-9d11cc623d04
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 0%

---

# Update een analytische bronschakelaarimplementatie aan nieuwe gebieden XDM voor het stromen de media diensten

>[!NOTE]
>
>Deze informatie is voorgenomen voor organisaties die de [ bron van Analytics schakelaar ](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/analytics) gebruiken om het stromen media gegevens van Adobe Analytics in Adobe Experience Platform voor gebruik met Customer Journey Analytics te brengen rapporterend of een andere dienst van het Platform.
>
>De wijzigingen hebben geen invloed op Adobe Analytics als zelfstandige toepassing, zoals gegevensverzameling, -verwerking en -rapportage. Gereedschappen zoals Gegevensfeeds en Verwerkingsregels blijven ongewijzigd, zodat de implementatie van Analytics niet hoeft te worden bijgewerkt.

Er is nu een nieuwe Adobe Data Collection-implementatie (de bronconnector van Analytics) beschikbaar voor de streaming-mediaservice die van de ene set XDM-velden naar een andere migreert.

## Nieuw XDM-veldpad

Als onderdeel van deze migratie is het `mediaReporting` XDM-veldpad toegevoegd aan de XDM-schema&#39;s die worden gebruikt in de gegevensverzamelingsstromen van Adobe (de bronconnector van Analytics). Dit nieuwe veld wordt automatisch toegevoegd aan een bestaand en nieuw gegenereerd schema voor Adobe-gegevensverzameling.

## Vervanging van het oude XDM-veldpad

Alle gegevensverzamelingsstromen van Adobe (de bronschakelaar van de Analyse) die streaming media gegevens van Adobe Analytics naar Adobe Experience Platform overbrengen verzenden momenteel zowel gegevens over het nieuwe `mediaReporting` XDM gebiedspad als het oude `media.mediaTimed` XDM gebiedspad. Beide veldpaden zullen drie maanden beschikbaar zijn, tot eind oktober 2025. Na oktober worden de velden `media.mediaTimed` volledig vervangen en bevatten de gegevens die na oktober worden ingevoerd alleen `mediaReporting` . Na de veroudering zijn de `media.mediaTimed` -velden niet meer zichtbaar in de gebruikersinterface van het Adobe Experience Platform-schema en wordt de gegevensinvoer in deze velden stopgezet. Deze velden zijn dan ook niet meer beschikbaar voor gebruik in Adobe Experience Platform-services.

Gegevens die vóór deze datum zijn ingevoerd, blijven beschikbaar voor rapportage.

## Aanvullende verschillen met het nieuwe XDM-veldpad

Met de nieuwe Adobe bronschakelaarimplementatie voor het stromen media, houd-levende vraag van Adobe Analytics nu wordt opgenomen in Adobe Experience Platform.

Eerder waren deze oproepen niet terug te vinden in platformapps zoals Customer Journey Analytics. Dientengevolge, zou uw organisatie de volgende verschillen in rapportering kunnen waarnemen:

* **Nauwkeurige zittingsaantallen**: In sommige gevallen, zou dit deflatie in zittingsaantallen kunnen betekenen, omdat houden-levende vraag de hulp actieve gebruikerszittingen zelfs in afwezigheid van directe media interactie handhaaft. Deze houden-levende vraag wordt geproduceerd om de 20 minuten na de laatste gebeurtenis, per media playback, met de bedoeling om het bezoek open te houden. Om een optimale sessietracering in Customer Journey Analytics te garanderen, wordt aangeraden de vervaldatum van het bezoek in de gegevensweergave in te stellen op 30 minuten.

* **een verhoging van het aantal gebeurtenissen**: Omdat houden-levende vraag nu in metrische Gebeurtenissen van Customer Journey Analytics wordt geteld. Als u wilt houden-levende vraag van het melden uitsluiten, kunt u een filter tot stand brengen die gebeurtenissen uitsluiten die het Type van Gebeurtenis van `media.keepalive` hebben.

Deze wijziging zorgt voor een betere afstemming tussen de rapportage van Analytics en CJA.

## Bestaande instellingen migreren

Voor een soepele overgang moeten alle klanten vóór eind oktober 2025 bestaande instellingen migreren van `media.mediaTimed` -velden naar `mediaReporting` -velden. De betrokken gebieden zijn die gebieden die afhankelijk zijn van `media.mediaTimed` gebruik, en zij zouden moeten worden gemigreerd zoals die in de volgende secties worden beschreven.

### Customer Journey Analytics**

Er zijn twee manieren waarop CJA-rapporten kunnen worden gemigreerd:

>[!NOTE]
>
>Nadat u een van de volgende opties hebt gekozen, moet u elk `media.mediaTimed` -veld dat in Customer Journey Analytics-rapporten wordt gebruikt, handmatig vervangen door het corresponderende afgeleide veld of XDM-veldpad rapporteren.

* **om historische gegevens** te behouden: De teams van Adobe hebben een vooraf bepaald malplaatje van Customer Journey Analytics ontwikkeld dat een reeks afgeleide gebieden introduceert die de oude en nieuwe gebieden XDM in één enkel gebied combineren. Deze sjabloon kan op verzoek per Customer Journey Analytics-verbinding worden ingeschakeld. Neem contact op met het Adobe-ondersteuningsteam om u te helpen bij het inschakelen van de nieuwe velden. Deze afgeleide gebieden tellen niet naar de afgeleide gebiedsgrens van uw organisatie.

  Om een lijst van afbeeldingen te bekijken, zie [ de parameterafbeelding van Analytics van Media voor Adobe Experience Platform en Customer Journey Analytics ](/help/use-cases/xdm-updates/parameters-mapping.md).

* **als het historische gegeven niet wordt vereist**: Het is voldoende om het Rapporterende Weg van het Gebied XDM bij het melden van tijd te gebruiken. Voor meer informatie, zie [ Customer Journey Analytics migreren om de nieuwe het stromen media gebieden ](/help/use-cases/xdm-updates/migrate-cja-setup.md) te gebruiken.

### Real-Time CDP

Alle soorten publiek en profielen moeten zijn gebaseerd op `mediaReporting` . Voor meer informatie, zie [ profielen aan de nieuwe het stromen media gebieden ](/help/use-cases/xdm-updates/migrate-profiles.md) migreren.

### Gegevensstroom en gegevensverzameling

Dynamische configuraties en gegevenstoewijzing moeten `mediaReporting` gebruiken. Voor meer informatie, zie [ Prep van Gegevens voor douanegebieden aan de nieuwe het stromen media gebieden ](/help/use-cases/xdm-updates/migrate-dataprep.md) migreren.

### Overige diensten die moeten worden gemigreerd

* Adobe Journey Optimizer: Campagne- en reisconfiguraties moeten `mediaReporting` bevatten.

* Gebeurtenis doorsturen: alleen `mediaReporting` velden moeten in configuraties worden opgenomen.

* Query Services: query&#39;s moeten verwijzen naar `mediaReporting` -velden.

* Tagconfiguraties: instellingen voor codering moeten verwijzen naar `mediaReporting` -velden.

* Verbindingen en bestemmingen: de invoer en de uitvoer gegevensstromen zouden rond `mediaReporting` gebieden moeten worden gestructureerd.

Houd er rekening mee dat elke andere stroom die afhankelijk is van `media.mediaTimed` -velden wordt beïnvloed en dat logische updates zijn vereist.

## Volgende stappen en ondersteuning

Alle klanten die Adobe-gegevensverzameling voor streamingmedia gebruiken, moeten hun migratie binnen de opgegeven overgangsperiode voltooien.

Neem voor vragen of ondersteuningsbehoeften contact op met het Adobe-ondersteuningsteam.
