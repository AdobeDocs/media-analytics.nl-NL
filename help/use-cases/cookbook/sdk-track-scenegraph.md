---
title: Tracking in SceneGraph (Roku)
description: Leer hoe te om media met het Roku SceneGraph XML programmeringskader te volgen.
uuid: fa85e546-c79b-4df4-8c03-d6593fa296d5
exl-id: e428d3cd-dbc7-48bb-82ff-61b6b892884c
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 1%

---

# Roku — Tekstspatiëring in SceneGraph {#tracking-in-scenegraph-roku}

## Inleiding {#introduction}

U kunt het Roku programmeringskader van XML gebruiken SceneGraph om toepassingen te ontwikkelen. Dit kader heeft twee belangrijke concepten:

* SceneGraph-rendering van de toepassingsschermen
* De configuratie van XML van de schermen SceneGraph

De Adobe Mobile SDK for Roku is geschreven in BrightScript. De SDK gebruikt vele componenten die niet beschikbaar voor een app zijn die op SceneGraph (bijvoorbeeld, draden) loopt. Daarom kan een ontwikkelaar van een Roku-app die het SceneGraph-framework wil gebruiken, geen Adobe Mobile SDK API&#39;s aanroepen (deze zijn vergelijkbaar met de API&#39;s die beschikbaar zijn in oudere BrightScript-toepassingen).

## Architectuur {#architecture}

Adobe heeft een nieuwe API toegevoegd die een verbindingsbrug maakt tussen de AdobeMobile SDK en `adbmobileTask` om SceneGraph-ondersteuning toe te voegen aan de AdobeMobile SDK. Dit laatste is een SceneGraph-knooppunt dat wordt gebruikt voor de uitvoering van de SDK API. (Het gebruik van `adbmobileTask` wordt in de rest van dit document uitgebreid uitgelegd.)

De verbindingsbrug is ontworpen om als volgt te presteren:

* De bridge retourneert een instantie die compatibel is met SceneGraph van Adobe Mobile SDK. De SceneGraph-compatibele SDK heeft alle APIs die erfenis SDK blootstelt.
* U gebruikt AdobeMobile SDK APIs in SceneGraph op een zeer gelijkaardige manier als hoe u verouderde APIs gebruikte.
* De bridge stelt ook een mechanisme beschikbaar om te luisteren naar callbacks voor API&#39;s die bepaalde gegevens retourneren.

![](assets/SceneGraph_arch.png)

## Onderdelen {#components}

**Toepassing SceneGraph:**

* Verbruikt `AdobeMobileLibrary` APIs via SceneGraph schakelaarbrug APIs.
* Registreert voor callbacks van reacties op `adbmobileTask` voor verwachte variabelen van outputgegevens.

**AdobeMobileLibrary:**

* Stelt een reeks openbare APIs (Verouderd), met inbegrip van de schakelaarbrug API bloot.
* Retourneert een SceneGraph-connectorinstantie die alle oudere openbare API&#39;s omvat.
* Communiceert met een `adbmobileTask` knoop SceneGraph voor uitvoering van APIs.

**adbmobileTask Node:**

* Een SceneGraph taakknoop die `AdobeMobileLibrary` APIs op een achtergronddraad uitvoert.
* Fungeert als afgevaardigde om gegevens terug te sturen naar toepassingsscènes.

## Public SceneGraph-API&#39;s {#public-scenegraph-apis}

### ADBMobileConnector

