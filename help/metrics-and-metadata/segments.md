---
title: Media Streaming Segmenten beschreven
description: '"Leer over de rapporterende segmenten verbonden aan het Type van Stream van Media met inbegrip van het Segment, de Beschrijving, en de Regel voor het Type van Stroom van Media."'
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
exl-id: a450801c-0d6b-4e2a-8662-f00aaaa6e4e0
feature: '"Media Analytics, Segmentation"'
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: 2d9d4352b0fd71710a9952ba4a77f6796ea9f5cc
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 6%

---

# Segmenten{#segments}

Met segmenten kunt u subsets bezoekers identificeren op basis van kenmerken of interacties op de website. Met streaming-mediasegmenten kunt u het stroomtype van de bezoeker identificeren, zoals audio-, live- of podcast-streams. Voor informatie over de segmenten van Adobe Analytics, zie [Informatie over segmenten en containers](https://experienceleague.adobe.com/docs/analytics/components/segmentation/seg-overview.html?lang=en) in de Gids van de Componenten van Adobe Analytics.

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
