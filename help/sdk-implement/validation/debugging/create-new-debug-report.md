---
title: Nieuw foutopsporingsrapport maken
description: Leer hoe te om een nieuw Debug rapport tot stand te brengen.
uuid: 438fde3d-98f9-46d1-9672-75d204361568
exl-id: 047acf35-8c1c-4493-9ee7-e2bad47c351e
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 4%

---

# Nieuw rapport voor foutopsporing maken{#create-a-new-debug-report}

Een nieuw rapport voor foutopsporing maken:

1. Selecteer in [!UICONTROL Create New Debug Report] het volgende:

   ![](assets/create-new-debug-report.png)

1. Vul de velden in met de volgende informatie:

   * **Geef het rapport**  een naam: voer de naam en de datum van de speler in, zodat u de speler tijdens de certificering eenvoudig kunt volgen en merken en platforms van elkaar kunt scheiden.
   * **Adobe Analytics**

      * [!UICONTROL User Name] en  [!UICONTROL Shared Secret] - Deze velden zijn optioneel, maar u kunt uw API-referenties voor webservices toevoegen aan Adobe Debug om de variabelenamen en variabelemontages voor de rapportsuite weer te geven.

         U kunt op een van de volgende manieren toegang krijgen:

         * [!UICONTROL Analytics > Admin > Company Settings > Web Services]
         * [!UICONTROL Analytics > Admin > User Management > Users > Individual User Settings] Als u een API-referentie voor webservices voor een nieuwe gebruiker wilt maken, voegt u de gebruiker toe  [!UICONTROL User Management]aan de gebruikersgroep  **Webservice** Accessuser.
      * [!UICONTROL Default Endpoint] - De gegevens in dit veld worden verstrekt door Adobe en kunnen niet worden gewijzigd.
      * [!UICONTROL Extra Endpoint] - Voeg  `CNAMES`, als u hen gebruikt, voor het volgen van server als toe  `metrics.companyname.com`
   * **Videohartslagen (Media Analytics)**

      * [!UICONTROL Default Endpoint] - De gegevens in dit veld worden verstrekt door Adobe en kunnen niet worden gewijzigd.
      * [!UICONTROL Extra Endpoint] - Voeg  `CNAMES`, als u hen gebruikt, voor uw volgende server toe, bijvoorbeeld,  `metrics.companyname.com`.