| Categorie | Naam methode | Beschrijving |
|---|---|---|
| **Constanten** | |  |
|  | `sceneGraphConstants` | Retourneert een object dat `SceneGraphConstants` bevat. Zie de bovenstaande tabel voor meer informatie. |
|  | | |
| **zuivert het Registreren** | | |
|  | `setDebugLogging` | SceneGraph API om te plaatsen zuivert het registreren op ADBMobile SDK. |
|  | `getDebugLogging` | SceneGraph API om te krijgen zuivert registreren van ADBMobile SDK. |
|  | Raadpleeg voor meer informatie de sectie Foutopsporingsregistratie van de verouderde SDK. | |
|  | | |
| **Status van de Privacy / uit:schakelen** | | |
|  | `setPrivacyStatus` | SceneGraph API om privacystatus op ADBMobile SDK in te stellen. |
|  | `getPrivacyStatus` | SceneGraph API om privacystatus van ADBMobile SDK te krijgen. |
|  | Raadpleeg het gedeelte Opt-Out/Privacy Status van verouderde SDK voor meer informatie. | |
|  | | |
| **Analytics** | | |
|  | `trackState` | SceneGraph API om staat op ADBMobile SDK te volgen. |
|  | `trackAction` | SceneGraph API om actie op ADBMobile SDK te volgen. |
|  | `trackingIdentifier` | SceneGraph API om een volgende herkenningsteken van ADBMobile SDK te krijgen. |
|  | `userIdentifier` | SceneGraph-API om een gebruikers-id op te halen uit de ADBMobile-SDK. |
|  | `setUserIdentifier` | SceneGraph API om het gebruikersherkenningsteken op ADBMobile SDK te plaatsen. |
|  | `getAllIdentifiers` | SceneGraph-API haalt alle gebruikersidentiteiten op die bekend zijn bij en worden voortgezet door de Roku SDK. |
|  | Raadpleeg de sectie Analytics van de verouderde SDK voor meer informatie. | |
|  | | |
| **Experience Cloud** | | |
|  | `visitorSyncIdentifiers` | SceneGraph API om Experience Cloud-id&#39;s te synchroniseren op de ADBMobile SDK. |
|  | `visitorMarketingCloudID` | SceneGraph-API voor het ophalen van de Experience Cloud-id van de Bezoeker van de ADBMobile-SDK. |
|  | Raadpleeg voor meer informatie de sectie Experience Cloud van de verouderde SDK. | |
|  | | |
| **Audience Manager** | | |
|  | `audienceSubmitSignal` | SceneGraph API om een signaal van het publieksbeheer met eigenschap te verzenden. |
|  | `audienceVisitorProfile` | SceneGraph-API om een bezoekersprofiel van de publieksmanager op te halen van de ADBMobile-SDK. |
|  | `audienceDpid` | SceneGraph API om een publiekDpid van ADBMobile SDK te krijgen. |
|  | `audienceDpuuid` | SceneGraph API om een publiek Dpuuid van ADBMobile SDK te krijgen. |
|  | `audienceSetDpidAndDpuuid` | SceneGraph API om publiek Dpid en Dpuuid op ADBMobile SDK te plaatsen. |
|  | Raadpleeg voor meer informatie de sectie Audience Manager van de verouderde SDK. | |
|  | | |
| **MediaHeartbone** | | |
|  | `mediaTrackLoad` | SceneGraph-API om video-inhoud te laden voor MediaHeartbone-tracking. |
|  | mediaTrackStart | SceneGraph-API om een sessie voor het bijhouden van video te starten met MediaHeartbone. |
|  | `mediaTrackUnload` | SceneGraph-API om video-inhoud van MediaHeartbone-tracking te verwijderen. |
|  | `mediaTrackPlay` | SceneGraph-API om het afspelen van video-inhoud te volgen. |
|  | mediaTrackPause | SceneGraph-API om gepauzeerde video-inhoud bij te houden. |
|  | `mediaTrackComplete` | SceneGraph-API om het afspelen van video-inhoud te volgen. |
|  | `mediaTrackError` | SceneGraph API om playbackfouten te volgen. |
|  | mediaTrackEvent | SceneGraph API om playbackgebeurtenissen tijdens het volgen te volgen. Bijvoorbeeld: Advertenties, Hoofdstukken. |
|  | `mediaUpdatePlayhead` | SceneGraph API om playhead updates naar MediaHeartbone tijdens video het volgen te verzenden. |
|  | `mediaUpdateQoS` | SceneGraph API om updates QoS naar MediaHeartbone tijdens video het volgen te verzenden. |
|  | Raadpleeg het gedeelte MediaHeartbeat van de verouderde SDK voor meer informatie. | |

