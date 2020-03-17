---
title: Toepassingsstaten bijhouden
description: 'App-statussen zijn de verschillende schermen of weergaven in uw toepassing. Wanneer deze worden weergegeven, moet dit resulteren in een trackState-aanroep. '
uuid: 2f98fb43-c362-4a9b-8732-fa7e963da729
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Toepassingsstaten bijhouden{#track-app-states}

Frames zijn de verschillende schermen of weergaven in uw toepassing. Telkens als een nieuw staat in uw toepassing wordt getoond, zou u een `trackState` vraag moeten verzenden. Wanneer een gebruiker bijvoorbeeld van de startpagina naar het scherm met videodetails navigeert, stuurt u een `trackState` aanroep. Frames worden meestal weergegeven met behulp van een tekenrapport, zodat u kunt zien hoe gebruikers door uw app navigeren en welke frames het meest worden weergegeven.

## trackState-oproepen

U roept doorgaans `trackState` telkens wanneer de toepassing een nieuw scherm laadt.

### Roku

```js
ADBMobile().trackState("State Name", {})
```

### Chromecast

```js
ADBMobile.analytics.trackState("State Name",{});
```

De statusnaam wordt vermeld in de variabele &quot;View State&quot; in Adobe Mobile-services en er wordt voor elke `trackState` aanroep een weergave opgenomen. In andere analytische interfaces, wordt de &quot;Staat van de Mening&quot;gerapporteerd als &quot;Naam van de Pagina&quot;; &quot;Statusweergaven&quot; wordt gerapporteerd als &quot;Paginaweergaven&quot;.

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

