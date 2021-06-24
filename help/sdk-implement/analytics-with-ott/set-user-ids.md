---
title: Gebruikers-ID's instellen
description: API's voor het instellen van gebruikers-id's, welke server een unieke klant-id is.
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
exl-id: 6b451082-47f3-4e65-9fe0-cecb2d20dc2d
feature: '"Media Analytics, API"'
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 8%

---

# Gebruikers-id&#39;s instellen{#set-user-ids}

De gebruikers-id is een unieke aangepaste bezoeker-id die door de toepassing voor een gebruiker is gedefinieerd.

Stel de unieke gebruikers-id in de SDK van ADBMobile in en ontvang deze als volgt:

* **Instellen:**

   * **Roku:**

      ```
      ADBMobile().setUserIdentifer("app-generated-unique-id")
      ```

   * **Chromecast:**

      ```
      ADBMobile().config.setUserIdentifer("app-generated-unique-id");
      ```

* **Ophalen:**

   * **Roku:**

      ```
      vid = ADBMobile().userIdentifer()
      ```

   * **Chromecast:**

      ```
      vid = ADBMobile().config.getUserIdentifer();
      ```