### SceneGraphConstants

| Naam van constante | Beschrijving |
|---|---|
| `API_RESPONSE` | Wordt gebruikt om het reactieobject op te halen uit het veld `adbmobileTask` van `adbmobileApiResponse` node |
| `DEBUG_LOGGING` | Wordt gebruikt als `apiName` for `getDebugLogging` |
| `PRIVACY_STATUS` | Wordt gebruikt als `apiName` for `getPrivacyStatus` |
| `TRACKING_IDENTIFIER` | Wordt gebruikt als `apiName` for `trackingIdentifier` |
| `USER_IDENTIFIER` | Wordt gebruikt als `apiName` for `userIdentifier` |
| `VISITOR_MARKETING_CLOUD_ID` | Wordt gebruikt als `apiName` for `visitorMarketingCloudID` |
| `AUDIENCE_VISITOR_PROFILE` | Wordt gebruikt als `apiName` for `audienceVisitorProfile` |
| `AUDIENCE_DPID` | Wordt gebruikt als `apiName` for `audienceDpid` |
| `AUDIENCE_DPUUID` | Wordt gebruikt als `apiName` for `audienceDpuuid` |

### adbmobileTask Node

<table>
<thead>
<tr>
<td> Veld </td><td> Type </td><td> Standaard </td><td> Gebruik </td>
</tr>
</thead>
<tbody>
<tr>
<td> adbmobileApiCall </td>
<td> assocarray </td>
<td> Ongeldig </td>
<td> Wijzig dit veld NIET of laat dit door de toepassing worden gebruikt. Dit gebied wordt gebruikt door ADBMobile SceneGraphConnector om API vraag via knopen te leiden SceneGraph en reacties te halen. Daarom is deze sleutel/het gebied gereserveerd voor AdobeMobileSDK voor verenigbaarheid SceneGraph. <b> Belangrijk:</b> Om het even welke wijzigingen aan dit gebied kunnen in het functioneren van AdobeMobileSDK verkeerd resulteren.</td>
</tr>
<tr>
<td> adbmobileApiResponse </td>
<td> assocarray </td>
<td> Ongeldig </td>
<td> Alleen-lezen Alle API's die op AdobeMobileSDK worden uitgevoerd, retourneren reacties in dit veld. Registreer u voor een callback om te luisteren naar updates voor dit veld om reactieobjecten te ontvangen. Hier volgt de indeling voor het reactieobject:  
<pre>
response = {
  "apiName" : &lt;SceneGraphConstants.
               API_NAME&gt;
  "returnValue : &lt;API_RESPONSE&gt;
}</pre>
Een instantie van dit reactieobject wordt verzonden voor elke API-aanroep op AdobeMobileSDK die een waarde retourneert volgens de API-naslaggids. Een API-aanroep voor bezoekerMarketingCloudID() retourneert bijvoorbeeld het volgende reactieobject:
<pre>
response = {
  "apiName" : m.
              adbmobileConstants.
              VISITOR_MARKETING_CLOUD_ID  
  "returnValue : "07050x25671x33760x72644x14"  
}
</pre>
OR, kunnen de reactiegegevens ook ongeldig zijn:
<pre>
response = {  
  "apiName" : m.
              adbmobileConstants.
              VISITOR_MARKETING_CLOUD_ID  
  "returnValue : invalid
}
</pre>
</td>
</tr>
</tbody>
</table>

### `adbmobile.brs`

#### `getADBMobileConnectorInstance`

API-handtekening: `ADBMobile().getADBMobileConnectorInstance()`\
Invoer: `adbmobileTask`
Retourneringstype: `ADBMobileConnector`

#### `sgConstants`

API-handtekening: `ADBMobile().sgConstants()`
Invoer: geen\
Retourneringstype: `SceneGraphConstants`

>[!NOTE]
>Raadpleeg de API-naslaggids voor `ADBMobileConnector` voor meer informatie.

