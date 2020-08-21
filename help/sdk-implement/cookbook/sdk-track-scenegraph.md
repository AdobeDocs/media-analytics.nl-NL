---
title: Tracking in SceneGraph (Roku)
description: Het volgen media met het Roku SceneGraph de programmeringskader van XML.
uuid: fa85e546-c79b-4df4-8c03-d6593fa296d5
translation-type: tm+mt
source-git-commit: 305f97d6d1350a3bb8b0ad9c4c58e0a5fefca045
workflow-type: tm+mt
source-wordcount: '1171'
ht-degree: 1%

---


# Tracking in SceneGraph (Roku){#tracking-in-scenegraph-roku}

## Inleiding {#introduction}

Roku heeft een nieuw programmeringskader voor de ontwikkeling van toepassingen geïntroduceerd: het SceneGraph de programmeringskader van XML. Dit nieuwe kader omvat twee nieuwe zeer belangrijke concepten:

* SceneGraph die van de toepassingsschermen teruggeven
* De configuratie van XML van de schermen SceneGraph

Adobe Mobile SDK voor Roku wordt geschreven in BrightScript. SDK gebruikt vele componenten die niet beschikbaar voor app zijn die op SceneGraph (bijvoorbeeld, draden) lopen. Daarom kan een Roku app ontwikkelaar die van plan is om het kader te gebruiken SceneGraph geen Adobe Mobile SDK APIs (de laatstgenoemde zijn gelijkaardig aan die beschikbaar in erfenisBrightScript apps) roepen.

## Architectuur {#architecture}

Om steun SceneGraph aan AdobeMobile SDK toe te voegen, heeft Adobe nieuwe API toegevoegd die tot een schakelaarbrug tussen AdobeMobile SDK en leidt `adbmobileTask`. Het laatstgenoemde is een knoop SceneGraph die voor de API van SDK uitvoering wordt gebruikt. (Gebruik van `adbmobileTask` wordt in de rest van dit document uitvoerig toegelicht.)

De verbindingsbrug is ontworpen om als volgt te presteren:

* De brug keert een SceneGraph-Compatibele instantie van AdobeMobile SDK terug. SceneGraph-Compatibele SDK heeft alle APIs die de erfenis SDK blootstelt.
* U gebruikt AdobeMobile SDK APIs in SceneGraph op een zeer gelijkaardige manier aan hoe u de erfenis APIs gebruikte.
* De brug stelt ook een mechanisme bloot om callbacks voor APIs te letten die sommige gegevens terugkeren.

![](assets/SceneGraph_arch.png)

## Onderdelen {#components}

**SceneGraph-toepassing:**

* Consumenten `AdobeMobileLibrary` APIs via de SceneGraph schakelaarbrug APIs.
* Registers voor terugbellen op reacties `adbmobileTask` voor de variabelen voor verwachte outputgegevens.

**AdobeMobileLibrary:**

* Stelt een reeks openbare APIs (Erfenis), met inbegrip van de schakelaarbrug API bloot.
* Keert een SceneGraph schakelaarinstantie terug die al erfenis openbare APIs verpakt.
* Communiceert met een `adbmobileTask` De knoop SceneGraph voor uitvoering van APIs.

**adbmobileTask Node:**

* Een SceneGraph taakknoop die uitvoert `AdobeMobileLibrary` APIs op een achtergronddraad.
* Dient als afgevaardigde om gegevens terug naar toepassingsscènes terug te keren.

## Public SceneGraph APIs {#public-scenegraph-apis}

### ADBMobileConnector

