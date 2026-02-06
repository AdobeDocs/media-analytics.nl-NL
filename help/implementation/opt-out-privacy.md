---
title: Uitschakelen en Privacy uitgelegd
description: Leer hoe u de optie voor aanmelding, opt-out en privacy kunt gebruiken.
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
exl-id: 64f5ef2b-7850-43d8-8f32-3d008ea4f156
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---

# Uitschakelen en privacy{#opt-out-and-privacy}

## Uitschakelen/Opt-in {#opt-out-opt-in}

U kunt bepalen of traceringsactiviteit is toegestaan op een specifiek apparaat:

* **Mobiele Apps -** de bibliotheek VA eerbiedigt de `AdobeMobile` privacy en opt-out montages van de bibliotheek. Als u het bijhouden van gegevens wilt uitschakelen, moet u de `AdobeMobile` -bibliotheek gebruiken. Voor meer informatie over de `AdobeMobile` optie-uit van de bibliotheek en privacymontages, zie [&#x200B; Opt-uit en de Montages van de Privacy &#x200B;](https://experienceleague.adobe.com/docs/mobile-services/android/gdpr-privacy-android/privacy.html).
* **JavaScript/Browser Apps -** de bibliotheek VA eerbiedigt de `VisitorAPI` privacy en optout montages. Als u het bijhouden wilt uitschakelen, moet u zich afmelden bij de service voor de Bezoeker-API. Voor verdere informatie over optout en privacy, zie [&#x200B; de Dienst van de Identiteit van Adobe Experience Platform.](https://experienceleague.adobe.com/docs/id-service/using/home.html).
* **OTT Apps (Chromecast, Roku) -** OTT SDKs verstrekt Algemene Verordening van de Bescherming van Gegevens (GDPR) - klaar APIs die u toestaan om `opt` statusvlaggen voor gegevensinzameling en transmissie te plaatsen, en lokaal opgeslagen identiteiten terug te winnen.

  >[!NOTE]
  >
  >Aanroepen voor het bijhouden van de hartslag van media worden ook uitgeschakeld als de privacystatus is ingesteld op Weigeren.

  Met de volgende instellingen kunt u bepalen of analysegegevens op een specifiek apparaat worden verzonden:

   * De instelling `privacyDefault` in het `ADBMobile.json` config-bestand. Hiermee bepaalt u de eerste instelling en gaat u door totdat deze in de code wordt gewijzigd.

   * De methode `ADBMobile().setPrivacyStatus()` .

      * **Weigeren:**

         * **Chromecast:**

           ```
           ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_OUT)
           ```

         * **Roku:**

           ```
           ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_OUT)
           ```

           >[!IMPORTANT]
           >
           >Wanneer een gebruiker het bijhouden uitschakelt, worden alle gegevens en id&#39;s van het apparaat gewist totdat de gebruiker weer inklikt.

      * **Opt terug binnen:**

         * **Chromecast:**

           ```
           ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_IN)
           ```

         * **Roku:**

           ```
           ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)
           ```

      * **terugkeer het huidige plaatsen:**

         * **Chromecast:**

           ```
           ADBMobile.config.getPrivacyStatus()
           ```

         * **Roku:**

           ```
           ADBMobile().getPrivacyStatus()
           ```

  Nadat u de privacy-instelling met `setPrivacyStatus` hebt gewijzigd, is de wijziging blijvend totdat deze opnieuw met deze methode wordt gewijzigd of de toepassing wordt verwijderd en opnieuw geïnstalleerd.

## Opgeslagen id&#39;s ophalen (OTT-apps) {#retrieving-stored-identifiers-ott-apps}

Met deze informatie kunt u lokaal opgeslagen gebruikersidentiteiten ophalen uit uw Roku-app.

>[!IMPORTANT]
>
>De methode voor het ophalen van alle id&#39;s geeft alle gebruikers-id&#39;s op die bekend zijn bij en die door de SDK blijven bestaan. U moet deze methode **roepen alvorens** een gebruiker uit opteert.

De lokaal opgeslagen identiteiten worden geretourneerd in een JSON-tekenreeks, die het volgende kan bevatten:

* Bedrijfcontext - IMS-organisatie-id&#39;s
* Gebruikersnamen
* Experience Cloud-id (MCID)
* Source-id&#39;s voor gegevens (DPID, DPUUID)
* Analyse-id&#39;s (AVID, AID, VID en bijbehorende RSID&#39;s)
* Audience Manager-id (UUID)

Bijvoorbeeld:

* **Chromecast:**

  ```
  ADBMobile.config.getAllIdentifiersAsync(callback)
  ```

* **Roku:**

  ```
  vids = ADBMobile().getAllIdentifiers()
  ```
