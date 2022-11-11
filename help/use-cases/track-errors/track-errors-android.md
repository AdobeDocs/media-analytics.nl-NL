---
title: Meer informatie over het bijhouden van fouten op Android
description: Meer informatie over het implementeren van foutcontrole met de Media SDK op Android.
uuid: 7d0c77e5-924c-4619-8e29-3484748ab736
exl-id: 6c4f693d-45c0-4a9c-bda1-c8721afe31f5
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# Fouten bijhouden op Android{#track-errors-on-android}

De volgende instructies bieden richtlijnen voor implementatie met 2.x SDK&#39;s.

>[!IMPORTANT]
>
>Als u een 1.x-versie van de SDK implementeert, kunt u de 1.x-handleidingen voor ontwikkelaars hier downloaden: [SDK&#39;s downloaden.](/help/getting-started/download-sdks.md)

1. Fouten met mediaspeler bijhouden:

   ```java
   public void onPlayerError(Observable observable, Object data) {  
       _heartbeat.trackError("mediaErrorID");
   }
   ```

>[!NOTE]
>
>Fouten bij het bijhouden van mediaspeler stoppen de mediatrackingsessie niet. Als de fout in de mediaspeler voorkomt dat het afspelen wordt voortgezet, controleert u of de mediatrackingsessie is gesloten door `trackSessionEnd` na het aanroepen `trackError`.
