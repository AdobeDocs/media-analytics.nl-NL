---
title: Standaardweergave testen
description: Leer meer over de standaardafspeeltest die bij validatie wordt gebruikt.
uuid: c4b3fead-1b27-484b-ab6a-39f1ae0f03f2
exl-id: 3781f0f7-be75-43e5-a40b-a34956dce36e
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---

# Test 1: Standaardweergave{#test-standard-playback}

Deze testcase valideert het algemene afspelen en rangschikken.

De implementaties van de Analytics van media omvatten twee soorten het volgen vraag:
* Oproepen die rechtstreeks aan uw server van Adobe Analytics (AppMeasurement) worden gemaakt - Deze vraag komt op de gebeurtenissen &quot;van het Begin van Media&quot;en &quot;van het Begin van de Advertentie&quot;voor.
* Vraag die aan de server van de Analyse van Media (hartslagen) wordt gemaakt - Deze omvatten in-band en out-of-band vraag:
   * In-band - De SDK verzendt getimede spelvraag of &quot;pingelt&quot;met intervallen van 10 seconden tijdens inhoudsplayback, en met intervallen van één seconde tijdens advertenties.
   * out-of-band - Deze vraag kan op om het even welk punt gebeuren, en omvat Pauze, Buffering, fouten, volledige inhoud, en volledige, enz.

>[!NOTE]
>Het volgen van media gedraagt zich het zelfde op alle platforms.

## Testprocedure

Voer de volgende handelingen uit en registreer deze (in volgorde):

1. **De pagina of toepassing laden**

   **Servers**  bijhouden (voor alle website- en mobiele apps):

   * **Adobe Analytics-server (AppMeasurement) -** Een RDC-trackingserver of CNAME die wordt omgezet in een RDC-trackingserver is vereist voor de Experience Cloud Bezoeker ID-service. De Adobe Analytics tracking-server moet eindigen in &quot;`.sc.omtrdc.net`&quot; of een CNAME zijn.

   * **Media Analytics (Heartbeats)-server -** Deze server heeft altijd de indeling &quot;`[namespace].hb.omtrdc.net`&quot;, waarbij uw bedrijfsnaam  `[namespace]` wordt opgegeven. Deze naam wordt opgegeven door Adobe.

   U moet bepaalde zeer belangrijke variabelen bevestigen die over alle volgende vraag universeel zijn:

   **Adobe Bezoeker-id (`mid`):** De  `mid` variabele wordt gebruikt om de waarde vast te leggen die is ingesteld in het AMCV-cookie. De variabele `mid` is de primaire identificatiewaarde voor zowel websites als mobiele apps en geeft ook aan dat de service Experience Cloud Visitor ID op de juiste wijze is ingesteld. Deze vindt u in zowel aanroepen van Adobe Analytics (AppMeasurement) als Media Analytics (heartbeats).

   * **Aanroep Adobe Analytics Start**

      | Parameter | Waarde (monster) |
      |---|---|
      | `pev2` | ms_s |
      | `mid` | 3025003550378987647348458054595324209 |

   * **Aanroep van webpagina**

      | Parameter | Waarde (monster) |
      |---|---|
      | `mid` | 3025003550378987647348458054595324209 |

   * **Levenscyclusgesprek**

      | Parameter | Waarde (monster) |
      |---|---|
      | `pev2` | ADBINTERN:levenscyclus |
      | `mid` | 3025003550378987647348458054595324209 |

   * **De vraag van het Begin van de Analyse van media**

      | Parameter | Waarde (monster) |
      |---|---|
      | `s:event:type` | start |

      >[!NOTE]
      >
      >Op de vraag van het Begin van de Analyse van Media (`s:event:type=start`) kunnen de `mid` waarden niet aanwezig zijn. Dit is oké. Zij kunnen niet verschijnen tot de Vraag van het Spel van de Analyse van Media ( `s:event:type=play`).

   * **Media Analytics Play-aanroep**

      | Parameter | Waarde (monster) |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 3025003550378987647348458054595324209 |


