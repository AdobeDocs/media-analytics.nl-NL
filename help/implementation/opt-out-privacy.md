---
title: Uitschakelen en Privacy uitgelegd
description: Leer hoe u de optie voor aanmelding, opt-out en privacy kunt gebruiken.
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
exl-id: 64f5ef2b-7850-43d8-8f32-3d008ea4f156
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 1%

---

# Uitschakelen en privacy{#opt-out-and-privacy}

## Uitschakelen/Opt-in {#opt-out-opt-in}

U kunt bepalen of traceringsactiviteit is toegestaan op een specifiek apparaat:

* **Mobiele apps -** De VA-bibliotheek eerbiedigt de `AdobeMobile` de privacy- en opt-outinstellingen van de bibliotheek. Als u niet wilt bijhouden, moet u de opdracht `AdobeMobile` bibliotheek. Voor meer informatie over de `AdobeMobile` de optie om te weigeren en privacy-instellingen van de bibliotheek, raadpleegt u [Instellingen voor Weigeren en Privacy](https://experienceleague.adobe.com/docs/mobile-services/android/gdpr-privacy-android/privacy.html?lang=nl-NL).
* **JavaScript-/browsertoepassingen -** De VA-bibliotheek eerbiedigt de `VisitorAPI` privacy- en optout-instellingen. Als u het bijhouden wilt uitschakelen, moet u zich afmelden bij de service voor de Bezoeker-API. Voor meer informatie over optout en privacy raadpleegt u [Adobe Experience Platform Identity Service.](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=nl-NL).
* **OTT-apps (Chromecast, Roku) -** De OTT SDK&#39;s bieden API&#39;s die geschikt zijn voor algemene gegevensbeschermingsregels (General Data Protection Regulation, GDPR), waarmee u de volgende instellingen kunt instellen `opt` statusvlaggen voor gegevensinzameling en transmissie, en om lokaal opgeslagen identiteiten terug te winnen.

   >[!NOTE]
   >
   >Aanroepen voor het bijhouden van de hartslag van media worden ook uitgeschakeld als de privacystatus is ingesteld op Weigeren.

   Met de volgende instellingen kunt u bepalen of analysegegevens op een specifiek apparaat worden verzonden:

   * De `privacyDefault` in het dialoogvenster `ADBMobile.json` configuratiebestand. Hiermee bepaalt u de eerste instelling en gaat u door totdat deze in de code wordt gewijzigd.

   * De `ADBMobile().setPrivacyStatus()` methode.

      * **Weigeren:**

         * **Chromecast:**

                &quot;
                ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_OUT)
                &quot;
            
         * **Roku:**

                &quot;
                ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_OUT)
                &quot;
            
            >[!IMPORTANT]
            >
            >Wanneer een gebruiker het bijhouden uitschakelt, worden alle gegevens en id&#39;s van het apparaat gewist totdat de gebruiker weer inklikt.
      * **Opnieuw aanmelden:**

         * **Chromecast:**

                &quot;
                ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_IN)
                &quot;
            
         * **Roku:**

                &quot;
                ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)
                &quot;
            * **Retourneer de huidige instelling:**

         * **Chromecast:**

                &quot;
                ADBMobile.config.getPrivacyStatus()
                &quot;
            
         * **Roku:**

                &quot;
                ADBMobile().getPrivacyStatus()
                &quot;
            Nadat u de privacyinstelling hebt gewijzigd met `setPrivacyStatus`, is de wijziging permanent totdat deze opnieuw wordt gewijzigd met deze methode, of de toepassing wordt verwijderd en opnieuw geïnstalleerd.

## Opgeslagen id&#39;s ophalen (OTT-apps) {#retrieving-stored-identifiers-ott-apps}

Met deze informatie kunt u lokaal opgeslagen gebruikersidentiteiten ophalen uit uw Roku-app.

>[!IMPORTANT]
>
>De methode om alle herkenningstekens terug te winnen krijgt alle die gebruikersidentiteiten door SDK worden gekend en worden voortgeduurd. U moet deze methode aanroepen **voor** een gebruiker kiest uit.

De lokaal opgeslagen identiteiten worden geretourneerd in een JSON-tekenreeks, die het volgende kan bevatten:

* Bedrijfcontext - IMS-organisatie-id&#39;s
* Gebruikersnamen
* Experience Cloud-id (MCID)
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
