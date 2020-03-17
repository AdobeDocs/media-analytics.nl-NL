---
title: Toepassingsacties bijhouden
description: Toepassingsacties zijn de gebeurtenissen die in uw app voorkomen en die u wilt meten.
uuid: 9cdc048a-419a-4725-bd61-6ca6d909cf10
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Toepassingsacties bijhouden{#track-app-actions}

Acties zijn de gebeurtenissen die in uw app voorkomen en die u wilt meten.

Elke actie heeft één of meerdere overeenkomstige metriek die elke keer worden verhoogd de gebeurtenis voorkomt. Bijvoorbeeld, zou u een `trackAction` vraag voor elk nieuw abonnement kunnen verzenden, of telkens als de inhoud wordt beoordeeld, of telkens als een niveau wordt voltooid.

Handelingen worden niet automatisch bijgehouden, dus roep deze aan `trackAction` wanneer een gebeurtenis plaatsvindt die u wilt bijhouden en wijs de handeling toe aan een aangepaste gebeurtenis.

1. Wanneer een gebeurtenis die u wilt volgen voorkomt, roep `trackAction`.

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

