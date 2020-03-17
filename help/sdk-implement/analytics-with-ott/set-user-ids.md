---
title: Gebruikers-id's instellen
description: API's voor het instellen van gebruikers-id's, welke server een unieke klant-id is.
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

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
