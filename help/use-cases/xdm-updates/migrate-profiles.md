---
title: Profielen migreren naar de nieuwe Streaming Media-velden
description: Leer hoe u profielen kunt migreren naar de nieuwe Streaming Media-velden
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: 0f75e594-5216-4ac1-91bd-fa89ab4b2110
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---

# Profielen migreren naar nieuwe streamingmediavelden

In dit document wordt beschreven hoe de profielfilterservice wordt gemigreerd die aanwezig is boven op de gegevensverzamelingsstromen van Adobe die zijn ingeschakeld voor Adobe Analytics voor het streamen van mediagegevens. De migratie zet de profiel het filtreren dienst van het gebruiken van het stromen van Adobe media de dienstgegevenstype genoemd &quot;Media&quot;om het nieuwe overeenkomstige gegevenstype te gebruiken genoemd &quot;[ Media die Details ](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) melden.&quot;

## Profielen migreren

Om het profiel te migreren dat van het oude gegevenstype &quot;Media&quot;aan het nieuwe geroepen gegevenstype &quot;[ Media het Melden van Details ](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) filtreert,&quot;moet u de bestaande profiel het filtreren regels uitgeven:

1. In Adobe Experience Platform, onder de [!UICONTROL **Bronnen**] sectie, ga naar [!UICONTROL **Dataflows**] tabel.

1. Zoek de gegevensstroom die verantwoordelijk is voor het importeren van streaming mediagegevens van Adobe Analytics naar Adobe Experience Platform via Adobe Data Collection.

1. Selecteer [!UICONTROL **dataflow van de Update**] om de profiel het filtreren opstelling te wijzigen door elke douaneregel te vervangen die een afgekeurd gebied met het nieuwe overeenkomstige gebied van het nieuwe voorwerp XDM bevat.

1. Zoek de filters die velden van het afgekeurde object Media bevatten.

1. Voeg die filters toe door velden toe te voegen van het nieuwe object &quot;Media Reporting Details&quot;.

1. Gebruik een operator OR tussen de twee velden;

1. Controleer of de profielen nog steeds naar behoren werken.

Zie de [ parameter van identiteitskaart van de Inhoud ](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/audio-video-parameters#content-id) op de [ Audio en videoparameters ](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/audio-video-parameters) pagina aan kaart tussen de oude gebieden en de nieuwe gebieden. Het oude veldpad kan worden gevonden onder de eigenschap &quot;XDM Field Path&quot;, terwijl het nieuwe veldpad kan worden gevonden onder de eigenschap &quot;Reporting XDM Field Path&quot;.

## Voorbeeld

Om het gemakkelijker te maken om de migratierichtlijnen te volgen, overweeg het volgende voorbeeld dataflow die één enkele profiel het filtreren regel bevat. In dit geval, aangezien er slechts één enkele regel is, moet u de migratierichtlijnen slechts eenmaal toepassen.

1. In Adobe Experience Platform, onder de [!UICONTROL **Bronnen**] sectie, ga naar [!UICONTROL **Dataflows**] tabel.

1.Zoek de gegevensstroom die verantwoordelijk is voor het importeren van streaming mediagegevens van Adobe Analytics naar Adobe Experience Platform via Adobe Analytics.

1. Selecteer **[!UICONTROL Update dataflow]** om de bewerkingsinterface in te voeren, zoals wordt weergegeven in de onderstaande afbeelding.

   ![ AEP dataflow profiel ](assets/aep-dataflow-profile.jpeg)

1. Selecteer **[!UICONTROL Next]** om naar het tabblad Filteren te gaan.

   ![ AEP dataflow filterlusje ](assets/aep-dataflow-filtering-profile.jpeg)

1. Geef op het tabblad **[!UICONTROL Filtering]** de filterregels aan die afhankelijk zijn van `media.mediaTimed` -velden.

   ![ AEP dataflow filterregels ](assets/dataflow-filtering-rules-profile.jpeg)


   Voor elk filter dat het media.mediaTimed voorwerp gebruikt, vind zijn correspondent in het `mediaReporting` voorwerp gebruikend de [ Audio en videoparameters ](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/audio-video-parameters) pagina om tussen de oude gebieden en de nieuwe gebieden in kaart te brengen. Het oude veldpad wordt gevonden onder de eigenschap &quot;XDM Field Path&quot; terwijl het nieuwe veldpad wordt gevonden onder de eigenschap &quot;Reporting XDM Field Path&quot;. Als voorbeeld, voor [ Media begint ](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/audio-video-parameters#media-starts), is de correspondent voor `media.mediaTimed.impressions.value` `mediaReporting.sessionDetails.isViewed`.

   ![ Nieuwe en oude gebieden XDM ](assets/xdm-fields-new-and-old.jpeg)

1. Sleep het relevante `mediaReporting` veld naar de filterregel en gebruik de operator OR tussen de twee regels. Voeg dezelfde regel toe als de bestaande regel wanneer u het nieuwe veld gebruikt.

   ![ voeg filterregels ](assets/add-filter-rules.jpeg) toe

1. Selecteer **[!UICONTROL Next]** om uw wijzigingen op te slaan.
