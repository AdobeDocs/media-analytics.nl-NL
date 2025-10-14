---
title: Standaardweergave testen
description: Leer meer over de standaardafspeeltest die bij validatie wordt gebruikt.
uuid: c4b3fead-1b27-484b-ab6a-39f1ae0f03f2
exl-id: 3781f0f7-be75-43e5-a40b-a34956dce36e
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 0%

---

# Testen 1: Standaard afspelen{#test-standard-playback}

Deze testcase valideert het algemene afspelen en rangschikken.

De implementaties van de Analytics van media omvatten twee soorten het volgen vraag:
* Oproepen die rechtstreeks aan uw server van Adobe Analytics (AppMeasurement) worden gemaakt - Deze vraag komt op &quot;het Begin van Media&quot;en &quot;Ad Start&quot;gebeurtenissen voor.
* Vraag die aan de server van de Analyse van Media (hartslagen) wordt gemaakt - Deze omvatten in-band en out-of-band vraag:
   * In-band - De SDK verzendt getimede spelvraag of &quot;pingelt&quot;met intervallen van 10 seconden tijdens inhoudsplayback, en met intervallen van één seconde tijdens advertenties.
   * out-of-band - Deze vraag kan op om het even welk punt gebeuren, en omvat Pauze, Buffering, fouten, volledige inhoud, en volledige, enz.

>[!NOTE]
>Het volgen van media gedraagt zich het zelfde op alle platforms.

## Testprocedure

Voer de volgende handelingen uit en registreer deze (in volgorde):

1. **Laad de pagina of app**

   **het Volgen Servers** (voor alle website en mobiele apps):

   * **de server van Adobe Analytics (AppMeasurement) -** Een server of CNAME van RDC die aan een RDC het volgen server oplost wordt vereist voor de dienst van identiteitskaart van de Bezoeker van Experience Cloud. De het volgen van Adobe Analytics server zou in &quot;`.sc.omtrdc.net`&quot;moeten beëindigen of een NAAM zijn.

   * **de Analyseserver van Media (Hartbeats) -** Deze server heeft altijd het formaat &quot;`[namespace].hb.omtrdc.net`&quot;, waar `[namespace]` uw bedrijfsnaam specificeert. Deze naam wordt opgegeven door Adobe.

   U moet bepaalde zeer belangrijke variabelen bevestigen die over alle volgende vraag universeel zijn:

   **identiteitskaart van de Bezoeker van Adobe (`mid`):** de `mid` variabele wordt gebruikt om de waarde te vangen die in het koekje AMCV wordt geplaatst. De variabele `mid` is de primaire identificatiewaarde voor zowel websites als mobiele apps en geeft ook aan dat de service Experience Cloud Visitor ID op de juiste wijze is ingesteld. Deze vindt u in aanroepen van Adobe Analytics (AppMeasurement) en Media Analytics (heartbeats).

   * **de vraag van het Begin van Adobe Analytics**

     | Parameter | Waarde (monster) |
     |---|---|
     | `pev2` | ms_s |
     | `mid` | 30250035503789876473484580554595324209 |

   * **de vraag van de Pagina van de Website**

     | Parameter | Waarde (monster) |
     |---|---|
     | `mid` | 30250035503789876473484580554595324209 |

   * **vraag van de Levenscyclus**

     | Parameter | Waarde (monster) |
     |---|---|
     | `pev2` | ADBINTERN:levenscyclus |
     | `mid` | 30250035503789876473484580554595324209 |

   * **de vraag van het Begin van Analytics van Media**

     | Parameter | Waarde (monster) |
     |---|---|
     | `s:event:type` | start |

     >[!NOTE]
     >
     >Op de vraag van het Begin van de Analyse van Media (`s:event:type=start`) kunnen de `mid` waarden niet aanwezig zijn. Dit is oké. Ze worden mogelijk pas weergegeven wanneer de aanroepen van Media Analytics Play worden uitgevoerd ( `s:event:type=play` ).

   * **de Vraag van het Spel van Analytics van Media**

     | Parameter | Waarde (monster) |
     |---|---|
     | `s:event:type` | play |
     | `s:user:mid` | 30250035503789876473484580554595324209 |

