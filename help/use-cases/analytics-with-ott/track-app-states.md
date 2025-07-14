---
title: App-statussen bijhouden
description: Toepassingsstaten zijn de verschillende schermen of weergaven in uw toepassing. Leer hoe u de toepassingsstatus in uw toepassing kunt bijhouden met behulp van de trackState-oproep.
uuid: 2f98fb43-c362-4a9b-8732-fa7e963da729
exl-id: bb1e0eee-7c59-40b4-9359-a7441b9686b8
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# Toepassingsstaten bijhouden{#track-app-states}

Frames zijn de verschillende schermen of weergaven in uw toepassing. Telkens wanneer een nieuwe staat in uw toepassing wordt getoond, zou u een `trackState` vraag moeten verzenden. Wanneer een gebruiker bijvoorbeeld van de startpagina naar het scherm met videodetails navigeert, stuurt u een `trackState` -aanroep. Frames worden meestal weergegeven met behulp van een tekenrapport, zodat u kunt zien hoe gebruikers door uw app navigeren en welke frames het meest worden weergegeven.

## trackState-oproepen

Doorgaans roept u `trackState` aan wanneer de toepassing een nieuw scherm laadt.

### Roku

```js
ADBMobile().trackState("State Name", {})
```

### Chromecast

```js
ADBMobile.analytics.trackState("State Name",{});
```

De statusnaam wordt vermeld in de variabele &quot;View State&quot; in Adobe Mobile-services en een weergave wordt opgenomen voor elke `trackState` -aanroep. In andere Analytics-interfaces wordt &quot;View State&quot; gerapporteerd als &quot;Page Name&quot;; &quot;State Views&quot; als &quot;Page Views&quot;.

## Contextgegevens verzenden

Naast &quot;de Naam van de Staat&quot;, kunt u extra contextgegevens met elke vraag van de spoorstaat verzenden.

### Roku

```js
dictionary = { } 
dictionary["myapp.login.LoginStatus"] = "logged in"  
ADBMobile().trackState("Home Screen", dictionary)
```

### Chromecast

```js
var dictionary = { }; 
dictionary["myapp.login.LoginStatus"] = "logged in"; 
ADBMobile.analytics.trackState("Home Screen", dictionary); 
```

>[!NOTE]
>
>Contextgegevenswaarden moeten worden toegewezen aan aangepaste variabelen in Adobe Mobile-services.
