---
title: Segmenten
description: Segmenten
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
exl-id: a450801c-0d6b-4e2a-8662-f00aaaa6e4e0
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 12%

---

# Segmenten{#segments}

>[!NOTE]
>
>Deze rapporteringssegmenten verbonden aan het Type van Stream van Media werden geïntroduceerd op 9/13/18 samen met de `streamType` parameter.

| Segment | Beschrijving | Regel |
|---|---|---|
| Type mediastroom: Alles | Alle *media* streamgegevens segmenteren | &quot;Inhoud (ID) bestaat&quot; |
| Type mediastroom: Audio | Alle *audio* streamgegevens segmenteren | &quot;Content (ID) exists&quot; EN &quot;Media Stream Type = `audio`&quot; |
| Type mediastroom: Video | Alle *video* streamgegevens segmenteren | &quot;Content (ID) exists&quot; EN &quot;Media Stream Type != `audio`&quot; |
| Type media-inhoud: VoD | Alle VoD-inhoud segmenteren | &quot;Inhoudstype = `vod`&quot; |
| Type media-inhoud: Live | Alle actieve inhoud segmenteren | &quot;Inhoudstype = `live`&quot; |
| Type media-inhoud: Lineair | Alle lineaire inhoud segmenteren | &quot;Inhoudstype = `linear`&quot; |
| Type media-inhoud: Podcast | Alle inhoud van podcast segmenteren | &quot;Inhoudstype = `podcast`&quot; |
| Type media-inhoud: Audiobook | Alle inhoud van Audiobook segmenteren | &quot;Inhoudstype = `audiobook`&quot; |
| Type media-inhoud: AoD | Alle AoD-inhoud segmenteren | &quot;Inhoudstype = `aod`&quot; |
