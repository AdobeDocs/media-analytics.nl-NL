---
title: Adobe Debug configureren
description: Dit onderwerp beschrijft hoe te om Adobe te vormen zuiver, dat u kunt gebruiken om de implementaties van SDK van Media problemen op te lossen.
uuid: e416458d-f23c-41ce-8d99-fa5076c455f0
translation-type: tm+mt
source-git-commit: f0f04ffab851999becb2b7771eef36ad7477c9f3
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 1%

---


# Adobe Debug configureren{#configure-adobe-debug}

## De toegang tot Adobe zuivert {#accessing-adobe-debug}

Om tot Adobe toegang te hebben zuiver:

1. Ga naar [Ervaar Cloud](https://www.marketing.adobe.com) en maak een nieuwe Adobe Experience Cloud-gebruiker.

   >[!TIP]
   >
   >Deze login is niet de zelfde gebruikersbenaming/het wachtwoord u aan login van de Analyse van Adobe gebruikt.

1. Nadat u een rekening van de Wolk van de Ervaring hebt, contacteer uw vertegenwoordiger van Adobe om toegang tot Adobe te verzoeken zuiver.
1. Nadat de toegang is verleend, ga naar [https://debug.adobe.com](https://debug.adobe.com) en gebruik uw referenties van de Cloud van de Ervaring aan login.

   ![](assets/adobe-debug-login.png)

   Ondersteunde browsers voor dit gereedschap zijn:
   * Google Chrome
   * Mozilla Firefox
   * Apple Safari
   * Microsoft Internet Explorer versie 9-11

De geadviseerde browsers zijn de recentste versies van Chrome en Firefox.

## Zuiver Volmacht {#debug-proxy}

De download en vormt Debug Volmacht:

1. Download Debug app van de Volmacht bij [App Downloads.](https://debug.adobe.com/#/downloads)

   De ondersteunde besturingssystemen zijn:
   * OS X 10.7 64-bits of hoger
   * Windows 7.1 64-bits of hoger

   ![](assets/debug-proxy-app.png)

1. De Debug server van de Volmacht zal op uw lokale machine op haven 33284 lopen en zal als systeemvolmacht worden geplaatst.

   U zou uw browser kunnen moeten aanpassen die op OS en browser wordt gebaseerd plaatst.

## Download en installeer het SSL Certificaat op Desktop of apps {#download-and-install-sSL-desktop}

De eerste keer u zuivert Adobe, zal een uniek SSL certificaat worden geproduceerd. Als u verkeer HTTPS over Desktop en/of Apps steunt, moet u ons SSL certificaat downloaden en installeren.

Download en installeer het SSL certificaat:

1. Nadat Adobe zuivert is geïnstalleerd en is begonnen, ga naar [https://proxy.debug.adobe.com/ssl](https://proxy.debug.adobe.com/ssl) en download de certificering.
1. Het certificaat importeren

   **Mac OS**
   1. Klik het certificaat van wortelCA tweemaal om het in Keychain Access te openen.
   1. Het certificaat van wortelCA verschijnt in login.
   1. Verplaats (sleep) het certificaat van de wortelCA naar Systeem.
   1. U moet het certificaat aan Systeem kopiëren om ervoor te zorgen dat het door alle gebruikers en lokale systeemprocessen wordt vertrouwd.
   1. Open het certificaat van wortel CA, breid Vertrouwen uit, selecteer altijd Vertrouwen, en sla uw veranderingen op.

   **Windows**
   1. Voer een van de volgende procedures uit:

      * [Het toevoegen van certificaten aan de Vertrouwde opslag van de Certificatie van de Wortel voor een lokale computer](https://technet.microsoft.com/en-us/library/cc754841.aspx#BKMK_addlocal)
   1. Voor Firefox, voltooi de procedure in [Het installeren van wortelcertificaat in Mozilla Firefox.](https://wiki.wmtransfer.com/projects/webmoney/wiki/Installing_root_certificate_in_Mozilla_Firefox)

      U zou kunnen moeten ophouden en Firefox heropenen om de verandering te zien.
   **iOS-apparaten**
   1. Plaats uw iOS apparaat om Adobe te gebruiken zuiveren als zijn volmacht van HTTP door te klikken **[!UICONTROL Settings app]** **>** **[!UICONTROL Wifi settings]**.

   1. Ga in Safari naar [Zuiver.](https://proxy.debug.adobe.com/ssl)

      Safari zal u ertoe aanzetten om het SSL certificaat te installeren.




## Installeer het SSL certificaat voor uw mobiel apparaat {#install-sSL-for-mobile-device}

Als u de vraag HTTPS in Adobe zuivert mist, moet u het SSL Certificaat voor Adobe installeren zuivert op het mobiele apparaat.

### iOS

Om het SSL certificaat op een iOS apparaat te installeren:

1. Voor uw laptop, zet de Debug Volmacht aan, en ga naar [Adobe zuivert.](https://debug.adobe.com)
1. Voer de volgende stappen uit op uw iOS-apparaat:
   1. Draai uw apparaat in de vliegtuigmodus.
   1. Selecteer hetzelfde Wi-Fi-signaal dat door uw laptop wordt gebruikt.
   1. Voor uw laptop, plaats manueel IP en de haven die op Debug app van de Volmacht wordt getoond.
   1. Open een browser van Apple Safari venster.
   1. Ga naar [https://proxy.debug.adobe.com/ssl](https://proxy.debug.adobe.com/ssl)
   1. Download en installeer het SSL certificaat.

1. Voor uw laptop, begin uw Adobe zuiveren zitting.
1. Test het iOS-apparaat.

### Android

Om het SSL certificaat op een Android apparaat te installeren:

1. Schakel op uw laptop de Debug Proxy in en ga naar [Adobe zuivert.](https://debug.adobe.com)
1. Voer de volgende stappen uit op uw Android-apparaat:
   1. Stel uw apparaat in op de vliegtuigmodus.
   1. Selecteer hetzelfde Wi-Fi-signaal dat door uw laptop wordt gebruikt.
   1. Voor uw laptop, plaats manueel IP en de haven die op Debug app van de Volmacht wordt getoond.
   1. Open een browservenster.
   1. Ga naar [https://proxy.debug.adobe.com/ssl](https://proxy.debug.adobe.com/ssl)
   1. Download en installeer het SSL certificaat.

1. Voor uw laptop, begin uw Adobe zuiveren zitting.
1. Test het Android-apparaat.