### ADBMobile-constanten

|  Functie  | Naam van constante | Beschrijving   |
|---|---|---|
| Versioning | `version` | Constante voor het ophalen van AdobeMobileLibrary-versiegegevens |
| Privacy/opt-out | `PRIVACY_STATUS_OPT_IN` | Constante voor privacystatus gekozen in |
|   | `PRIVACY_STATUS_OPT_OUT` | Constante voor privacystatus uitgeschakeld |
| MediaHeartbone-constanten | Verwijs naar de constanten op deze pagina: <br/><br/>[ de Methoden van de Hartslag van Media.](/help/use-cases/track-av-playback/track-core/track-core-roku.md) | Deze constanten gebruiken met MediaHeartbone-API&#39;s |
| Standaardmetagegevens | Verwijs naar de constanten op deze pagina: <br/><br/>[ StandaardParameters van Meta-gegevens.](/help/use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md) | Gebruik deze constanten om standaard video-/advertentiemetagegevens toe te voegen in MediaHeartbone-API&#39;s |



Globally defined nut `MediaHeartbeat` APIs op erfenis AdobeMobileLibrary is toegankelijk *zoals is* in het milieu SceneGraph omdat zij geen componenten van het Helderscript gebruiken die in knopen SceneGraph niet beschikbaar zijn. Zie de onderstaande tabel voor meer informatie over deze methoden:

### Algemene methoden voor MediaHeartbeat

| Methode | Beschrijving |
| --- | --- |
| `adb_media_init_mediainfo` | Deze methode retourneert een geïnitialiseerd Media Information-object `Function adb_media_init_mediainfo(name As String, id As String, length As Double, streamType As String) As Object` |
| `adb_media_init_adinfo` | Deze methode retourneert het geïnitialiseerde object AD Information `Function adb_media_init_adinfo(name As String, id As String, position As Double, length As Double) As Object` |
| `adb_media_init_chapterinfo` | Deze methode retourneert het geïnitialiseerde object Chapter Information.  `Function adb_media_init_adbreakinfo(name As String, startTime as Double, position as Double) As Object` |
| `adb_media_init_adbreakinfo` | Deze methode retourneert het geïnitialiseerde object AdBreak Information.  `Function adb_media_init_chapterinfo(name As String, position As Double, length As Double, startTime As Double) As Object` |
| `adb_media_init_qosinfo` | Deze methode keert een geïnitialiseerd voorwerp van de Informatie QoS terug.  `Function adb_media_init_qosinfo(bitrate As Double, startupTime as Double, fps as Double, droppedFrames as Double) As Object` |

## Implementatie {#implementation}

1. **Download de Bibliotheek van Roku -** Download de [ recentste bibliotheek van Roku.](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.2)

1. **opstelling Uw Ontwikkelomgeving**

   1. Kopieer `adbmobile.brs` (AdobeMobileLibrary) naar de map `pkg:/source/` .

   1. Kopieer `adbmobileTask.brs` en `adbMobileTask.xml` naar de map `pkg:/components/` voor ondersteuning voor scènegrafiek.

