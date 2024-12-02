---
title: Media Streaming Segmenten beschreven
description: Leer over de rapporterende segmenten verbonden aan het Type van Stroom van Media met inbegrip van het Segment, de Beschrijving, en de Regel voor het Type van Stroom van Media.
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
exl-id: a450801c-0d6b-4e2a-8662-f00aaaa6e4e0
feature: "Media Analytics, Segmentation"
role: User, Admin, Data Engineer
source-git-commit: b15a81dc8f08e94c9b80d66019f3d0fe95ef5a74
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# Mediasegmenten{#segments}

Met segmenten kunt u subsets bezoekers identificeren op basis van kenmerken of interacties op de website. Met streaming-mediasegmenten kunt u het stroomtype van de bezoeker identificeren, zoals audio-, live- of podcast-streams. Voor informatie over de segmenten van Adobe Analytics, zie [ Ongeveer segmenten en containers ](https://experienceleague.adobe.com/docs/analytics/components/segmentation/seg-overview.html?lang=en) in de Gids van de Componenten van Adobe Analytics.

>[!NOTE]
>
>Deze rapportsegmenten die aan het Type van Stream van Media zijn gekoppeld werden op 13/18 9 geïntroduceerd samen met de `streamType` parameter.

| Segment | Beschrijving | Regel |
|---|---|---|
| Type mediastream: alle | Segmenteer alle *media* stroomgegevens | &quot;Inhoud (ID) bestaat&quot; |
| Type mediastroom: Audio | Segmenteer alle *audio* stroomgegevens | &quot;Content (ID) exists&quot; EN &quot;Media Stream Type = `audio`&quot; |
| Type mediastroom: Video | Segmenteer alle *video* stroomgegevens | &quot;Content (ID) exists&quot; EN &quot;Media Stream Type != `audio`&quot; |
| Type media-inhoud: VoD | Alle VoD-inhoud segmenteren | &quot;Inhoudstype = `vod`&quot; |
| Type media-inhoud: Actief | Alle actieve inhoud segmenteren | &quot;Inhoudstype = `live`&quot; |
| Type media-inhoud: lineair | Alle lineaire inhoud segmenteren | &quot;Inhoudstype = `linear`&quot; |
| Type media-inhoud: Podcast | Alle inhoud van podcast segmenteren | &quot;Inhoudstype = `podcast`&quot; |
| Type media-inhoud: Audiobook | Alle inhoud van Audiobook segmenteren | &quot;Inhoudstype = `audiobook`&quot; |
| Type media-inhoud: AoD | Alle AoD-inhoud segmenteren | &quot;Inhoudstype = `aod`&quot; |