| Categorie | Naam methode | Beschrijving |
|---|---|---|
| **Constanten** |  |  |
|  | `sceneGraphConstants` | Keert een voorwerp terug dat bevat `SceneGraphConstants`. Raadpleeg de tabel hierboven voor meer informatie. |
|  |  |  |
| **Foutopsporing** |  |  |
|  | `setDebugLogging` | SceneGraph API om te plaatsen zuivert het registreren op ADBMobile SDK. |
|  | `getDebugLogging` | SceneGraph API om te krijgen zuiveren registreren van ADBMobile SDK. |
|  | Voor meer informatie verwijs naar de Debug het Registreren sectie van de erfenis SDK. |  |
|  |  |  |
| **Privacystatus / opt-out** |  |  |
|  | `setPrivacyStatus` | SceneGraph API om privacystatus op ADBMobile SDK te plaatsen. |
|  | `getPrivacyStatus` | SceneGraph API om privacystatus van ADBMobile SDK te krijgen. |
|  | Voor meer informatie, verwijs naar de Opt-uit/de sectie van de Status van de Privacy van de erfenis SDK. |  |
|  |  |  |
| **Analytics**   |  |  |
|  | `trackState` | SceneGraph API aan spoorstaat op ADBMobile SDK. |
|  | `trackAction` | SceneGraph API aan spooractie op ADBMobile SDK. |
|  | `trackingIdentifier` | SceneGraph API om een volgend herkenningsteken van ADBMobile SDK te krijgen. |
|  | `userIdentifier` | SceneGraph API om een gebruikersidentificatie van ADBMobile SDK te krijgen. |
|  | `setUserIdentifier` | SceneGraph API om het gebruikersherkenningsteken op ADBMobile SDK te plaatsen. |
|  | `getAllIdentifiers` | SceneGraph API wint alle die gebruikersidentiteiten terug door Roku SDK worden gekend en worden voortgeduurd. |
|  | Voor meer informatie verwijs naar de sectie van de Analyse van de erfenis SDK. |  |
|  |  |  |
| **Ervaar Cloud** |  |  |
|  | `visitorSyncIdentifiers` | SceneGraph API aan de herkenningstekens van de Wolk van de synchronisatieervaring op ADBMobile SDK. |
|  | `visitorMarketingCloudID` | SceneGraph API om identiteitskaart van de Wolk van de Ervaring van de Bezoeker van ADBMobile SDK te krijgen. |
|  | Voor meer informatie verwijs naar de sectie van de Wolk van de Ervaring van de erfenis SDK. |  |
|  |  |  |
| **Audience Manager** |  |  |
|  | `audienceSubmitSignal` | SceneGraph API om een signaal van het publieksbeheer met eigenschap te verzenden. |
|  | `audienceVisitorProfile` | SceneGraph API om een de bezoekersprofiel van de publieksmanager van ADBMobile SDK te krijgen. |
|  | `audienceDpid` | SceneGraph API om een publiek Dpid van ADBMobile SDK te krijgen. |
|  | `audienceDpuuid` | SceneGraph API om een publiek Dpuuid van ADBMobile SDK te krijgen. |
|  | `audienceSetDpidAndDpuuid` | SceneGraph API om publiek Dpid en Dpuuid op ADBMobile SDK te plaatsen. |
|  | Voor meer informatie verwijs naar de sectie van de Manager van het Publiek van de erfenis SDK. |  |
|  |  |  |
| **MediaHeartbeat** |  |  |
|  | `mediaTrackLoad` | SceneGraph API om videoinhoud voor het volgen MediaHeartbeat te laden. |
|  | mediaTrackStart | SceneGraph API om video het volgen zitting te beginnen gebruikend MediaHeartbeat. |
|  | `mediaTrackUnload` | SceneGraph API om videoinhoud van MediaHeartbeat het volgen los te laden. |
|  | `mediaTrackPlay` | SceneGraph API om playback van videoinhoud te volgen. |
|  | mediaTrackPauze | SceneGraph API om gepauzeerde videoinhoud te volgen. |
|  | `mediaTrackComplete` | SceneGraph API om playback volledig voor videoinhoud te volgen. |
|  | `mediaTrackError` | SceneGraph API om playbackfouten te volgen. |
|  | mediaTrackEvent | SceneGraph API om playbackgebeurtenissen tijdens het volgen te volgen. Bijvoorbeeld: Advertentie, hoofdstukken. |
|  | `mediaUpdatePlayhead` | SceneGraph API om playhead updates naar MediaHeartbeat tijdens video het volgen te verzenden. |
|  | `mediaUpdateQoS` | SceneGraph API om updates QoS naar MediaHeartbeat tijdens video het volgen te verzenden. |
|  | Voor meer informatie verwijs naar de sectie MediaHeartbeat van de erfenis SDK. |  |

