---
title: Soorten publiek migreren naar het nieuwe Adobe Analytics-gegevenstype voor streaming media
description: Leer hoe u het publiek kunt migreren naar het nieuwe gegevenstype Adobe Analytics voor streaming media
feature: Streaming Media
role: User, Admin, Developer
exl-id: 67e67a4b-bd61-4247-93b7-261bd348d29b
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 0%

---

# Customer Journey Analytics migreren voor het gebruik van de nieuwe streamingmediavelden

Dit document beschrijft hoe een opstelling van Customer Journey Analytics die Adobe het stromen media de dienstgegevenstype genoemd &quot;Media&quot;gebruikt zou moeten worden bijgewerkt om het nieuwe overeenkomstige gegevenstype te gebruiken genoemd &quot;[&#x200B; Media die Details &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-platform/xdm/data-types/media-reporting-details) melden.&quot;

## Customer Journey Analytics migreren

Om een opstelling van Customer Journey Analytics van het oude gegevenstype te migreren genoemd &quot;Media&quot;aan het nieuwe gegevenstype genoemd &quot;[&#x200B; Media die Details &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-platform/xdm/data-types/media-reporting-details) melden,&quot;moet u de volgende montages bijwerken die het oude gegevenstype gebruiken:

* Gegevensweergaven

* Afgeleide velden

### Gegevens migreren

De gegevensweergaven migreren naar het nieuwe gegevenstype:

1. Zoek alle gegevensweergaven met het afgekeurde gegevenstype &quot;Media&quot;. Dit zijn alle velden waarvoor het pad begint met `media.mediaTimed` .

1. Voer een van de volgende handelingen uit:

   * Voeg in deze gegevensweergaven de velden in van het nieuwe gegevenstype &quot;Media Reporting Details&quot;.

   * Maak een afgeleid veld dat het nieuwe gegevenstype &quot;Media Reporting Details&quot; gebruikt als dit is ingesteld of dat terugvalt naar het oude gegevenstype &quot;Media&quot; als het gegevenstype &quot;Media Reporting Details&quot; niet is ingesteld.

### Afgeleide velden migreren

U kunt als volgt afgeleide velden migreren naar het nieuwe gegevenstype:

1. Zoek alle afgeleide velden met het afgekeurde gegevenstype &quot;Media&quot;. Dit zijn alle afgeleide velden die velden bevatten waarvan het pad begint met `media.mediaTimed` .

1. Vervang alle oude velden in het afgeleide veld door het nieuwe corresponderende veld van &quot;Media Reporting Details&quot;.

Zie de [&#x200B; parameter van identiteitskaart van de Inhoud &#x200B;](https://experienceleague.adobe.com/nl/docs/media-analytics/using/implementation/variables/audio-video-parameters#content-id) op de [&#x200B; Audio en videoparameters &#x200B;](https://experienceleague.adobe.com/nl/docs/media-analytics/using/implementation/variables/audio-video-parameters) pagina aan kaart tussen de oude gebieden en de nieuwe gebieden. Het oude veldpad wordt gevonden onder de eigenschap &quot;XDM Field Path&quot; terwijl het nieuwe veldpad wordt gevonden onder de eigenschap &quot;Reporting XDM Field Path&quot;.

![&#x200B; Oude en nieuwe XDM gebiedspaden &#x200B;](assets/field-paths-updated.jpeg)

## Voorbeeld

Om het gemakkelijker te maken om de migratierichtlijnen te volgen, overweeg het volgende voorbeeld dat een gegevensmening met gebieden van het oude verouderde &quot;Media&quot;gegevenstype bevat. In deze gegevensweergave moet u de nieuwe corresponderende velden toevoegen.

### De gegevensweergave bijwerken

U kunt een van de volgende opties gebruiken om de gegevensweergave bij te werken:

#### Optie 1

1. Zoek een metrische of een dimensie die het oude veld van het vervangen gegevenstype gebruikt.

   ![&#x200B; Oude gebiedspad in gegevensmening &#x200B;](assets/old-field-data-view.jpeg)

1. Controleer het overeenkomstige nieuwe gebied in de [&#x200B; Verschuiving van het Hoofdstuk &#x200B;](https://experienceleague.adobe.com/nl/docs/media-analytics/using/implementation/variables/chapter-parameters#chapter-offset) sectie in het [&#x200B; de parameters van het Hoofdstuk &#x200B;](https://experienceleague.adobe.com/nl/docs/media-analytics/using/implementation/variables/chapter-parameters) artikel.

1. Zoek het nieuwe corresponderende veld in de gegevensweergave.

   ![&#x200B; Nieuwe gebiedspad in gegevensmening &#x200B;](assets/new-field-data-view.jpeg)

1. Sleep het nieuwe veld naar de metrische waarde of de afmeting.

1. Herhaal dit proces voor alle metriek en afmetingen die gebieden van het afgekeurde &quot;Media&quot;gegevenstype gebruiken.

#### Optie 2

Met deze optie maakt u een afgeleid veld waarmee de waarde in het oude veld wordt geselecteerd of de waarde in het nieuwe veld op basis waarvan een waarde voor een specifieke gebeurtenis bestaat. Dit afgeleide gebied vervangt het oude &quot;Media&quot;gegevenstype in om het even welke projecten waar het wordt gebruikt.

Als u een afgeleid gebied voor de &quot;Naam van het Hoofdstuk&quot;wilt tot stand brengen die het nieuwe &quot;Media die Details&quot;gegevenstype&quot;gebruikt als het wordt geplaatst, of die terug naar het oude &quot;Media&quot;gegevenstype als het &quot;Media meldt&quot;gegevenstype niet wordt geplaatst:

1. Sleep een &quot;Geval wanneer&quot;clausule in de afgeleide gebieden.

   ![&#x200B; pas het nieuwe gebied aan om een gegevensmening &#x200B;](assets/create-derived-field2.jpeg) te creëren

1. Vul [!UICONTROL **als**] clausule gebruikend de waarde van de **Rapporterende Weg van het Gebied XDM**, zoals aangetoond in de [&#x200B; naam van het Hoofdstuk &#x200B;](https://experienceleague.adobe.com/nl/docs/media-analytics/using/implementation/variables/chapter-parameters#chapter-name) parameter op de [&#x200B; parameters van het Hoofdstuk &#x200B;](https://experienceleague.adobe.com/nl/docs/media-analytics/using/implementation/variables/chapter-parameters) pagina.

   ![&#x200B; de naam van het Hoofdstuk &#x200B;](assets/chapter-name.jpeg)

   ![&#x200B; de naam van het Hoofdstuk &#x200B;](assets/chapter-name2.jpeg)

   ![&#x200B; Voortgekomen gebiedsvoorwaarde &#x200B;](assets/derived-field-condition.jpeg)

   ![&#x200B; Voortgekomen naam van het gebiedshoofdstuk &#x200B;](assets/derived-field-chapter-name.jpeg)

1. Vul de fallback-waarde met het oude veld van het afgekeurde gegevenstype &quot;Media&quot;.

   ![&#x200B; waarde van de Fallback &#x200B;](assets/fallback-value.jpeg)

   ![&#x200B; waarde van de Fallback &#x200B;](assets/fallback-value2.jpeg)

   Dit is de definitieve definitie van het afgeleide gebied.

   ![&#x200B; Afgeleid gebied volledig &#x200B;](assets/derived-field-complete.jpeg)

1. Als u de afgeleide velden wilt bijwerken, zoekt u een afgeleid veld dat de oude vervangen velden gebruikt (pad dat begint met `media.mediaTimed`).

   ![&#x200B; afgeleid gebied &#x200B;](assets/old-derived-field.jpeg)

1. De muis over het afgeleide gebied dat u wilt bijwerken, dan selecteren [!UICONTROL **geeft**] pictogram uit.

1. Zoek alle velden van het oude gegevenstype (pad dat begint met `media.mediaTimed` ) en vervang deze door het nieuwe corresponderende veld.

   ![&#x200B; bepaal de plaats van gebied met oud gegevenstype &#x200B;](assets/locate-fields-with-old-datatype.jpeg)

1. Controleer het overeenkomstige nieuwe gebied in de [&#x200B; Naam van de Inhoud (veranderlijke) &#x200B;](https://experienceleague.adobe.com/nl/docs/media-analytics/using/implementation/variables/audio-video-parameters#content-name-variable) sectie in het [&#x200B; Streaming de parameters van Media &#x200B;](https://experienceleague.adobe.com/nl/docs/media-analytics/using/implementation/variables/audio-video-parameters#content-name-variable) artikel.

1. Vervang het oude veld door het nieuwe veld.

   ![&#x200B; Nieuw gebied &#x200B;](assets/derived-field-new.jpeg)

1. Herhaal dit proces voor alle afgeleide gebieden gebruikend gebieden van het oude vervangen &quot;Media&quot;gegevenstype.

   De migratie van de CJA-installatie is voltooid.
