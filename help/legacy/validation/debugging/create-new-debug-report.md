---
title: Nieuw foutopsporingsrapport maken
description: Leer hoe te om een nieuw Debug rapport tot stand te brengen.
uuid: 438fde3d-98f9-46d1-9672-75d204361568
exl-id: 047acf35-8c1c-4493-9ee7-e2bad47c351e
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 4%

---

# Nieuw rapport voor foutopsporing maken{#create-a-new-debug-report}

Een nieuw rapport voor foutopsporing maken:

1. In [!UICONTROL Create New Debug Report] Selecteer de volgende opties:

   ![](assets/create-new-debug-report.png)

1. Vul de velden in met de volgende informatie:

   * **Geef het rapport een naam** - Voer de naam en de datum van de speler in, zodat u de speler tijdens de certificering eenvoudig kunt volgen en merken en platforms van elkaar kunt onderscheiden.
   * **Adobe Analytics**

      * [!UICONTROL User Name] en [!UICONTROL Shared Secret] - Deze velden zijn optioneel, maar u kunt uw API-referenties voor webservices toevoegen aan Adobe Debug om de variabelenamen en variabelemontages voor de rapportsuite weer te geven.

         U kunt op een van de volgende manieren toegang krijgen:

         * [!UICONTROL Analytics > Admin > Company Settings > Web Services]
         * [!UICONTROL Analytics > Admin > User Management > Users > Individual User Settings] Als u een API-referentie voor webservices wilt maken voor een nieuwe gebruiker, kunt u [!UICONTROL User Management], voegt u de gebruiker toe aan de **Webservicetoegang** gebruikersgroep.
      * [!UICONTROL Default Endpoint] - De gegevens in dit veld worden verstrekt door Adobe en kunnen niet worden gewijzigd.
      * [!UICONTROL Extra Endpoint] - Toevoegen `CNAMES`, als u deze gebruikt, voor het bijhouden van de server als `metrics.companyname.com`
   * **Videohartslagen (Media Analytics)**

      * [!UICONTROL Default Endpoint] - De gegevens in dit veld worden verstrekt door Adobe en kunnen niet worden gewijzigd.
      * [!UICONTROL Extra Endpoint] - Toevoegen `CNAMES`, als u deze gebruikt, voor uw trackingserver, bijvoorbeeld: `metrics.companyname.com`.
