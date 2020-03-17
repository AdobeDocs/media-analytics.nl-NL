---
title: Adobe Debug configureren
description: Dit onderwerp beschrijft hoe te om Adobe te vormen zuivert, die u kunt gebruiken om de implementaties van SDK van Media problemen op te lossen.
uuid: e416458d-f23c-41ce-8d99-fa5076c455f0
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Adobe Debug configureren{#configure-adobe-debug}

## Toegang tot Adobe Debug {#accessing-adobe-debug}

Ga als volgt te werk om Adobe Debug te openen:

1. Ga naar [Experience Cloud](https://www.marketing.adobe.com) en maak een nieuwe Adobe Experience Cloud-gebruiker.

   >[!TIP]
   >
   >Deze aanmelding is niet dezelfde gebruikersnaam/hetzelfde wachtwoord als waarmee u zich aanmeldt bij Adobe Analytics.

1. Nadat u een Experience Cloud-account hebt, neemt u contact op met uw Adobe-vertegenwoordiger om toegang tot Adobe Debug te vragen.
1. Nadat toegang is verleend, gaat u naar [https://debug.adobe.com](https://debug.adobe.com) en gebruikt u uw aanmeldingsgegevens voor de Experience Cloud om u aan te melden.

   ![](assets/adobe-debug-login.png)

   De ondersteunde browsers voor dit gereedschap zijn:
   * Google Chrome
   * Mozilla Firefox
   * Apple Safari
   * Microsoft Internet Explorer 9-11

De aanbevolen browsers zijn de nieuwste versies van Chrome en Firefox.

## Proxy voor foutopsporing {#debug-proxy}

Download en vorm de Debug Proxy:

1. Download de toepassing Debug Proxy op [App Downloads.](https://debug.adobe.com/#/downloads)

   De ondersteunde besturingssystemen zijn:
   * OS X 10.7 64-bits of hoger
   * Windows 7.1 64-bits of hoger
   ![](assets/debug-proxy-app.png)

1. De server van de Volmacht zuivert zal op uw lokale computer op haven 33284 lopen en zal als systeemvolmacht worden geplaatst.

   Mogelijk moet u de browserinstelling aanpassen op basis van het besturingssysteem en de browser.

## Download en installeer het SSL-certificaat op een desktopcomputer of op apps {#download-and-install-sSL-desktop}

De eerste keer dat u Adobe Debug uitvoert, wordt een uniek SSL-certificaat gegenereerd. Als u HTTPS-verkeer op het bureaublad en/of toepassingen ondersteunt, moet u ons SSL-certificaat downloaden en installeren.

Download en installeer het SSL-certificaat:

1. Nadat Adobe Debug is geïnstalleerd en gestart, gaat u naar [https://proxy.debug.adobe.com/ssl](https://proxy.debug.adobe.com/ssl) en downloadt u de certificering.
1. Het certificaat importeren

   **Mac OS**
   1. Dubbelklik op het basis-CA-certificaat om dit te openen in Keychain Access.
   1. Het basiscertificaat van CA wordt weergegeven in de aanmelding.
   1. Verplaats (sleep) het basis-CA-certificaat naar Systeem.
   1. U moet het certificaat naar Systeem kopiëren om ervoor te zorgen dat het door alle gebruikers en lokale systeemprocessen wordt vertrouwd.
   1. Open het basiscertificaat van CA, vouw vertrouwen uit, selecteer altijd Vertrouwen, en sla uw veranderingen op.
   **Windows**
   1. Voer een van de volgende handelingen uit:

      * [Certificaten toevoegen aan het archief met vertrouwde basiscertificeringsinstanties voor een lokale computer](https://technet.microsoft.com/en-us/library/cc754841.aspx#BKMK_addlocal)
<!--        * [How To Import a Trusted Root Certification Authority In Windows 7/Vista/XP](https://www.sqlservermart.com/HowTo/Windows_Import_Certificate.aspx) You might need to quit and reopen your browser to see the change.
-->

    1. Voor Firefox voltooit u de procedure in [Het basiscertificaat installeren in Mozilla Firefox.](https://wiki.wmtransfer.com/projects/webmoney/wiki/Installing_root_certificate_in_Mozilla_Firefox)
    
    Mogelijk moet u Firefox afsluiten en opnieuw openen om de wijziging te zien.
    
    **iOS-apparaten**
    1. Stel uw iOS-apparaat in om Adobe Debug als HTTP-proxy te gebruiken door te klikken op **[!UICONTROL Settings app]********[!UICONTROL Wifi settings]*.
    
    1. Ga in Safari naar [Foutopsporing].](https://proxy.debug.adobe.com/ssl)
    
    Safari vraagt u het SSL-certificaat te installeren.

## Het SSL-certificaat voor uw mobiele apparaat installeren {#install-sSL-for-mobile-device}

Als u de HTTPS-aanroepen in Adobe Debug mist, moet u het SSL-certificaat voor Adobe Debug installeren op het mobiele apparaat.

### iOS

Het SSL-certificaat installeren op een iOS-apparaat:

1. Schakel op uw laptop de optie Debug Proxy in en ga naar [Adobe Debug.](https://debug.adobe.com)
1. Voer de volgende stappen uit op uw iOS-apparaat:
   1. Zet het apparaat om in de vliegtuigmodus.
   1. Selecteer hetzelfde Wi-Fi-signaal dat door uw laptop wordt gebruikt.
   1. Stel op uw laptop handmatig het IP-adres en de poort in die worden weergegeven in de toepassing Proxy debuggen.
   1. Open een browservenster van Apple Safari.
   1. Ga naar [https://proxy.debug.adobe.com/ssl.](https://proxy.debug.adobe.com/ssl)
   1. Download en installeer het SSL-certificaat.

1. Start op uw laptop de Adobe Debug-sessie.
1. Test op uw iOS-apparaat.

### Android

Het SSL-certificaat installeren op een Android-apparaat:

1. Schakel op uw laptop de Debug Proxy in en ga naar [Adobe Debug.](https://debug.adobe.com)
1. Voer de volgende stappen uit op uw Android-apparaat:
   1. Stel uw apparaat in op de vliegtuigmodus.
   1. Selecteer hetzelfde Wi-Fi-signaal dat door uw laptop wordt gebruikt.
   1. Stel op uw laptop handmatig het IP-adres en de poort in die worden weergegeven in de toepassing Proxy debuggen.
   1. Open een browservenster.
   1. Ga naar [https://proxy.debug.adobe.com/ssl.](https://proxy.debug.adobe.com/ssl)
   1. Download en installeer het SSL-certificaat.

1. Start op uw laptop de Adobe Debug-sessie.
1. Start met testen op uw Android-apparaat.
