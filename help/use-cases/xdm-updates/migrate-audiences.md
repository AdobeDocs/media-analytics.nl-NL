---
title: Soorten publiek migreren naar het nieuwe Adobe Analytics-gegevenstype voor streaming media
description: Leer hoe u het publiek kunt migreren naar het nieuwe gegevenstype Adobe Analytics voor streaming media
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 19e729c7d87b4e81b6952c7ebcb8b122043d516d
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# Soorten publiek migreren naar de nieuwe streamingmediavelden

Dit document beschrijft hoe een publiek dat gebieden van het Adobe het stromen gegevenstype van de Inzameling van Media van de Inzameling genoemd &quot;Media&quot;gebruikt zou moeten worden gemigreerd om het nieuwe overeenkomstige gegevenstype te gebruiken genoemd &quot;[ Media die Details ](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) melden.&quot;

## Een publiek migreren

Om een publiek van het oude gegevenstype te migreren genoemd &quot;Media&quot;aan het nieuwe geroepen gegevenstype &quot;[ Media die Details ](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) melden,&quot;u moet het publiek uitgeven en in elke regel vervangen het oude gebied van het vervangen gegevenstype met het nieuwe overeenkomstige gebied van het nieuwe gegevenstype:

1. Zoek regels met velden van het vervangen gegevenstype &quot;Media&quot;. Dit zijn alle velden die met het pad beginnen, `media.mediaTimed` .

1. Dupliceer die regels gebruikend gebieden van nieuwe &quot;[ Media die Details ](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)&quot;gegevenstype melden.

1. Houd beide regels op zijn plaats tot u bevestigt dat het publiek zoals verwacht werkt.

1. Verwijder de regels die velden bevatten uit het afgekeurde gegevenstype &quot;Media&quot;.

1. Controleer of het publiek nog steeds naar behoren functioneert.

Zie de [ parameter van identiteitskaart van de Inhoud ](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/audio-video-parameters#content-id) op de [ Audio en videoparameters ](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/audio-video-parameters) pagina aan kaart tussen de oude gebieden en de nieuwe gebieden. Het oude veldpad wordt gevonden onder de eigenschap &quot;XDM Field Path&quot; terwijl het nieuwe veldpad wordt gevonden onder de eigenschap &quot;Reporting XDM Field Path&quot;.

![ Oude en nieuwe XDM gebiedspaden ](assets/field-paths-updated.jpeg)

## Voorbeeld

Om het gemakkelijker te maken om de migratierichtlijnen te volgen, overweeg het volgende voorbeeld dat een publiek met één enkele regel bevat. Omdat het publiek één regel heeft, moet u de migratierichtlijnen slechts eenmaal toepassen.

1. Selecteer [!UICONTROL **uitgeeft publiek**] knoop in de hoger-juiste hoek.

1. Bepaal de plaats van de regels die voor het publiek worden gevormd.

   ![ geef publiek ](assets/audience-edit.jpeg) uit

   ![ geef publiek ](assets/audience-edit2.jpeg) uit

1. Selecteer de regel om de configuratie te openen.

   ![ geef publiek ](assets/audience-edit3.jpeg) uit

1. (Optioneel) Als u het pad wilt weergeven van het veld dat in de regel wordt gebruikt, selecteert u de informatieknop bij de veldnaam.

   ![ geef publiek ](assets/audience-edit4.jpeg) uit

1. Identificeer de veldnaam (in dit geval &quot;Media start&quot;).

   ![ geef publiek ](assets/audience-edit5.jpeg) uit

1. Zie de [ Audio en videoparameters ](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/audio-video-parameters) pagina aan kaart tussen de oude gebieden. Het oude veldpad kan worden gevonden onder de eigenschap &quot;XDM Field Path&quot;, terwijl het nieuwe veldpad kan worden gevonden onder de eigenschap &quot;Reporting XDM Field Path&quot;. Als voorbeeld, voor [ begint de Media ](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/audio-video-parameters#media-starts) parameter, is de correspondent voor `media.mediaTimed.impressions.value` `mediaReporting.sessionDetails.isViewed`.

   ![ Bijgewerkte weg XDM ](assets/updated-xdm-path.jpeg)

1. Voeg dezelfde regel toe als de bestaande regel met het nieuwe veld.

   ![ voeg regel ](assets/add-rule.jpeg) toe

   ![ voeg regel ](assets/add-rule2.jpeg) toe

   ![ voeg regel ](assets/add-rule3.jpeg) toe

1. Selecteer [!UICONTROL **sparen**] om het publiek te bewaren. U kunt deze opstelling houden zolang u moet bevestigen dat het publiek nog werkt zoals verwacht.

1. Nadat de bevestiging volledig is, verwijder het oude gebied, dan uitgezocht [!UICONTROL **sparen**] om het publiek te bewaren.

   ![ voeg regel ](assets/add-rule4.jpeg) toe

1. Valideer het publiek opnieuw.

   Het doelmigratieproces is voltooid.
