---
title: Toepassingshandelingen bijhouden
description: Toepassingsacties zijn de gebeurtenissen die in uw app voorkomen en die u wilt meten.
uuid: 9cdc048a-419a-4725-bd61-6ca6d909cf10
exl-id: 88b7d540-67b7-4ec1-8273-02e34853bf60
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---

# Toepassingsacties bijhouden{#track-app-actions}

Acties zijn de gebeurtenissen die in uw app voorkomen en die u wilt meten.

Elke actie heeft één of meerdere overeenkomstige metriek die elke keer worden verhoogd de gebeurtenis voorkomt. U kunt bijvoorbeeld een `trackAction` oproep voor elk nieuw abonnement verzenden, telkens wanneer inhoud wordt beoordeeld of telkens wanneer een niveau wordt voltooid.

Handelingen worden niet automatisch bijgehouden, dus roep `trackAction` aan wanneer een gebeurtenis plaatsvindt die u wilt bijhouden en wijs de handeling toe aan een aangepaste gebeurtenis.

1. Roep `trackAction` aan wanneer een gebeurtenis die u wilt bijhouden plaatsvindt.

   * **Roku:**

     ```js
     ADBMobile().trackAction("myapp.ActionName", {})
     ```

   * **Chromecast:**

     ```js
     ADBMobile.analytics.trackAction("myapp.ActionName", {});
     ```

1. Wijs de handeling toe aan een aangepaste gebeurtenis.

   * **Roku:**

     ```js
     dictionary = {} 
     dictionary["myapp.social.SocialSource"] = "Twitter"  
     ADBMobile().trackAction("myapp.SocialShare", dictionary)
     ```

   * **Chromecast:**

     ```js
     var dictionary = {}; 
     dictionary["myapp.social.SocialSource"] = "Twitter"; 
     ADBMobile.analytics.trackAction("myapp.SocialShare", dictionary);
     ```

U kunt ook aanvullende contextgegevens verzenden met elke aanroep van de trackactie.