### SceneGraphConstants

| Constante naam | Beschrijving |
|---|---|
| `API_RESPONSE` | Gebruikt om het reactievoorwerp van terug te winnen `adbmobileTask` knooppunten `adbmobileApiResponse` gebied |
| `DEBUG_LOGGING` | Gebruikt als `apiName` voor `getDebugLogging` |
| `PRIVACY_STATUS` | Gebruikt als `apiName` voor `getPrivacyStatus` |
| `TRACKING_IDENTIFIER` | Gebruikt als `apiName` voor `trackingIdentifier` |
| `USER_IDENTIFIER` | Gebruikt als `apiName` voor `userIdentifier` |
| `VISITOR_MARKETING_CLOUD_ID` | Gebruikt als `apiName` voor `visitorMarketingCloudID` |
| `AUDIENCE_VISITOR_PROFILE` | Gebruikt als `apiName` voor `audienceVisitorProfile` |
| `AUDIENCE_DPID` | Gebruikt als `apiName` voor `audienceDpid` |
| `AUDIENCE_DPUUID` | Gebruikt als `apiName` voor `audienceDpuuid` |

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
<td> Wijzig dit veld NIET of laat het door de toepassing worden gebruikt. Dit gebied wordt gebruikt door ADBMobile SceneGraphConnector aan route API vraag via knopen SceneGraph en om reacties te halen. Daarom is deze sleutel/het gebied gereserveerd voor AdobeMobileSDK voor verenigbaarheid SceneGraph. <b>Belangrijk:</b> Om het even welke wijzigingen aan dit gebied kunnen in verkeerd werkend AdobeMobileSDK resulteren.</td>
</tr>
<tr>
<td> adbmobileApiResponse </td>
<td> assocarray </td>
<td> Ongeldig </td>
<td> Alleen-lezen Alle API's die worden uitgevoerd op AdobeMobileSDK zullen reacties op dit veld teruggeven. Register voor een callback om updates aan dit gebied te luisteren om reactievoorwerpen te ontvangen. Na is het formaat voor het reactievoorwerp:  
<pre>
respons = { "apiName" : &lt;scenegraphconstants.&gt;
               API_NAME&gt; "returnValue: &lt;api_response&gt; 
}</pre>
Een geval van dit reactievoorwerp zal voor om het even welke API vraag op AdobeMobileSDK worden verzonden die om een waarde volgens de API verwijzingsgids zou moeten terugkeren. Bijvoorbeeld, zal een API vraag naar bezoekorMarketingCloudID () het volgende reactievoorwerp terugkeren: 
<pre>
respons = { "apiName" : m. adbmobileConstants.
              VISITOR_MARKETING_CLOUD_ID "returnValue: "07050x25671x33760x72644x14"} 
</pre>
OF, kunnen de antwoordgegevens ook ongeldig zijn: 
<pre>
respons = { "apiName" : m. adbmobileConstants.
              VISITOR_MARKETING_CLOUD_ID "returnValue: ongeldig} 
</pre>
</td>
</tr>
</tbody>
</table>

### `adbmobile.brs`

#### `getADBMobileConnectorInstance`

API-handtekening: `ADBMobile().getADBMobileConnectorInstance()`\
Invoer: `adbmobileTask`
Retourtype: `ADBMobileConnector`

#### `sgConstants`

API-handtekening: `ADBMobile().sgConstants()`
Invoer: Geen\
Retourtype: `SceneGraphConstants`

>[!NOTE]
>Verwijs naar `ADBMobileConnector` API-referentie voor details.

### ADBMobile Constanten

|  Functie  | Constante naam | Beschrijving   |
|---|---|---|
| Versioning | `version` | Constante voor het herstellen van de versie info van AdobeMobileLibrary |
| Privacy/opt-out | `PRIVACY_STATUS_OPT_IN` | Constante voor privacystatus gekozen in |
|  | `PRIVACY_STATUS_OPT_OUT` | Constante voor privacystatus uitgekozen |
| MediaHeartbeat Constanten | Verwijs naar de constanten op deze pagina: <br/><br/>[Mediahartslagmethoden.](/help/sdk-implement/track-av-playback/track-core/track-core-roku.md) | Gebruik deze constanten met MediaHeartbeat APIs |
| Standaardmetagegevens | Verwijs naar de constanten op deze pagina: <br/><br/>[Standaard metagegevensparameters.](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md) | Gebruik deze constanten om StandaardVideo/Ad meta-gegevens in MediaHeartbeat APIs vast te maken |

Globaal bepaald nut `MediaHeartbeat` APIs op de erfenis AdobeMobileLibrary is toegankelijk *zoals* in het milieu SceneGraph omdat zij geen componenten gebruiken van het Helderscript die in knopen SceneGraph niet beschikbaar zijn. Voor meer informatie over deze methodes, verwijs naar de hieronder lijst:

### Globale Methodes voor MediaHeartbeat

| Methode | Beschrijving |
| --- | --- |
| `adb_media_init_mediainfo` | Deze methode keert een geïnitialiseerd voorwerp van de Informatie van Media terug `Function adb_media_init_mediainfo(name As String, id As String, length As Double, streamType As String) As Object` |
| `adb_media_init_adinfo` | Deze methode keert geïnitialiseerd Add voorwerp van de Informatie terug `Function adb_media_init_adinfo(name As String, id As String, position As Double, length As Double) As Object` |
| `adb_media_init_chapterinfo` | Deze methode keert het geïnitialiseerde voorwerp van de Informatie van het Hoofdstuk terug.  `Function adb_media_init_adbreakinfo(name As String, startTime as Double, position as Double) As Object` |
| `adb_media_init_adbreakinfo` | Deze methode keert geïnitialiseerd voorwerp van de Informatie AdBreak terug.  `Function adb_media_init_chapterinfo(name As String, position As Double, length As Double, startTime As Double) As Object` |
| `adb_media_init_qosinfo` | Deze methode keert een geïnitialiseerd voorwerp van de Informatie QoS terug.  `Function adb_media_init_qosinfo(bitrate As Double, startupTime as Double, fps as Double, droppedFrames as Double) As Object` |

## Implementatie {#implementation}

1. **Download de Roku Library -** Download de [de nieuwste Roku-bibliotheek.](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.2)

1. **Stel uw ontwikkelomgeving in**

   1. Kopie `adbmobile.brs` (AdobeMobileLibrary) in uw `pkg:/source/` directory.

   1. Voor de steun van de Grafiek van de Scène, exemplaar `adbmobileTask.brs` en `adbMobileTask.xml` in uw `pkg:/components/` directory.

1. **Initialiseren**

   1. Invoer `adbmobile.brs` in uw Scène.

      ```
      <script type="text/brightscript" uri="pkg:/source/adbmobile.brs" />
      ```

   1. Creeer een geval van `adbmobileTask` knoop in uw Scène.

      ```
      m.adbmobileTask = createObject("roSGNode", "adbmobileTask")
      ```

   1. Krijg een geval van `adbmobile` schakelaar voor SceneGraph die de `adbmobileTask` instantie.

      ```
      m.adbmobile = ADBMobile().getADBMobileConnectorInstance(m.adbmobileTask)
      ```

   1. Krijg `adbmobile` SG constanten.

      ```
      m.adbmobileConstants = m.adbmobile.sceneGraphConstants()
      ```

   1. Registreer een callback voor het ontvangen van reactievoorwerp voor allen `AdbMobile` API-oproepen.

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

### De steekproef API roept op de Erfenis SDK

```
'get an instance of SDK 
m.adbmobile = ADBMobile() 
   
'execute setter APIs 
m.adbmobile.setDebugLogging(true) 
   
'execute getter APIs 
debugLogging = m.adbmobile.getDebugLogging()
```

### De steekproef API roept SG SDK

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

