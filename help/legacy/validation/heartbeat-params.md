---
title: Beschrijvingen van hartslagparameters
description: Verken de hartslagparameters die Adobe verzamelt en verwerkt op de Media Analytics-server (heartbeats).
uuid: e9ddda32-0952-43d0-a702-49f5b1bfd8cf
exl-id: ffa67b5e-ee54-4a5b-8064-decd108f944b
feature: "Streaming Media, Variables"
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 4%

---

# Beschrijving van de parameter Media Analytics (heartbeats){#heartbeat-parameter-descriptions}

Lijst met parameters voor Media Analytics die Adobe verzamelt en verwerkt op de Media Analytics-server (heartbeats):

## Alle gebeurtenissen

| Naam | Data Source |  Beschrijving  |
| ---  | --- | --- |
| `s:event:type` | Media-SDK | (Vereist) <br/><br/> het type van de gebeurtenis die wordt gevolgd. Gebeurtenistypen: <ul> <li> s:event: type=start </li> <li> `s:event:type=complete` </li> <li> `s:event:type=chapter_start` </li> <li> `s:event:type=chapter_complete` </li> <li> `s:event:type=buffer` </li> <li> `s:event:type=pause` </li> <li> `s:event:type=resume` </li> <li> `s:event:type=bitrate_change` </li> <li> `s:event:type=aa_start` </li> <li> `s:event:type=stall` </li> <li> `s:event:type=end` </li> </ul> |
| `l:event:prev_ts` | Media-SDK | (Vereist) <br/><br/> timestamp van de laatste gebeurtenis van het zelfde type in deze zitting. De waarde is -1. |
| `l:event:ts` | Media-SDK | (Vereist) <br/><br/> timestamp van de gebeurtenis. |
| `l:event:duration` | Media-SDK | (Vereist) <br/><br/> Deze waarde wordt geplaatst intern (in milliseconden) door Media SDK, niet door de speler. Het wordt gebruikt om de tijd te berekenen gebruikte metriek op het achterste eind. Bijvoorbeeld: a.media.totalTimePlayed wordt berekend als som van de duur voor alle (type=play)hartslagen van het Spel die worden geproduceerd. <br/>*Nota:* Deze parameter wordt geplaatst aan 0 voor bepaalde gebeurtenissen omdat zij &quot;de gebeurtenissen van de staatsverandering&quot;zijn (b.v., type=complete, type=chapter_complete, of type=bitrate_change.) |
| `l:event:playhead` | VideoInfo | (Vereist) <br/><br/> playhead was binnen de momenteel actieve activa (hoofd of advertentie), toen de gebeurtenis werd geregistreerd. |
| `s:event:sid` | Media-SDK | (Vereist) <br/><br/> Sessieidentiteitskaart (een willekeurig geproduceerd koord). Alle gebeurtenissen in een bepaalde sessie (video + advertenties) moeten hetzelfde zijn. |
| `l:asset:duration` / `l:asset:length` <br/> (hernoemd van lengteduur) | VideoInfo | (Vereist) <br/><br/> de videomateriaal lengte van het belangrijkste activa. |
| `s:asset:publisher` | MediaHeartboneConfig | (Vereist) <br/><br/> de uitgever van de activa. |
| `s:asset:video_id` | VideoInfo | (Vereist) <br/><br/> identiteitskaart uniek identificeert de video in de catalogus van de uitgever. |
| `s:asset:type` | Media-SDK | (Vereist) <br/><br/> het activatype (hoofd of advertentie). |
| `s:stream:type` | VideoInfo | (Vereist) <br/><br/> het stroomtype. Kan een van de volgende opties zijn: <ul> <li> leven </li> <li> vod </li> <li> lineair </li> </ul> |
| `s:user:id` | Config-object voor mobiele toepassing, weergaveid voor toepassingsmeting | (Facultatief) <br/><br/> specifiek plaatste identiteitskaart van de Gebruiker van de Bezoeker. |
| `s:user:aid` | Experience Cloud Org | (Facultatief) <br/><br/> de waarde van identiteitskaart van de Bezoeker van de Analyse van de gebruiker. |
| `s:user:mid` | Experience Cloud Org | (Vereist) <br/><br/> de waarde van identiteitskaart van de de wolkenbezoeker van de Ervaring van de gebruiker. |
| `s:cuser:customer_user_ids_x` | MediaHeartboneConfig | (Facultatief) <br/><br/> Alle die klantengebruiker IDs op Audience Manager wordt geplaatst. |
| `l:aam:loc_hint` | MediaHeartboneConfig | (Vereist) <br/><br/> die gegevens van AAM op elke nuttige lading na aa_start worden verzonden |
| `s:aam:blob` | MediaHeartboneConfig | (Vereist) <br/><br/> die gegevens van AAM op elke nuttige lading na aa_start worden verzonden |
| `s:sc:rsid` | Uitsluitings-id (of id&#39;s) rapporteren | (Vereist) <br/><br/> Adobe Analytics RSID waar de rapporten zouden moeten worden verzonden. |
| `s:sc:tracking_server` | MediaHeartboneConfig | (Vereist) <br/><br/> het volgen van Adobe Analytics server. |
| `h:sc:ssl` | MediaHeartboneConfig | (Vereist) <br/><br/> of het verkeer over HTTPS (als reeks aan 1) of over HTTP (wordt geplaatst aan 0) is. |
| `s:sp:ovp` | MediaHeartboneConfig | (Facultatief) <br/><br/> plaatste aan &quot;primetime&quot;voor spelers Primetime, of daadwerkelijke OVP voor andere spelers. |
| `s:sp:sdk` | MediaHeartboneConfig | (Vereist) <br/><br/> het OVP versiekoord. |
| `s:sp:player_name` | VideoInfo | (Vereist) <br/><br/> Video spelernaam (de daadwerkelijke spelersoftware, die wordt gebruikt om de speler te identificeren). |
| `s:sp:channel` | MediaHeartboneConfig | (Facultatief) <br/><br/> het kanaal waar de gebruiker de inhoud kijkt. Voor een mobiele app, de naam van de app. De domeinnaam voor een website. |
| `s:sp:hb_version` | Media-SDK | (Vereist) <br/><br/> het versieaantal van de bibliotheek van Media SDK die de vraag uitgeeft. |
| `l:stream:bitrate` | QoSInfo | (Vereist) <br/><br/> De huidige waarde van de stroom bitrate (in bps). |

## Foutgebeurtenissen

| Naam | Data Source | Beschrijving   |
| ---  | --- | --- |
| `s:event:source` | Media-SDK | (Vereist) <br/><br/> de bron van de fout, of speler-intern, of toepassing-niveau. |
| `s:event:id` | Media-SDK | (Vereist) <br/><br/> identiteitskaart van de Fout, identificeert uniek de fout. |

## Gebeurtenissen toevoegen

| Naam | Data Source | Beschrijving   |
| ---  | --- | --- |
| `s:asset:ad_id` | AdInfo | (Vereist) <br/><br/> de naam van de advertentie. |
| `s:asset:ad_sid` | Media-SDK | (Vereist) <br/><br/> een uniek herkenningsteken dat door de Media SDK wordt geproduceerd, die aan alle op elkaar betrekking hebbende pingelt wordt toegevoegd. |
| `s:asset:pod_id` | Media-SDK | (Vereist) <br/><br/> identiteitskaart van de Pod binnen de video. Deze waarde wordt automatisch berekend op basis van de volgende formule: <br/>`MD5(video_id) + `<br/>`"_" + `<br/>`[pod index]` |
| `s:asset:pod_position` | AdBreakInfo | (Vereist) <br/><br/> Index van de advertentie binnen de pod (eerste advertentie heeft index 0, tweede advertentie heeft index 1, enz.). |
| `s:asset:resolver` | AdBreakInfo | (Vereist) <br/><br/> de advertentieresolver. |
| `s:meta:custom_ad_metadata.x` | MediaHeartbone | (Facultatief) <br/><br/> de douane en meta-gegevens. |

## Gebeurtenissen van hoofdstuk

| Naam | Data Source | Beschrijving   |
| ---  | --- | --- |
| `s:stream:chapter_sid` | Media-SDK | (Vereist) <br/><br/> het unieke herkenningsteken verbonden aan de playbackinstantie van het hoofdstuk.  <br/> **Nota:** Een hoofdstuk kan veelvoudige tijden toe te schrijven aan zoek-achterverrichtingen worden gespeeld die door de gebruiker worden uitgevoerd. |
| `s:stream:chapter_name` | ChapterInfo | (Facultatief) <br/><br/> de vriendschappelijke (d.w.z., menselijke leesbare) naam van het hoofdstuk. |
| `s:stream:chapter_id` | Media-SDK | (Vereist) <br/><br/> unieke identiteitskaart van het hoofdstuk. Deze waarde wordt automatisch berekend op basis van de volgende formule: <br/>`MD5(video_id) +`<br/>` "_" +`<br/>`chapter_pos` |
| `l:stream:chapter_pos` | ChapterInfo | (Vereist) <br/><br/> de index van het hoofdstuk in de lijst van hoofdstukken (beginnend met 1). |
| `l:stream:chapter_offset` | ChapterInfo | (Vereist) <br/><br/> de compensatie van het hoofdstuk (die in seconden wordt uitgedrukt) binnen de belangrijkste inhoud, exclusief advertenties. |
| `l:stream:chapter_length` | ChapterInfo | (Vereist) <br/><br/> de duur van het hoofdstuk (die in seconden wordt uitgedrukt). |
| `s:meta:custom_chapter_metadata.x` | ChapterInfo | (Facultatief) <br/><br/> meta-gegevens van het hoofdstuk van de Douane. |

## Gebeurtenis einde sessie

| Naam | Data Source | Beschrijving   |
| ---  | --- | --- |
| `s:event:type=end` | Media-SDK | (Vereist) <br/><br/> De `end` `close` |
