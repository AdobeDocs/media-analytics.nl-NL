---
title: Uitschakelen en privacy
description: Optie-in, opt-out en privacy afhandelen.
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Uitschakelen en privacy{#opt-out-and-privacy}

## Uitschakelen/Opt-in {#opt-out-opt-in}

U kunt bepalen of traceringsactiviteit is toegestaan op een specifiek apparaat:

* **Mobiele apps -** De VA-bibliotheek respecteert de privacy- en opt-out-instellingen van de `AdobeMobile` bibliotheek. Als u de optie wilt uitschakelen, moet u de `AdobeMobile` bibliotheek gebruiken. Zie `AdobeMobile` Afmelden en Privacy-instellingen [voor meer informatie over de instellingen voor weigeren en privacy van de](https://docs.adobe.com/content/help/en/mobile-services/android/gdpr-privacy-android/privacy.html)bibliotheek.
* **JavaScript-/browsertoepassingen -** De VA-bibliotheek respecteert de privacy- en `VisitorAPI` optoutinstellingen. Als u het bijhouden wilt uitschakelen, moet u zich afmelden bij de service voor de Bezoeker-API. Zie [Adobe Experience Platform Identity Service voor meer informatie over plug-out en privacy.](https://marketing.adobe.com/resources/help/en_US/mcvid/).
* **OTT Apps (Chromecast, Roku) -** `opt` De OTT SDKs verstrekken algemene de regelgevende (GDPR) - klaar APIs van de Bescherming van Gegevens die u toestaan om statusvlaggen voor gegevensinzameling en transmissie te plaatsen, en lokaal opgeslagen identiteiten terug te winnen.

   >[!NOTE]
   >
   >Aanroepen voor het bijhouden van de hartslag van media worden ook uitgeschakeld als de privacystatus is ingesteld op Weigeren.

   Met de volgende instellingen kunt u bepalen of analysegegevens op een specifiek apparaat worden verzonden:

   * De `privacyDefault` instelling in het `ADBMobile.json` configuratiebestand. Hiermee bepaalt u de eerste instelling en gaat u door totdat deze in de code wordt gewijzigd.

   * De `ADBMobile().setPrivacyStatus()` methode.

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

      * **Opnieuw aanmelden:**

         * **Chromecast:**

            ```
            ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_IN)
            ```

         * **Roku:**

            ```
            ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)
            ```
      * **Retourneer de huidige instelling:**

         * **Chromecast:**

            ```
            ADBMobile.config.getPrivacyStatus()
            ```

         * **Roku:**

            ```
            ADBMobile().getPrivacyStatus()
            ```
   Nadat u de privacyinstelling hebt gewijzigd met `setPrivacyStatus`deze methode, is de wijziging permanent totdat deze opnieuw wordt gewijzigd of totdat de toepassing wordt verwijderd en opnieuw wordt geïnstalleerd.

## Opgeslagen id&#39;s ophalen (OTT-apps) {#retrieving-stored-identifiers-ott-apps}

Met deze informatie kunt u lokaal opgeslagen gebruikersidentiteiten ophalen uit uw Roku-app.

>[!IMPORTANT]
>
>De methode om alle herkenningstekens terug te winnen krijgt alle die gebruikersidentiteiten door SDK worden gekend en worden voortgeduurd. U moet deze methode aanroepen **voordat** een gebruiker de functie uitschakelt.

De lokaal opgeslagen identiteiten worden geretourneerd in een JSON-tekenreeks, die het volgende kan bevatten:

* Bedrijfcontext - IMS-organisatie-id&#39;s
* Gebruikersnamen
* Experience Cloud ID (MCID)
* Gegevensbron-id&#39;s (DPID, DPUUID)
* Analytische id&#39;s (AVID, AID, VID en bijbehorende RSID&#39;s)
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