1. **De mediaspeler starten**

   Wanneer de media speler begint, verzendt SDK van Media de belangrijkste vraag naar de twee servers in de volgende orde:

   1. Adobe Analytics-server - Aanroep starten
   1. Media Analytics-server - Aanroep starten
   1. Media Analytics-server - &quot;Aanvraag voor Adobe Analytics Start aangevraagd&quot;

   De eerste twee bovenstaande aanroepen bevatten aanvullende metagegevens en variabelen. Voor vraagparameters en meta-gegevens, zie [de vraagdetails van de test.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   De derde vraag hierboven vertelt de server van de Analyse van Media dat de Media SDK verzocht om de vraag van het Begin van Adobe Analytics (`pev2=ms_s`) naar de server van Adobe Analytics wordt verzonden.

1. **Weergeven en afbreken indien beschikbaar**

   * **Ad Start**

   Wanneer de advertentie begint, worden de volgende belangrijkste vraag verzonden in de volgende orde:

   1. Adobe Analytics-server - Aanroep toevoegen
   1. Media Analytics-server - Aanroep toevoegen
   1. Media Analytics-server - &quot;Aanroep Adobe Analytics Ad Start aangevraagd&quot;

   De eerste twee aanroepen bevatten aanvullende metagegevens en variabelen. Voor vraagparameters en meta-gegevens, zie [de vraagdetails van de test.](/help/sdk-implement/validation/test-call-details.md#view-ad-playback)

   De derde oproep vertelt de Media Analytics-server dat de Media SDK heeft verzocht om de Adobe Analytics Ad Start-aanroep (`pev2=msa_s`) naar de Adobe Analytics-server te verzenden.

   * **Ad Play**

      Tijdens het afspelen van advertenties verzendt de Media Analytics SDK elke seconde afspeelgebeurtenissen van het type &quot;ad&quot; naar de Media Analytics-server.

   * **Toevoegen voltooid**

      Op het 100% punt van een advertentie, zou een Volledige vraag van de Analyse van Media moeten worden verzonden.



1. **Pauzeren en afspelen gedurende 30 seconden, indien beschikbaar.**   **Pauzeren**

   Tijdens de Pauze van de Advertentie, wordt de hartslag van de Analyse van Media of &quot;pingel&quot;vraag verzonden door SDK naar de server van de Analyse van Media elke seconde.

   >[!NOTE]
   >
   >De waarde van de afspeelkop moet tijdens het pauzeren constant blijven.

   Voor vraagparameters en meta-gegevens, zie [de vraagdetails van de test.](/help/sdk-implement/validation/test-call-details.md#ma-ad-pause-call)

1. **De belangrijkste inhoud van het spel ononderbroken 10 seconden.**   **Inhoud afspelen**

   Tijdens hoofdinhoudsplayback, verzendt SDK van Media hartslagen (de vraag van het Spel) naar de server van de Analyse van Media om de 10 seconden.

   Opmerkingen:

   * De positie van de playhead zou met 10 met elke vraag van het Spel moeten verhogen.
   * De `l:event:duration` waarde vertegenwoordigt het aantal milliseconden sinds de laatste het volgen vraag en zou ruwweg de zelfde waarde op elke 10 tweede vraag moeten zijn.

      Voor vraagparameters en meta-gegevens, zie [de vraagdetails van de test.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Pauzeren tijdens afspelen gedurende ten minste 30 seconden.** Wanneer de mediaspeler wordt gepauzeerd, worden de aanroepen van de pauzegebeurtenis elke 10 seconden door de SDK naar de Media Analytics-server verzonden. Nadat de pauze is afgelopen, moeten de afspeelgebeurtenissen worden hervat.

   Voor vraagparameters en meta-gegevens, zie [de vraagdetails van de test.](/help/sdk-implement/validation/test-call-details.md#pause-main-content)

1. **Medium zoeken/scrubben.** Bij het scrubben van media playhead, wordt geen speciale het volgen vraag verzonden, echter, wanneer media playback na het scrubben hervat, zou de playhead waarde op de nieuwe positie binnen de belangrijkste inhoud moeten wijzen.

1. **Media opnieuw afspelen (alleen VOD).** Wanneer media wordt herhaald, zou een nieuwe reeks vraag van het Begin van Media moeten worden verzonden (alsof het een nieuwe start was).

1. **Volgende media in afspeellijst weergeven.** Op het Begin van Media van de volgende media in playlist, zou een nieuwe reeks vraag van het Begin van Media moeten worden verzonden.

1. **Media of stream wisselen.** Wanneer het schakelen van levende stromen, zou een volledige vraag van Media Analytics voor de eerste stroom niet moeten worden verzonden. De vraag van het Begin van Media en de vraag van het Spel zouden met de nieuwe show en stroomnaam, en met de correcte playhead en duurwaarden voor nieuwe show moeten beginnen.
