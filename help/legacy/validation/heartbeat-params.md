---
title: Beschrijvingen van hartslagparameters
description: Verken de hartslagparameters die Adobe verzamelt en verwerkt op de Media Analytics-server (heartbeats).
uuid: e9ddda32-0952-43d0-a702-49f5b1bfd8cf
exl-id: ffa67b5e-ee54-4a5b-8064-decd108f944b
feature: "Media Analytics, Variables"
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 5%

---

# Beschrijving van de parameter Media Analytics (heartbeats){#heartbeat-parameter-descriptions}

Lijst met parameters voor Media Analytics die Adobe verzamelt en verwerkt op de Media Analytics-server (heartbeats):

## Alle gebeurtenissen

| Naam | Gegevensbron |  Beschrijving  |
| ---  | --- | --- |
| s:event:type | Media-SDK | (Vereist)<br/><br/>Het type gebeurtenis dat wordt bijgehouden. Gebeurtenistypen: <ul> <li> s:event:type=start </li> <li> s:event:type=complete </li> <li> s:event:type=chapter_start </li> <li> s:event:type=chapter_complete </li> <li> s:event:type=buffer </li> <li> s:event:type=pause </li> <li> s:event:type=resume </li> <li> s:event:type=bitrate_change </li> <li> s:event:type=aa_start </li> <li> s:event:type=stall </li> <li> s:event:type=end </li> </ul> |
| l:event:prev_ts | Media-SDK | (Vereist)<br/><br/>Het tijdstempel van de laatste gebeurtenis van hetzelfde type in deze sessie. De waarde is -1. |
| l:event:ts | Media-SDK | (Vereist)<br/><br/>Het tijdstempel van de gebeurtenis. |
| l:event:duur | Media-SDK | (Vereist)<br/><br/>Deze waarde wordt intern (in milliseconden) ingesteld door de Media SDK, niet door de speler. Het wordt gebruikt om de tijd te berekenen gebruikte metriek op het achterste eind. Bijvoorbeeld: a.media.totalTimePlayed wordt berekend als som van de duur voor alle spelen (type=play) hartslagen die worden geproduceerd. <br/>*Opmerking:* Deze parameter wordt ingesteld op 0 voor bepaalde gebeurtenissen omdat dit &#39;state change events&#39; zijn (bijvoorbeeld type=complete, type=chapter_complete of type=bitrate_change.) |
| l:event:afspeelkop | VideoInfo | (Vereist)<br/><br/>De afspeelkop stond in het actieve element (hoofd of advertentie) toen de gebeurtenis werd opgenomen. |
| s:event:zand | Media-SDK | (Vereist)<br/><br/>De sessie-id (een willekeurig gegenereerde tekenreeks). Alle gebeurtenissen in een bepaalde sessie (video + advertenties) moeten hetzelfde zijn. |
| l:asset:duration / l:asset:length <br/>(Naam wijzigen van duur) | VideoInfo | (Vereist)<br/><br/>De lengte van het video-element van het hoofdelement. |
| s:asset:uitgever | MediaHeartboneConfig | (Vereist)<br/><br/>De uitgever van het element. |
| s:asset:video_id | VideoInfo | (Vereist)<br/><br/>Een unieke id die de video in de catalogus van de uitgever identificeert. |
| s:asset:type | Media-SDK | (Vereist)<br/><br/>Het type element (hoofd of advertentie). |
| s:stream:type | VideoInfo | (Vereist)<br/><br/>Het streamtype. Kan een van de volgende opties zijn: <ul> <li> leven </li> <li> vod </li> <li> lineair </li> </ul> |
| s:user:id | Config-object voor mobiele toepassing, weergaveid voor toepassingsmeting | (Optioneel)<br/><br/>Door de gebruiker ingestelde bezoeker-id. |
| s:user:steun | Experience Cloud Org | (Optioneel)<br/><br/>De waarde van de Analytics Visitor ID van de gebruiker. |
| s:user:midden | Experience Cloud Org | (Vereist)<br/><br/>De waarde van de Experience cloud bezoeker-id van de gebruiker. |
| s:cuser:customer_user_ids_x | MediaHeartboneConfig | (Optioneel)<br/><br/>Alle gebruikers-id&#39;s van de klant zijn ingesteld op Audience Manager. |
| l:aam:loc_hint | MediaHeartboneConfig | (Vereist)<br/><br/>Gegevens AAM verzonden op elke lading na aa_start |
| s:aam:opblazen | MediaHeartboneConfig | (Vereist)<br/><br/>Gegevens AAM verzonden op elke lading na aa_start |
| s:sc:razend | Uitsluitings-id (of id&#39;s) rapporteren | (Vereist)<br/><br/>Adobe Analytics RSID waar de rapporten zouden moeten worden verzonden. |
| s:sc:tracking_server | MediaHeartboneConfig | (Vereist)<br/><br/>Adobe Analytics-traceringsserver. |
| h:sc:ssl | MediaHeartboneConfig | (Vereist)<br/><br/>Geeft aan of het verkeer plaatsvindt via HTTPS (indien ingesteld op 1) of via HTTP (is ingesteld op 0). |
| s:sp:ovp | MediaHeartboneConfig | (Optioneel)<br/><br/>Stel dit in op &#39;primetime&#39; voor primetime-spelers of op de werkelijke OVP voor andere spelers. |
| s:sp:sdk | MediaHeartboneConfig | (Vereist)<br/><br/>De OVP-versietekenreeks. |
| s:sp:player_name | VideoInfo | (Vereist)<br/><br/>De naam van de videospeler (de daadwerkelijke spelersoftware, die wordt gebruikt om de speler te identificeren). |
| s:sp:kanaal | MediaHeartboneConfig | (Optioneel)<br/><br/>Het kanaal waar de gebruiker de inhoud bekijkt. Voor een mobiele app, de naam van de app. De domeinnaam voor een website. |
| s:sp:hb_version | Media-SDK | (Vereist)<br/><br/>Het versienummer van de bibliotheek van Media SDK die de vraag uitgeeft. |
| l:stream:bitsnelheid | QoSInfo | (Vereist)<br/><br/>De huidige waarde van de streambitsnelheid (in bps). |

## Foutgebeurtenissen

| Naam | Gegevensbron | Beschrijving   |
| ---  | --- | --- |
| s:event:bron | Media-SDK | (Vereist)<br/><br/>De bron van de fout, of speler-intern, of toepassing-niveau. |
| s:event:id | Media-SDK | (Vereist)<br/><br/>Fout-id; identificeert de fout op unieke wijze. |

## Gebeurtenissen toevoegen

| Naam | Gegevensbron | Beschrijving   |
| ---  | --- | --- |
| s:asset:ad_id | AdInfo | (Vereist)<br/><br/>De naam van de advertentie. |
| s:asset:ad_sid | Media-SDK | (Vereist)<br/><br/>Een unieke id die wordt gegenereerd door de Media SDK en die wordt toegevoegd aan alle advertentiegerelateerde pings. |
| s:asset:pod_id | Media-SDK | (Vereist)<br/><br/>Pod-id in de video. Deze waarde wordt automatisch berekend op basis van de volgende formule: <br/>`MD5(video_id) + `<br/>`"_" + `<br/>`[pod index]` |
| s:asset:pod_position | AdBreakInfo | (Vereist)<br/><br/>Index van de advertentie in de pod (de eerste advertentie heeft index 0, de tweede advertentie heeft index 1, enz.). |
| s:asset:oplosmiddel | AdBreakInfo | (Vereist)<br/><br/>De advertentiesolver. |
| s:meta:custom_ad_metadata.x | MediaHeartbone | (Optioneel)<br/><br/>De aangepaste en metagegevens. |

## Gebeurtenissen van hoofdstuk

| Naam | Gegevensbron | Beschrijving   |
| ---  | --- | --- |
| s:stream:hoofdstuk_sid | Media-SDK | (Vereist)<br/><br/>De unieke id die aan de afspeelinstantie van het hoofdstuk is gekoppeld.  <br/> **Opmerking:** Een hoofdstuk kan meerdere keren worden afgespeeld vanwege terugzoekbewerkingen die door de gebruiker worden uitgevoerd. |
| s:stream:hoofdstuk_naam | ChapterInfo | (Optioneel)<br/><br/>De vriendelijke (leesbare) naam van het hoofdstuk. |
| s:stream:hoofdstuk_id | Media-SDK | (Vereist)<br/><br/>De unieke id van het hoofdstuk. Deze waarde wordt automatisch berekend op basis van de volgende formule: <br/>`MD5(video_id) +`<br/>` "_" +`<br/>`chapter_pos` |
| l:stream:hoofdstuk_pos | ChapterInfo | (Vereist)<br/><br/>De index van het hoofdstuk in de lijst met hoofdstukken (te beginnen met 1). |
| l:stream:hoofdstuk_offset | ChapterInfo | (Vereist)<br/><br/>De verschuiving van het hoofdstuk (uitgedrukt in seconden) binnen de hoofdinhoud, exclusief advertenties. |
| l:stream:hoofdstuk_lengte | ChapterInfo | (Vereist)<br/><br/>De duur van het hoofdstuk (uitgedrukt in seconden). |
| s:meta:custom_chapter_metadata.x | ChapterInfo | (Optioneel)<br/><br/>Metagegevens van aangepaste hoofdstukken. |

## Gebeurtenis einde sessie

| Naam | Gegevensbron | Beschrijving   |
| ---  | --- | --- |
| s:event:type=end | Media-SDK | (Vereist)<br/><br/> De `end` `close` |
