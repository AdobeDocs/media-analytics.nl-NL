---
title: Profielen migreren naar de nieuwe Streaming Media-velden
description: Leer hoe u profielen kunt migreren naar de nieuwe Streaming Media-velden
feature: Streaming Media
role: User, Admin, Developer
exl-id: 0f75e594-5216-4ac1-91bd-fa89ab4b2110
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---

# Profielen migreren naar nieuwe streamingmediavelden

In dit document wordt beschreven hoe de profielfilterservice wordt gemigreerd die aanwezig is boven op de gegevensverzamelingsstromen van Adobe die zijn ingeschakeld voor Adobe Analytics voor het streamen van mediagegevens. De migratie zet de profiel het filtreren dienst van het gebruiken van het stromen van Adobe media de dienstgegevenstype genoemd &quot;Media&quot;om het nieuwe overeenkomstige gegevenstype te gebruiken genoemd &quot;[&#x200B; Media die Details &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-platform/xdm/data-types/media-reporting-details) melden.&quot;

## Profielen migreren

Om het profiel te migreren dat van het oude gegevenstype &quot;Media&quot;aan het nieuwe geroepen gegevenstype &quot;[&#x200B; Media het Melden van Details &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-platform/xdm/data-types/media-reporting-details) filtreert,&quot;moet u de bestaande profiel het filtreren regels uitgeven:

1. In Adobe Experience Platform, onder de [!UICONTROL **Bronnen**] sectie, ga naar [!UICONTROL **Dataflows**] tabel.

1. Zoek de gegevensstroom die verantwoordelijk is voor het importeren van streaming mediagegevens van Adobe Analytics naar Adobe Experience Platform via Adobe Data Collection.

1. Selecteer [!UICONTROL **dataflow van de Update**] om de profiel het filtreren opstelling te wijzigen door elke douaneregel te vervangen die een afgekeurd gebied met het nieuwe overeenkomstige gebied van het nieuwe voorwerp XDM bevat.

1. Zoek de filters die velden van het afgekeurde object Media bevatten.

1. Voeg die filters toe door velden toe te voegen van het nieuwe object &quot;Media Reporting Details&quot;.

1. Gebruik een operator OR tussen de twee velden;

1. Controleer of de profielen nog steeds naar behoren werken.

Zie de [&#x200B; parameter van identiteitskaart van de Inhoud &#x200B;](https://experienceleague.adobe.com/nl/docs/media-analytics/using/implementation/variables/audio-video-parameters#content-id) op de [&#x200B; Audio en videoparameters &#x200B;](https://experienceleague.adobe.com/nl/docs/media-analytics/using/implementation/variables/audio-video-parameters) pagina aan kaart tussen de oude gebieden en de nieuwe gebieden. Het oude veldpad kan worden gevonden onder de eigenschap &quot;XDM Field Path&quot;, terwijl het nieuwe veldpad kan worden gevonden onder de eigenschap &quot;Reporting XDM Field Path&quot;.

## Voorbeeld

Om het gemakkelijker te maken om de migratierichtlijnen te volgen, overweeg het volgende voorbeeld dataflow die één enkele profiel het filtreren regel bevat. In dit geval, aangezien er slechts één enkele regel is, moet u de migratierichtlijnen slechts eenmaal toepassen.

1. In Adobe Experience Platform, onder de [!UICONTROL **Bronnen**] sectie, ga naar [!UICONTROL **Dataflows**] tabel.

1.Zoek de gegevensstroom die verantwoordelijk is voor het importeren van streaming mediagegevens van Adobe Analytics naar Adobe Experience Platform via Adobe Analytics.

1. Selecteer **[!UICONTROL Update dataflow]** om de bewerkingsinterface in te voeren, zoals wordt weergegeven in de onderstaande afbeelding.

   ![&#x200B; AEP dataflow profiel &#x200B;](assets/aep-dataflow-profile.jpeg)

1. Selecteer **[!UICONTROL Next]** om naar het tabblad Filteren te gaan.

   ![&#x200B; AEP dataflow filterlusje &#x200B;](assets/aep-dataflow-filtering-profile.jpeg)

1. Geef op het tabblad **[!UICONTROL Filtering]** de filterregels aan die afhankelijk zijn van `media.mediaTimed` -velden.

   ![&#x200B; AEP dataflow filterregels &#x200B;](assets/dataflow-filtering-rules-profile.jpeg)


   Voor elk filter dat het media.mediaTimed voorwerp gebruikt, vind zijn correspondent in het `mediaReporting` voorwerp gebruikend de [&#x200B; Audio en videoparameters &#x200B;](https://experienceleague.adobe.com/nl/docs/media-analytics/using/implementation/variables/audio-video-parameters) pagina om tussen de oude gebieden en de nieuwe gebieden in kaart te brengen. Het oude veldpad wordt gevonden onder de eigenschap &quot;XDM Field Path&quot; terwijl het nieuwe veldpad wordt gevonden onder de eigenschap &quot;Reporting XDM Field Path&quot;. Als voorbeeld, voor [&#x200B; Media begint &#x200B;](https://experienceleague.adobe.com/nl/docs/media-analytics/using/implementation/variables/audio-video-parameters#media-starts), is de correspondent voor `media.mediaTimed.impressions.value` `mediaReporting.sessionDetails.isViewed`.

   ![&#x200B; Nieuwe en oude gebieden XDM &#x200B;](assets/xdm-fields-new-and-old.jpeg)

1. Sleep het relevante `mediaReporting` veld naar de filterregel en gebruik de operator OR tussen de twee regels. Voeg dezelfde regel toe als de bestaande regel wanneer u het nieuwe veld gebruikt.

   ![&#x200B; voeg filterregels &#x200B;](assets/add-filter-rules.jpeg) toe

1. Selecteer **[!UICONTROL Next]** om uw wijzigingen op te slaan.
