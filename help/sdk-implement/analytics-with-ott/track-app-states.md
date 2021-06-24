---
title: App-statussen bijhouden
description: 'Toepassingsstaten zijn de verschillende schermen of weergaven in uw toepassing. Leer hoe u de toepassingsstatus in uw toepassing kunt bijhouden met behulp van de trackState-oproep. '
uuid: 2f98fb43-c362-4a9b-8732-fa7e963da729
exl-id: bb1e0eee-7c59-40b4-9359-a7441b9686b8
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 2%

---

# Toepassingsstaten bijhouden{#track-app-states}

Frames zijn de verschillende schermen of weergaven in uw toepassing. Telkens wanneer een nieuwe staat in uw toepassing wordt getoond, zou u een `trackState` vraag moeten verzenden. Wanneer een gebruiker bijvoorbeeld van de startpagina naar het scherm met videodetails navigeert, verzendt u een `trackState`-aanroep. Frames worden meestal weergegeven met behulp van een tekenrapport, zodat u kunt zien hoe gebruikers door uw app navigeren en welke frames het meest worden weergegeven.

## trackState-oproepen

U roept `trackState` gewoonlijk elke keer wanneer app een nieuw scherm laadt.

### Roku

```js
ADBMobile().trackState("State Name", {})
```

### Chromecast

```js
ADBMobile.analytics.trackState("State Name",{});
```

De staatsnaam wordt vermeld in de &quot;staat van de Mening&quot;variabele in de Mobiele diensten van Adobe, en een mening wordt geregistreerd voor elke `trackState` vraag. In andere analytische interfaces, wordt de &quot;Staat van de Mening&quot;gerapporteerd als &quot;Naam van de Pagina&quot;; &quot;Statusweergaven&quot; wordt gerapporteerd als &quot;Paginaweergaven&quot;.

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
>De waarden van contextgegevens moeten aan douanevariabelen in de Mobiele diensten van Adobe worden in kaart gebracht.
