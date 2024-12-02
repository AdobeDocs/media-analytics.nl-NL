---
title: Foutopsporing Adobe configureren
description: Leer hoe te om Adobe te vormen zuivert, die u kunt gebruiken om de implementaties van SDK van Media problemen op te lossen.
uuid: e416458d-f23c-41ce-8d99-fa5076c455f0
exl-id: 48ad3f23-f36d-44f3-b8d9-b0b3a2ee06bc
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---

# Foutopsporing Adobe configureren{#configure-adobe-debug}

## Toegang tot foutopsporing Adobe {#accessing-adobe-debug}

Voor toegang tot foutopsporing in Adobe:

1. Ga naar [ Experience Cloud ](https://www.marketing.adobe.com/) en creeer een nieuwe gebruiker van Adobe Experience Cloud.

   >[!TIP]
   >
   >Deze aanmelding is niet dezelfde gebruikersnaam/hetzelfde wachtwoord als waarmee u zich aanmeldt bij Adobe Analytics.

1. Nadat u een rekening van het Experience Cloud hebt, contacteer uw vertegenwoordiger van de Adobe om toegang tot Adobe te verzoeken zuivert.
1. Nadat de toegang is verleend, ga naar [ https://debug.adobe.com ](https://debug.adobe.com) en gebruik uw geloofsbrieven van het Experience Cloud aan login.

   ![](assets/adobe-debug-login.png)

   De ondersteunde browsers voor dit gereedschap zijn:
   * Google Chrome
   * Mozilla Firefox
   * Apple Safari
   * Microsoft Internet Explorer 9-11

De aanbevolen browsers zijn de nieuwste versies van Chrome en Firefox.

## Proxy voor foutopsporing {#debug-proxy}

Download en vorm de Debug Proxy:

1. Download Debug Proxy app bij [ App Downloads.](https://debug.adobe.com/#/downloads)

   De ondersteunde besturingssystemen zijn:
   * OS X 10.7 64-bits of hoger
   * Windows 7.1 64-bits of hoger

   ![](assets/debug-proxy-app.png)

1. De server van de Volmacht zuivert zal op uw lokale computer op haven 33284 lopen en zal als systeemvolmacht worden geplaatst.

   Mogelijk moet u de browserinstelling aanpassen op basis van het besturingssysteem en de browser.

## Download en installeer het SSL-certificaat op een desktopcomputer of op apps {#download-and-install-sSL-desktop}

De eerste keer dat u Adobe debuggen uitvoert, wordt een uniek SSL certificaat gegenereerd. Als u HTTPS-verkeer op het bureaublad en/of toepassingen ondersteunt, moet u ons SSL-certificaat downloaden en installeren.

Download en installeer het SSL-certificaat:

1. Nadat de Adobe zuivert is geïnstalleerd en is begonnen, ga [ https://proxy.debug.adobe.com/ssl ](https://proxy.debug.adobe.com/ssl) en download de certificatie.
1. Het certificaat importeren

   **Mac OS**
   1. Dubbelklik op het basis-CA-certificaat om dit te openen in Keychain Access.
   1. Het basiscertificaat van CA wordt weergegeven in de aanmelding.
   1. Verplaats (sleep) het basis-CA-certificaat naar Systeem.
   1. U moet het certificaat naar Systeem kopiëren om ervoor te zorgen dat het door alle gebruikers en lokale systeemprocessen wordt vertrouwd.
   1. Open het basiscertificaat van CA, vouw vertrouwen uit, selecteer altijd Vertrouwen, en sla uw veranderingen op.

   **Vensters**
   1. Voer een van de volgende handelingen uit:

      * [ Toevoegend certificaten aan de Vertrouwde opslag van de Certificatie van de Wortel voor een lokale computer ](https://technet.microsoft.com/en-us/library/cc754841.aspx#BKMK_addlocal)

   1. Voor Firefox, voltooi de procedure in [ Installing wortelcertificaat in Mozilla Firefox.](https://wiki.wmtransfer.com/projects/webmoney/wiki/Installing_root_certificate_in_Mozilla_Firefox)

      Mogelijk moet u Firefox afsluiten en opnieuw openen om de wijziging te kunnen zien.

   **de apparaten van iOS**
   1. Plaats uw iOS apparaat om Adobe te gebruiken zuivert als volmacht van HTTP door **[!UICONTROL Settings app]** **>** **[!UICONTROL Wifi settings]** te klikken.

   1. In Safari, ga [ zuiveren.](https://proxy.debug.adobe.com/ssl)

      Safari vraagt u het SSL-certificaat te installeren.

## Het SSL-certificaat voor uw mobiele apparaat installeren {#install-sSL-for-mobile-device}

Als u de HTTPS-aanroepen in de foutopsporing voor Adobe mist, moet u het SSL-certificaat voor foutopsporing voor Adobe installeren op het mobiele apparaat.

### iOS

Ga als volgt te werk om het SSL-certificaat op een iOS-apparaat te installeren:

1. Voor uw laptop, zet de Debug Volmacht aan, en ga [ Adobe zuiveren.](https://debug.adobe.com)
1. Voer de volgende stappen uit op uw iOS-apparaat:
   1. Zet het apparaat om in de vliegtuigmodus.
   1. Selecteer hetzelfde Wi-Fi-signaal dat door uw laptop wordt gebruikt.
   1. Stel op uw laptop handmatig het IP-adres en de poort in die worden weergegeven in de toepassing Proxy debuggen.
   1. Open een Apple Safari-browservenster.
   1. Ga naar [ https://proxy.debug.adobe.com/ssl.](https://proxy.debug.adobe.com/ssl)
   1. Download en installeer het SSL-certificaat.

1. Start op uw laptop de foutopsporingssessie voor de Adobe.
1. Test op je iOS-apparaat.

### Android

Ga als volgt te werk om het SSL-certificaat op een Android-apparaat te installeren:

1. Op uw laptop zet de Debug Volmacht aan en gaat [ Adobe zuiveren.](https://debug.adobe.com)
1. Voer de volgende stappen uit op uw Android-apparaat:
   1. Stel uw apparaat in op de vliegtuigmodus.
   1. Selecteer hetzelfde Wi-Fi-signaal dat door uw laptop wordt gebruikt.
   1. Stel op uw laptop handmatig het IP-adres en de poort in die worden weergegeven in de toepassing Proxy debuggen.
   1. Open een browservenster.
   1. Ga naar [ https://proxy.debug.adobe.com/ssl.](https://proxy.debug.adobe.com/ssl)
   1. Download en installeer het SSL-certificaat.

1. Start op uw laptop de foutopsporingssessie voor de Adobe.
1. Test op je Android-apparaat.