1. **Begin de media speler**

   Wanneer de mediaspeler start, stuurt de Media SDK de toetsaanroepen naar de twee servers in de volgende volgorde:

   1. Adobe Analytics-server - Aanroep starten
   1. Media Analytics-server - Aanroep starten
   1. Media Analytics-server - &quot;Aanvraag voor Adobe Analytics Start aangevraagd&quot;

   De eerste twee hierboven vraag bevat extra meta-gegevens en variabelen. Voor vraagparameters en meta-gegevens, zie [&#x200B; de vraagdetails van de Test.](/help/legacy/validation/test-call-details.md#start-the-media-player)

   De derde vraag hierboven vertelt de server van de Analyse van Media dat de Media SDK verzocht om dat de vraag van het Begin van Adobe Analytics (`pev2=ms_s`) wordt verzonden naar de server van Adobe Analytics.

1. **Mening en onderbreking indien beschikbaar**

   * **Advertentie Begin**

   Wanneer de advertentie begint, worden de volgende zeer belangrijke vraag verzonden in de volgende orde:

   1. Adobe Analytics-server - Aanroep toevoegen
   1. Media Analytics-server - Aanroep toevoegen
   1. Media Analytics-server - &quot;Aanroep Adobe Analytics Ad Start aangevraagd&quot;

   De eerste twee aanroepen bevatten aanvullende metagegevens en variabelen. Voor vraagparameters en meta-gegevens, zie [&#x200B; de vraagdetails van de Test.](/help/legacy/validation/test-call-details.md#view-ad-playback)

   De derde vraag vertelt de server van de Analyse van Media dat de Media SDK verzocht om de vraag van het Begin van Adobe Analytics Ad (`pev2=msa_s`) te verzenden naar de server van Adobe Analytics.

   * **Advertentiespel**

     Tijdens het afspelen van advertenties verzendt de Media Analytics SDK elke seconde afspeelgebeurtenissen van het type &quot;ad&quot; naar de Media Analytics-server.

   * **Advertentie voltooide**

     Op het 100% punt van een advertentie, zou een Volledige vraag van de Analyse van Media moeten worden verzonden.

1. **Pauzeer en playback voor 30 seconden, als beschikbaar.**  **Advertentie**

   Tijdens de pauze van de Advertentie, worden de hartslag van Media Analytics of &quot;pingel&quot;vraag verzonden door SDK naar de server van de Analyse van Media elke seconde.

   >[!NOTE]
   >
   >De waarde van de afspeelkop moet tijdens het pauzeren constant blijven.

   Voor vraagparameters en meta-gegevens, zie [&#x200B; de vraagdetails van de Test.](/help/legacy/validation/test-call-details.md#ma-ad-pause-call)

1. **belangrijkste inhoud van het Spel ononderbroken 10 seconden.**  **Inhoud Spel**

   Tijdens het afspelen van hoofdinhoud verzendt de Media SDK hartslagen (Play-aanroepen) om de tien seconden naar de Media Analytics-server.

   Opmerkingen:

   * De positie van de playhead zou met 10 met elke vraag van het Spel moeten verhogen.
   * De `l:event:duration` waarde vertegenwoordigt het aantal milliseconden sinds de laatste het volgen vraag en zou ruwweg de zelfde waarde op elke 10 tweede vraag moeten zijn.

     Voor vraagparameters en meta-gegevens, zie [&#x200B; de vraagdetails van de Test.](/help/legacy/validation/test-call-details.md#play-main-content)

1. **Pauzeren tijdens playback voor minstens 30 seconden.** Wanneer de mediaspeler wordt gepauzeerd, worden de aanroepen van de pauze-gebeurtenis door de SDK elke 10 seconden naar de Media Analytics-server verzonden. Nadat de pauze is afgelopen, moeten de afspeelgebeurtenissen worden hervat.

   Voor vraagparameters en meta-gegevens, zie [&#x200B; de vraagdetails van de Test.](/help/legacy/validation/test-call-details.md#pause-main-content)

1. **Onderzoek/schrobt media.** Bij het scrubben van de afspeelkop van media worden geen speciale aanroepen voor het bijhouden van de beelden verzonden. Wanneer het afspelen van media echter wordt hervat na het scrubben, moet de waarde van de afspeelkop de nieuwe positie in de hoofdinhoud aangeven.

1. **Replay media (slechts VOD).** Wanneer media wordt herhaald, zou een nieuwe reeks vraag van het Begin van Media moeten worden verzonden (alsof het een nieuwe start was).

1. **Mening volgende media in playlist.** Bij het begin van media van de volgende media in een playlist, zou een nieuwe reeks vraag van het Begin van Media moeten worden verzonden.

1. **media of stroom van de Schakelaar.** Bij het schakelen van live streams moet een volledige aanroep van Media Analytics voor de eerste stream niet worden verzonden. De vraag van het Begin van Media en de vraag van het Spel zouden met de nieuwe show en stroomnaam, en met de correcte playhead en duurwaarden voor nieuwe show moeten beginnen.
