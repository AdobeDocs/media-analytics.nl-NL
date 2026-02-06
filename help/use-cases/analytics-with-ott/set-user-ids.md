---
title: Gebruikersnaam instellen
description: API's voor het instellen van gebruikers-id's, welke server een unieke klant-id is.
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
exl-id: 6b451082-47f3-4e65-9fe0-cecb2d20dc2d
feature: "Streaming Media, API"
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 0%

---

# Gebruikers-id&#39;s instellen{#set-user-ids}

De gebruikers-id is een unieke aangepaste bezoeker-id die door de toepassing voor een gebruiker is gedefinieerd.

Stel de unieke gebruikersnaam als volgt in op de ADBMobile SDK en krijg deze als volgt:

* **Reeks:**

   * **Roku:**

     ```
     ADBMobile().setUserIdentifer("app-generated-unique-id")
     ```

   * **Chromecast:**

     ```
     ADBMobile().config.setUserIdentifer("app-generated-unique-id");
     ```

* **krijgt:**

   * **Roku:**

     ```
     vid = ADBMobile().userIdentifer()
     ```

   * **Chromecast:**

     ```
     vid = ADBMobile().config.getUserIdentifer();
     ```
