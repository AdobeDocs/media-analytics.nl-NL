---
title: '"Uitschakelen en Privacy uitgelegd"'
description: '"Leer hoe u kunt werken met opt-in, opt-out en privacy."'
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
exl-id: 64f5ef2b-7850-43d8-8f32-3d008ea4f156
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 1%

---

# Uitschakelen en privacy{#opt-out-and-privacy}

## Uitschakelen/Opt-in {#opt-out-opt-in}

U kunt bepalen of traceringsactiviteit is toegestaan op een specifiek apparaat:

* **Mobiele apps -** De VA-bibliotheek respecteert de privacy- en opt-out-instellingen van de  `AdobeMobile` bibliotheek. Als u niet wilt bijhouden, moet u de bibliotheek `AdobeMobile` gebruiken. Zie [Opt-Out- en Privacy-instellingen](https://experienceleague.adobe.com/docs/mobile-services/android/gdpr-privacy-android/privacy.html) voor meer informatie over de `AdobeMobile`-instellingen van de bibliotheek.
* **JavaScript-/browsertoepassingen -** De VA-bibliotheek respecteert de instellingen voor  `VisitorAPI` privacy en optout. Als u het bijhouden wilt uitschakelen, moet u zich afmelden bij de service voor de Bezoeker-API. Zie [Adobe Experience Platform Identity Service.](https://experienceleague.adobe.com/docs/id-service/using/home.html) voor meer informatie over optout en privacy.
* **OTT Apps (Chromecast, Roku) -** De OTT SDKs verstrekken algemene de regelgevende (GDPR) - klaar APIs van de Bescherming van Gegevens die u toestaan om  `opt` statusvlaggen voor gegevensinzameling en transmissie te plaatsen, en lokaal opgeslagen identiteiten terug te winnen.

   >[!NOTE]
   >
   >Aanroepen voor het bijhouden van de hartslag van media worden ook uitgeschakeld als de privacystatus is ingesteld op Weigeren.

   Met de volgende instellingen kunt u bepalen of analysegegevens op een specifiek apparaat worden verzonden:

   * De instelling `privacyDefault` in het configuratiebestand `ADBMobile.json`. Hiermee bepaalt u de eerste instelling en gaat u door totdat deze in de code wordt gewijzigd.

   * De methode `ADBMobile().setPrivacyStatus()`.

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
   Nadat de privacy-instelling is gewijzigd met behulp van `setPrivacyStatus`, is de wijziging permanent totdat deze opnieuw wordt gewijzigd met deze methode of totdat de toepassing wordt verwijderd en opnieuw wordt geïnstalleerd.

## Opgeslagen id&#39;s ophalen (OTT-apps) {#retrieving-stored-identifiers-ott-apps}

Met deze informatie kunt u lokaal opgeslagen gebruikersidentiteiten ophalen uit uw Roku-app.

>[!IMPORTANT]
>
>De methode om alle herkenningstekens terug te winnen krijgt alle die gebruikersidentiteiten door SDK worden gekend en worden voortgeduurd. U moet deze methode **before** een gebruiker roepen uit.

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
