---
title: Segmenten
description: '"Leer over de rapporterende segmenten verbonden aan het Type van Stream van Media met inbegrip van het Segment, de Beschrijving, en de Regel voor het Type van Stroom van Media."'
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
exl-id: a450801c-0d6b-4e2a-8662-f00aaaa6e4e0
feature: '"Media Analytics, Segmentation"'
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 10%

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
