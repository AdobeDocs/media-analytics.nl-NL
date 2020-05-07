---
title: Custom Link-implementatiegids
description: null
uuid: 83315e73-20ca-4db5-9d43-33daade45a13
translation-type: tm+mt
source-git-commit: 72cdf2d03ebae6998514c9092ab462c29345c9f9
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 2%

---


# Custom Link Implementatiehandleiding{#custom-link-implementation-guide}

Bij Aangepaste videotracering wordt [handmatig koppelingen bijgehouden met behulp van aangepaste koppelingscode](https://docs.adobe.com/content/help/en/media-analytics/using/measurement-options/cl-in-aa/cl-impl-guide.html) in Analytics `appMeasurement`.
Het meest wordt aangepaste videotracering van koppelingen gebruikt op platforms en apparaten waar minimale videometing nodig is.

* In JavaScript: de `s.tl()` functie
* In mobiele toepassingen: [trackAction() Android](https://docs.adobe.com/content/help/en/mobile-services/android/analytics-android/actions.html), [trackAction() iOS](https://docs.adobe.com/content/help/en/mobile-services/ios/analytics-ios/actions.html), [trackAction() OTT](/help/sdk-implement/analytics-with-ott/track-app-actions.md)
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

## Voorbeeld-JavaScript voor HTML5 Player

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
