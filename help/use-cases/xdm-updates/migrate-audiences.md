---
title: Soorten publiek migreren naar het nieuwe Adobe Analytics-gegevenstype voor streaming media
description: Leer hoe u het publiek kunt migreren naar het nieuwe gegevenstype Adobe Analytics voor streaming media
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: 5664bf56-b228-430a-944c-faaab55fa108
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# Soorten publiek migreren naar nieuwe streamingmediavelden

Dit document beschrijft hoe een publiek dat gebieden van het Adobe het stromen media de dienstgegevenstype genoemd &quot;Media&quot;gebruikt zou moeten worden gemigreerd om het nieuwe overeenkomstige gegevenstype te gebruiken genoemd &quot;[&#x200B; Media die Details &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-platform/xdm/data-types/media-reporting-details) melden.&quot;

## Een publiek migreren

Om een publiek van het oude gegevenstype te migreren genoemd &quot;Media&quot;aan het nieuwe geroepen gegevenstype &quot;[&#x200B; Media die Details &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-platform/xdm/data-types/media-reporting-details) melden,&quot;u moet het publiek uitgeven en in elke regel vervangen het oude gebied van het vervangen gegevenstype met het nieuwe overeenkomstige gebied van het nieuwe gegevenstype:

1. Zoek regels met velden van het vervangen gegevenstype &quot;Media&quot;. Dit zijn alle velden die met het pad beginnen, `media.mediaTimed` .

1. Dupliceer die regels gebruikend gebieden van nieuwe &quot;[&#x200B; Media die Details &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-platform/xdm/data-types/media-reporting-details)&quot;gegevenstype melden.

1. Houd beide regels op zijn plaats tot u bevestigt dat het publiek zoals verwacht werkt.

1. Verwijder de regels die velden bevatten uit het afgekeurde gegevenstype &quot;Media&quot;.

1. Controleer of het publiek nog steeds naar behoren functioneert.

Zie de [&#x200B; parameter van identiteitskaart van de Inhoud &#x200B;](https://experienceleague.adobe.com/nl/docs/media-analytics/using/implementation/variables/audio-video-parameters#content-id) op de [&#x200B; Audio en videoparameters &#x200B;](https://experienceleague.adobe.com/nl/docs/media-analytics/using/implementation/variables/audio-video-parameters) pagina aan kaart tussen de oude gebieden en de nieuwe gebieden. Het oude veldpad wordt gevonden onder de eigenschap &quot;XDM Field Path&quot; terwijl het nieuwe veldpad wordt gevonden onder de eigenschap &quot;Reporting XDM Field Path&quot;.

![&#x200B; Oude en nieuwe XDM gebiedspaden &#x200B;](assets/field-paths-updated.jpeg)

## Voorbeeld

Om het gemakkelijker te maken om de migratierichtlijnen te volgen, overweeg het volgende voorbeeld dat een publiek met één enkele regel bevat. Omdat het publiek één regel heeft, moet u de migratierichtlijnen slechts eenmaal toepassen.

1. Selecteer [!UICONTROL **uitgeeft publiek**] knoop in de hoger-juiste hoek.

1. Bepaal de plaats van de regels die voor het publiek worden gevormd.

   ![&#x200B; geef publiek &#x200B;](assets/audience-edit.jpeg) uit

   ![&#x200B; geef publiek &#x200B;](assets/audience-edit2.jpeg) uit

1. Selecteer de regel om de configuratie te openen.

   ![&#x200B; geef publiek &#x200B;](assets/audience-edit3.jpeg) uit

1. (Optioneel) Als u het pad wilt weergeven van het veld dat in de regel wordt gebruikt, selecteert u de informatieknop bij de veldnaam.

   ![&#x200B; geef publiek &#x200B;](assets/audience-edit4.jpeg) uit

1. Identificeer de veldnaam (in dit geval &quot;Media start&quot;).

   ![&#x200B; geef publiek &#x200B;](assets/audience-edit5.jpeg) uit

1. Zie de [&#x200B; Audio en videoparameters &#x200B;](https://experienceleague.adobe.com/nl/docs/media-analytics/using/implementation/variables/audio-video-parameters) pagina aan kaart tussen de oude gebieden. Het oude veldpad kan worden gevonden onder de eigenschap &quot;XDM Field Path&quot;, terwijl het nieuwe veldpad kan worden gevonden onder de eigenschap &quot;Reporting XDM Field Path&quot;. Als voorbeeld, voor [&#x200B; begint de Media &#x200B;](https://experienceleague.adobe.com/nl/docs/media-analytics/using/implementation/variables/audio-video-parameters#media-starts) parameter, is de correspondent voor `media.mediaTimed.impressions.value` `mediaReporting.sessionDetails.isViewed`.

   ![&#x200B; Bijgewerkte weg XDM &#x200B;](assets/updated-xdm-path.jpeg)

1. Voeg dezelfde regel toe als de bestaande regel met het nieuwe veld.

   ![&#x200B; voeg regel &#x200B;](assets/add-rule.jpeg) toe

   ![&#x200B; voeg regel &#x200B;](assets/add-rule2.jpeg) toe

   ![&#x200B; voeg regel &#x200B;](assets/add-rule3.jpeg) toe

1. Selecteer [!UICONTROL **sparen**] om het publiek te bewaren. U kunt deze opstelling houden zolang u moet bevestigen dat het publiek nog werkt zoals verwacht.

1. Nadat de bevestiging volledig is, verwijder het oude gebied, dan uitgezocht [!UICONTROL **sparen**] om het publiek te bewaren.

   ![&#x200B; voeg regel &#x200B;](assets/add-rule4.jpeg) toe

1. Valideer het publiek opnieuw.

   Het doelmigratieproces is voltooid.
