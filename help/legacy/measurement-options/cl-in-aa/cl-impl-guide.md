---
title: Implementatie aangepaste koppeling beschreven
description: Leer hoe te om het volgen van de Verbinding van de Douane in het Streamen toe:voegen-on van de Inzameling van Media uit te voeren.
uuid: 83315e73-20ca-4db5-9d43-33daade45a13
exl-id: ee6f931a-ef80-4ebe-8ccb-cdbf970516e6
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# Custom Link Implementation Guide{#custom-link-implementation-guide}

Bij Aangepaste videotracering wordt handmatig koppelingen bijgehouden met behulp van aangepaste koppelingscode in Analytics `appMeasurement`.
Het meest wordt aangepaste videotracering van koppelingen gebruikt op platforms en apparaten waar minimale videometing nodig is.

* In JavaScript: de `s.tl()` function
* In mobiele toepassingen: [trackAction() Android](https://experienceleague.adobe.com/docs/mobile-services/android/analytics-android/actions.html), [trackAction() iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/analytics-ios/actions.html), [trackAction() OTT](/help/use-cases/analytics-with-ott/track-app-actions.md)
* In de API voor gegevensinvoeging: [linktype-tag](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/reference/r_supported_tags.md)

## Vereisten

* Toegang tot API-gebeurtenissen en -gegevens van videospeler
* Mogelijkheid om scripts toe te voegen bij gebruik van Analytics SDK
* Mogelijkheid om tekstspatiëringsbakens toe te voegen (aangepaste scripts of hardcode) bij gebruik van de API voor gegevensinvoeging

## Metagegevens

* Metagegevens kunnen aan elke volgende aanroep worden toegevoegd als onderdeel van de koppelingsgegevens
* Vergeet niet de `linkTrackVars` en `linkTrackEvents`

```javascript
/* Call on video complete */

if (e.type == "ended") {  
    s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15';
    s.linkTrackEvents = 'event3';
    s.prop10 = mediaName;
    s.eVar10 = mediaName;
    s.eVar12 = "video";
    s.eVar13 = document.title;
    s.eVar15 = mediaPlayerName;
    s.events = 'event3';
    s.tl(this,'o','Video Complete');
};
```

## Waarom aangepaste koppeling gebruiken

* Minimale voorwaarden zijn vereist
* Werkt op elk platform, inclusief geen script
* Alle berekeningen, zoals gebruikte tijd of kwartielen, moeten in een aangepast script worden berekend
* Heel eenvoudig zonder verborgen bibliotheken of scripts
* Totale controle over elk aspect van de videogegevens

## Voorbeeld JavaScript for HTML5 Player

```javascript
<script type="text/javascript">
  myvideo = document.getElementById('movie');
  myvideo.addEventListener('play',myHandler,false);
  myvideo.addEventListener('seeked',myHandler,false);
  myvideo.addEventListener('seeking',myHandler,false);
  myvideo.addEventListener('pause',myHandler,false);
  myvideo.addEventListener('ended',myHandler,false);

  function myHandler(e) {
      var video = document.getElementsByTagName('video')[0];
      var mediaName="13502979:Sailing";
      var mediaLength = video.duration;
      var mediaPlayerName = "HTML5 Player";
      /*Define video offset*/
      if (video.currentTime > 0) {
          mediaOffset = Math.floor(video.currentTime);
      } else {
          mediaOffset = 0;
      };
      /*Call on video start*/
      if (e.type == "play") {
          if (mediaOffset == 0) {
              console.log(mediaPlayerName +
                ' -> start -> playhead: ' +  
                Math.floor(video.currentTime));
              s.linkTrackVars='events,prop10,eVar10,eVar12,eVar13,eVar15';
              s.linkTrackEvents='event2';
              s.prop10=mediaName;
              s.eVar10=mediaName;
              s.eVar12="video";
              s.eVar13=document.title;
              s.eVar15=mediaPlayerName;
              s.events='event2';
              s.tl(this,'o','Video Start');
          }
      };

      /*Call on video pause*/
      if (e.type == "pause") {
          console.log(mediaPlayerName +' -> pause -> playhead: ' + Math.floor(video.currentTime));
          if (video.currentTime != video.duration) {
              s.linkTrackVars='events,prop10,eVar10,eVar12,eVar13,eVar15';
              s.linkTrackEvents='event7';
              s.prop10=mediaName;
              s.eVar10=mediaName;
              s.eVar12="video";
              s.eVar13=document.title;
              s.eVar15=mediaPlayerName;
              s.events='event7';
              s.tl(this,'o','Video Pause');
          }
      };

      /*Call on video complete*/
      if (e.type == "ended") {
          console.log(mediaPlayerName +
            ' -> ended -> playhead: ' +
            Math.floor(video.currentTime));
          s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15';
          s.linkTrackEvents = 'event3';
          s.prop10= m ediaName;
          s.eVar10=mediaName;
          s.eVar12="video";
          s.eVar13=document.title;
          s.eVar15=mediaPlayerName;
          s.events='event3';
          s.tl(this,'o','Video Complete');
      };
  };
</script>
```
