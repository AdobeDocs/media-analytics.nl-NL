---
title: Gebruikers-ID's instellen
description: API's voor het instellen van gebruikers-id's, welke server een unieke klant-id is.
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
exl-id: 6b451082-47f3-4e65-9fe0-cecb2d20dc2d
feature: "Media Analytics, API"
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 9%

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
