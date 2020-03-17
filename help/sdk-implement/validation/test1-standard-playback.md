---
title: Standaardweergave testen
description: Dit onderwerp beschrijft de standaardplaybacktest die in bevestiging wordt gebruikt.
uuid: c4b3fead-1b27-484b-ab6a-39f1ae0f03f2
translation-type: tm+mt
source-git-commit: cebf5697e3746721d29bfaa5356d5a2748fea435

---


# Test 1: Standaardweergave{#test-standard-playback}

Deze testcase valideert het algemene afspelen en rangschikken.

De implementaties van de Analytics van media omvatten twee soorten het volgen vraag:
* Oproepen rechtstreeks aan uw server van de Analyse van Adobe (AppMeasurement) - Deze vraag komt op &quot;van het Begin van Media&quot;en &quot;van het Begin van de Advertentie voor&quot;gebeurtenissen voor.
* Vraag die aan de server van de Analyse van Media (hartslagen) wordt gemaakt - Deze omvatten in-band en out-of-band vraag:
   * In-band - De SDK verzendt getimede spelvraag of &quot;pingelt&quot;met intervallen van 10 seconden tijdens inhoudsplayback, en met intervallen van één seconde tijdens advertenties.
   * out-of-band - Deze vraag kan op om het even welk punt gebeuren, en omvat Pauze, Buffering, fouten, volledige inhoud, en volledige, enz.

>[!NOTE]
>Het volgen van media gedraagt zich het zelfde op alle platforms.

## Testprocedure

Voer de volgende handelingen uit en registreer deze (in volgorde):

1. **De pagina of toepassing laden**

   **Servers** bijhouden (voor alle website- en mobiele apps):

   * **Adobe Analytics-server (AppMeasurement) -** Voor de Experience Cloud Visitor ID-service is een RDC-trackingserver of CNAME vereist die wordt omgezet in een RDC-trackingserver. De Adobe Analytics tracking-server moet &#39;`.sc.omtrdc.net`&#39; of &#39;CNAME&#39; als laatste hebben.

   * **Media Analytics (Heartbeats)-server -** Deze server heeft altijd de indeling &quot;`[namespace].hb.omtrdc.net`&quot;, waarbij de naam van uw bedrijf `[namespace]` wordt opgegeven. Deze naam wordt geleverd door Adobe.
   U moet bepaalde zeer belangrijke variabelen bevestigen die over alle volgende vraag universeel zijn:

   **Adobe Bezoeker-id (`mid`):** De `mid` variabele wordt gebruikt om de waarde vast te leggen die is ingesteld in het AMCV-cookie. De `mid` variabele is de primaire identificatiewaarde voor zowel websites als mobiele apps en geeft ook aan dat de Experience Cloud Visitor ID-service op de juiste wijze is ingesteld. Deze vindt u in aanroepen van Adobe Analytics (AppMeasurement) en Media Analytics (heartbeats).

   * **Aanroep van Adobe Analytics**

      | Parameter | Waarde (monster) |
      |---|---|
      | `pev2` | ms_s |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Aanroep van webpagina**

      | Parameter | Waarde (monster) |
      |---|---|
      | `mid` | 30250035503789876473484580554595324209 |

   * **Levenscyclusgesprek**

      | Parameter | Waarde (monster) |
      |---|---|
      | `pev2` | ADBINTERN:levenscyclus |
      | `mid` | 30250035503789876473484580554595324209 |

   * **De vraag van het Begin van de Analyse van media**

      | Parameter | Waarde (monster) |
      |---|---|
      | `s:event:type` | start |

      >[!NOTE]
      >
      >Bij de vraag van het Begin van de Analyse van Media (`s:event:type=start`) kunnen de `mid` waarden niet aanwezig zijn. Dit is oké. Zij kunnen niet verschijnen tot de Vraag van het Spel van de Analyse van Media ( `s:event:type=play`).

   * **Media Analytics Play-aanroep**

      | Parameter | Waarde (monster) |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |


1. **De mediaspeler starten**

   Wanneer de media speler begint, verzendt SDK van Media de belangrijkste vraag naar de twee servers in de volgende orde:

   1. Adobe Analytics-server - Aanroep starten
   1. Media Analytics-server - Aanroep starten
   1. Media Analytics-server - &quot;Aanvraag voor starten van Adobe Analytics aangevraagd&quot;
   De eerste twee bovenstaande aanroepen bevatten aanvullende metagegevens en variabelen. Voor vraagparameters en meta-gegevens, zie de vraagdetails van de [Test.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   In de derde bovenstaande oproep wordt aan de Media Analytics-server doorgegeven dat de Media SDK heeft verzocht dat de aanroep van Adobe Analytics Start (`pev2=ms_s`) naar de Adobe Analytics-server wordt verzonden.

1. **Weergeven en afbreken indien beschikbaar**

   * **Ad Start**
   Wanneer de advertentie begint, worden de volgende belangrijkste vraag verzonden in de volgende orde:

   1. Adobe Analytics-server - Aanroep toevoegen
   1. Media Analytics-server - Aanroep toevoegen
   1. Media Analytics-server - &quot;Aanroep van Adobe Analytics Ad Start aangevraagd&quot;
   De eerste twee aanroepen bevatten aanvullende metagegevens en variabelen. Voor vraagparameters en meta-gegevens, zie de vraagdetails van de [Test.](/help/sdk-implement/validation/test-call-details.md#view-ad-playback)

   De derde aanroep vertelt de Media Analytics-server dat de Media SDK heeft verzocht dat de aanroep van Adobe Analytics Ad Start (`pev2=msa_s`) naar de Adobe Analytics-server wordt verzonden.

   * **Ad Play**

      Tijdens het afspelen van advertenties verzendt de Media Analytics SDK elke seconde afspeelgebeurtenissen van het type &quot;ad&quot; naar de Media Analytics-server.

   * **Toevoegen voltooid**

      Op het 100% punt van een advertentie, zou een Volledige vraag van de Analyse van Media moeten worden verzonden.



1. **Pauzeren en afspelen gedurende 30 seconden, indien beschikbaar.**  Pauze **toevoegen**

   Tijdens de Pauze van de Advertentie, wordt de hartslag van de Analyse van Media of &quot;pingel&quot;vraag verzonden door SDK naar de server van de Analyse van Media elke seconde.

   >[!NOTE]
   >
   >De waarde van de afspeelkop moet tijdens het pauzeren constant blijven.

   Voor vraagparameters en meta-gegevens, zie de vraagdetails van de [Test.](/help/sdk-implement/validation/test-call-details.md#ma-ad-pause-call)

1. **De belangrijkste inhoud van het spel ononderbroken 10 minuten.**  **Inhoud afspelen**

   Tijdens hoofdinhoudsplayback, verzendt SDK van Media hartslagen (de vraag van het Spel) naar de server van de Analyse van Media om de 10 seconden.

   Opmerkingen:

   * De positie van de playhead zou met 10 met elke vraag van het Spel moeten verhogen.
   * De `l:event:duration` waarde vertegenwoordigt het aantal milliseconden sinds de laatste het volgen vraag en zou ruwweg de zelfde waarde op elke 10 tweede vraag moeten zijn.

      Voor vraagparameters en meta-gegevens, zie de vraagdetails van de [Test.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Pauzeren tijdens afspelen gedurende ten minste 30 seconden.** Wanneer de mediaspeler wordt gepauzeerd, worden de aanroepen van de pauzegebeurtenis elke 10 seconden door de SDK naar de Media Analytics-server verzonden. Nadat de pauze is afgelopen, moeten de afspeelgebeurtenissen worden hervat.

   Voor vraagparameters en meta-gegevens, zie de vraagdetails van de [Test.](/help/sdk-implement/validation/test-call-details.md#pause-main-content)

1. **Medium zoeken/scrubben.** Bij het scrubben van media playhead, wordt geen speciale het volgen vraag verzonden, echter, wanneer media playback na het scrubben hervat, zou de playhead waarde op de nieuwe positie binnen de belangrijkste inhoud moeten wijzen.

1. **Media opnieuw afspelen (alleen VOD).** Wanneer media wordt herhaald, zou een nieuwe reeks vraag van het Begin van Media moeten worden verzonden (alsof het een nieuwe start was).

1. **Volgende media in afspeellijst weergeven.** Op het Begin van Media van de volgende media in playlist, zou een nieuwe reeks vraag van het Begin van Media moeten worden verzonden.

1. **Media of stream wisselen.** Wanneer het schakelen van levende stromen, zou een volledige vraag van Media Analytics voor de eerste stroom niet moeten worden verzonden. De vraag van het Begin van Media en de vraag van het Spel zouden met de nieuwe show en stroomnaam, en met de correcte playhead en duurwaarden voor nieuwe show moeten beginnen.