1. **initialiseren**

   1. Importeer `adbmobile.brs` in de scène.

      ```
      <script type="text/brightscript" uri="pkg:/source/adbmobile.brs" />
      ```

   1. Maak een instantie van `adbmobileTask` node in uw scène.

      ```
      m.adbmobileTask = createObject("roSGNode", "adbmobileTask")
      ```

   1. Hiermee wordt een instantie van `adbmobile` connector voor SceneGraph opgehaald met de `adbmobileTask` -instantie.

      ```
      m.adbmobile = ADBMobile().getADBMobileConnectorInstance(m.adbmobileTask)
      ```

   1. Krijg `adbmobile` SG constanten.

      ```
      m.adbmobileConstants = m.adbmobile.sceneGraphConstants()
      ```

   1. Registreer een callback voor het ontvangen van reactievoorwerp voor alle `AdbMobile` API vraag.

      ```
      m.adbmobileTask.ObserveField(m.adbmobileConstants.API_RESPONSE,  
                                   "onAdbmobileApiResponse")
      
      ' Sample implementation of the callback
      ' Listen for all the constants for which API calls are made on the SDK
      function onAdbmobileApiResponse() as void
          responseObject = m.adbmobileTask[m.adbmobileConstants.API_RESPONSE]
      
          if responseObject <> invalid
              methodName = responseObject.apiName
              retVal = responseObject.returnValue
      
              if methodName = m.adbmobileConstants.DEBUG_LOGGING
                  if retVal
                      print "API Response: DEBUG LOGGING: " + "True"
                  else
                      print "API Response: DEBUG LOGGING: " + "False"
                  endif
              else if methodName = m.adbmobileConstants.PRIVACY_STATUS
                  print "API Response: PRIVACY STATUS: " + retVal
              else if methodName = m.adbmobileConstants.TRACKING_IDENTIFIER
                  if retVal <> invalid
                      print "API Response: TRACKING IDENTIFIER: " + retVal
                  else
                      print "API Response: TRACKING IDENTIFIER: " + "invalid"
                  endif
              else if methodName = m.adbmobileConstants.USER_IDENTIFIER
                  if retVal <> invalid
                      print "API Response: USER IDENTIFIER: " + retVal
                  else
                      print "API Response: USER IDENTIFIER: " + "invalid"
                  endif
              else if methodName = m.adbmobileConstants.VISITOR_MARKETING_CLOUD_ID
                  if retVal <> invalid
                      print "API Response: MCID: " + retVal
                  else
                      print "API Response: MCID: " + "invalid"
                  endif
              else if methodName = m.adbmobileConstants.AUDIENCE_DPID
                  if retVal <> invalid
                      print "API Response: AUDIENCE DPID: " + retVal
                  else
                      print "API Response: AUDIENCE DPID: " + "invalid"
                  endif
              else if methodName = m.adbmobileConstants.AUDIENCE_DPUUID
                  if retVal <> invalid
                      print "API Response: AUDIENCE DPUUID: " + retVal
                  else
                      print "API Response: AUDIENCE DPUUID: " + "invalid"
                  endif
              else if methodName = m.adbmobileConstants.AUDIENCE_VISITOR_PROFILE
                  if retVal <> invalid
                      print "API Response: AUDIENCE VISITOR PROFILE: Valid Object"
                  else
                      print "API Response: AUDIENCE VISITOR PROFILE: " + "invalid"
                  endif
              endif
          endif
      end function
      ```

## Voorbeeldimplementatie {#sample-implementation}

### Voorbeeld-API-aanroepen op verouderde SDK

```
'get an instance of SDK
m.adbmobile = ADBMobile()

'execute setter APIs
m.adbmobile.setDebugLogging(true)

'execute getter APIs
debugLogging = m.adbmobile.getDebugLogging()
```

### Voorbeeld-API-aanroepen op SG SDK

```
'create adbmobileTask instance
m.adbmobileTask = createObject("roSGNode", "adbmobileTask")

'get an instance of SDK using task instance
m.adbmobile =  
  ADBMobile().getADBMobileConnectorInstace(m.adbmobileTask)
m.adbmobileConstants = m.adbmobile.sceneGraphConstants()
'execute setter APIs
m.adbmobile.setDebugLogging(true)

'execute getter APIs
m.adbmobileTask.ObserverField(m.adbConstants.API_RESPONSE,  
                              "onAdbmobileApiResponse")
m.adbmobile.getDebugLogging()

'listen for return data in registered callbacks
function onAdbmobileApiResponse() as void
    responseObject = m.adbmobileTask[m.adbmobileConstants.API_RESPONSE]

        if responseObject <> invalid
            methodName = responseObject.apiName
            retVal = responseObject.returnValue

        if methodName = m.adbmobileConstants.DEBUG_LOGGING
            if retVal
                print "API Response: DEBUG LOGGING: " + "True"
            else
                print "API Response: DEBUG LOGGING: " + "False"
         endif
    endif
end function
```
