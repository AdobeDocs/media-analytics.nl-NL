---
title: Nieuw foutopsporingsrapport maken
description: Leer hoe te om een nieuw Debug rapport tot stand te brengen.
uuid: 438fde3d-98f9-46d1-9672-75d204361568
exl-id: 047acf35-8c1c-4493-9ee7-e2bad47c351e
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# Nieuw rapport voor foutopsporing maken{#create-a-new-debug-report}

Een nieuw rapport voor foutopsporing maken:

1. Selecteer in [!UICONTROL Create New Debug Report] het volgende:

   ![](assets/create-new-debug-report.png)

1. Vul de velden in met de volgende informatie:

   * **Naam het Rapport** - ga de spelernaam en datum in zodat u de speler tijdens certificatie gemakkelijk kunt volgen en merken en platforms gescheiden houden.
   * **Adobe Analytics**

      * [!UICONTROL User Name] en [!UICONTROL Shared Secret] - Deze velden zijn optioneel, maar u kunt uw API-referenties voor webservices toevoegen aan Adobe Debug en zo de variabelenamen en variabeleninstellingen voor de rapportsuite weergeven.

        U kunt op een van de volgende manieren toegang krijgen:

         * [!UICONTROL Analytics > Admin > Company Settings > Web Services]
         * [!UICONTROL Analytics > Admin > User Management > Users > Individual User Settings] om een referentie van de Webdiensten API voor een nieuwe gebruiker, in [!UICONTROL User Management] tot stand te brengen, voeg de gebruiker aan de **3&rbrace; gebruikersgroep van de Toegang van de Dienst van het Web &lbrace;toe.**

      * [!UICONTROL Default Endpoint] - De gegevens in dit veld worden verstrekt door Adobe en kunnen niet worden gewijzigd.
      * [!UICONTROL Extra Endpoint] - Voeg `CNAMES` toe, als u deze gebruikt, voor bijvoorbeeld het bijhouden van de server `metrics.companyname.com`

   * **Video Heartbeats (Analytics van Media)**

      * [!UICONTROL Default Endpoint] - De gegevens in dit veld worden verstrekt door Adobe en kunnen niet worden gewijzigd.
      * [!UICONTROL Extra Endpoint] - Voeg `CNAMES` toe, als u deze gebruikt, voor uw traceringsserver, bijvoorbeeld `metrics.companyname.com` .
