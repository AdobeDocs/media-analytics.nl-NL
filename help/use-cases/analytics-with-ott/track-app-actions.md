---
title: App-acties bijhouden
description: Toepassingsacties zijn de gebeurtenissen die in uw app voorkomen en die u wilt meten.
uuid: 9cdc048a-419a-4725-bd61-6ca6d909cf10
exl-id: 88b7d540-67b7-4ec1-8273-02e34853bf60
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 3%

---

# Toepassingsacties bijhouden{#track-app-actions}

Acties zijn de gebeurtenissen die in uw app voorkomen en die u wilt meten.

Elke actie heeft één of meerdere overeenkomstige metriek die elke keer worden verhoogd de gebeurtenis voorkomt. U kunt bijvoorbeeld een `trackAction` vraag voor elk nieuw abonnement, of telkens als de inhoud wordt beoordeeld, of telkens als een niveau wordt voltooid.

Handelingen worden niet automatisch bijgehouden, dus roep `trackAction` wanneer een gebeurtenis plaatsvindt die u wilt volgen, en de actie aan een douanegebeurtenis in kaart brengen.

1. Wanneer een gebeurtenis die u wilt volgen voorkomt, roept `trackAction`.

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
