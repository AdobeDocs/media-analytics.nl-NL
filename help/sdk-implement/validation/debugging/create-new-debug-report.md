---
title: Nieuw rapport voor foutopsporing maken
description: Dit onderwerp beschrijft hoe te om een nieuw te creëren zuivert rapport.
uuid: 438fde3d-98f9-46d1-9672-75d204361568
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Nieuw rapport voor foutopsporing maken{#create-a-new-debug-report}

Een nieuw rapport voor foutopsporing maken:

1. Selecteer [!UICONTROL Create New Debug Report] het volgende:

   ![](assets/create-new-debug-report.png)

1. Vul de velden in met de volgende informatie:

   * **Geef het rapport** een naam: voer de naam en de datum van de speler in, zodat u de speler tijdens de certificering eenvoudig kunt volgen en merken en platforms van elkaar kunt scheiden.
   * **Adobe Analytics**

      * [!UICONTROL User Name] en [!UICONTROL Shared Secret] - Deze velden zijn optioneel, maar u kunt uw API-referenties voor webservices toevoegen aan Adobe Debug en zo de variabelenamen en variabeleninstellingen voor de rapportsuite weergeven.

         U kunt op een van de volgende manieren toegang krijgen:

         * [!UICONTROL Analytics > Admin > Company Settings > Web Services]
         * [!UICONTROL Analytics > Admin > User Management > Users > Individual User Settings] Als u een API-referentie voor webservices voor een nieuwe gebruiker wilt maken, voegt u de gebruiker toe [!UICONTROL User Management]aan de gebruikersgroep Toegang tot **** webservice.
      * [!UICONTROL Default Endpoint] - De gegevens in dit veld zijn afkomstig van Adobe en kunnen niet worden gewijzigd.
      * [!UICONTROL Extra Endpoint] - Voeg `CNAMES`, als u hen gebruikt, voor het volgen van server als toe `metrics.companyname.com`
   * **Videohartslagen (Media Analytics)**

      * [!UICONTROL Default Endpoint] - De gegevens in dit veld zijn afkomstig van Adobe en kunnen niet worden gewijzigd.
      * [!UICONTROL Extra Endpoint] - Voeg `CNAMES`, als u hen gebruikt, voor uw volgende server toe, bijvoorbeeld, `metrics.companyname.com`.



