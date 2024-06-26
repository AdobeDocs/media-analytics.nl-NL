---
product: adobe analytics
audience: end-user
user-guide-title: Invoegtoepassing voor streaming media-verzameling
breadcrumb-title: Handleiding voor het streamen van media
user-guide-description: Streaming media implementeren. Bevat de Media-SDK en de Media Collection-API.
sub-product: media analytics
source-git-commit: 240fa48bdc738425e04cd29c27625c7dd612ff18
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 12%

---


# Invoegtoepassing voor streaming media-verzameling {#using}

+ [Handleiding voor het streamen van media](media-overview.md)
+ Opmerkingen bij de release {#release-notes}
   + [Opmerkingen bij de release Streaming Media Collection](additional-resources/release-notes.md)
+ Aan de slag {#getting-started}
   + [Vereisten](getting-started/prereqs.md)
   + [Ondersteunde apparaten](getting-started/supported-devices.md)
   + [Implementatiedocumentatie voor streamingmedia-verzameling](getting-started/implementation-documentation.md)
   + [SDK&#39;s, bibliotheken en extensies](getting-started/download-sdks.md)
   + Einde van ondersteuning {#end-of-support}
      + [Media Analytics Mobile SDK End of Support](additional-resources/end-of-support-faqs.md)
      + Verouderd - Standalone Media SDK om migratie te starten {#sdk-to-launch}
         + [Overzicht](legacy/sdk-to-launch/sdk-to-launch-migration.md)
         + [Android - SDK van media om te starten](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)
         + [iOS - SDK van media om te starten](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)
         + [JavaScript - SDK van media om te starten](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-js.md)
+ Implementatie {#implementation}
   + [Overzicht van implementatie](implementation/overview.md)
   + Edge-implementaties (aanbevolen) {#edge-recommended}
      + [Vereisten](/help/implementation/edge/prerequisites-edge.md)
      + Media Edge SDK&#39;s / Extensie {#media-edge-sdk}
         + [Media Edge SDK&#39;s / Extensie instellen](/help/implementation/edge/implementation-edge.md)
         + [Media Edge Web SDK](/help/implementation/edge/edge-web-sdk.md)
         + [Media Edge Mobile SDK](/help/implementation/edge/edge-mobile-sdk.md)
      + [Media Edge API](/help/implementation/edge/implementation-edge-api.md)
   + Alleen Adobe Analytics-implementaties {#analytics-only}
      + [Vereisten](/help/implementation/media-sdk/setup/prerequisites-analytics.md)
      + Media-SDK&#39;s / extensie {#media-sdk}
         + [JavaScript Web SDK](implementation/media-sdk/setup/web-implementation.md)
         + [Media Analytics-extensie](implementation/media-sdk/setup/web-implementation-tags.md)
         + [Mobiele SDK&#39;s](implementation/media-sdk/setup/mobile-implementation.md)
         + OTT SDK&#39;s {#ott-setup}
            + [De Chromecast SDK installeren](implementation/media-sdk/setup/set-up-chromecast.md)
            + [De Roku SDK installeren](implementation/media-sdk/setup/set-up-roku.md)
      + Media Collection-API&#39;s - Implementatie {#streaming-media-apis}
         + [Media-verzameling](implementation/media-collection-api/mc-api-overview.md)
         + [API Snel starten](implementation/media-collection-api/mc-api-impl/mc-api-quick-start.md)
         + [Aanvraag sessie](implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)
         + [Aanvraag voor gebeurtenissen](implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)
         + [Parameters aanvragen](implementation/media-collection-api/mc-api-ref/mc-api-req-params.md)
         + [Gebeurtenistypen en beschrijvingen](implementation/media-collection-api/mc-api-ref/mc-api-event-types.md)
         + De API implementeren {#mc-api-impl}
            + [Het HTTP-aanvraagtype instellen in de Player](implementation/media-collection-api/mc-api-impl/mc-api-set-http-req.md)
            + [Zitting-id verkrijgen](implementation/media-collection-api/mc-api-impl/mc-api-obtain-sid.md)
            + [Een Events-aanvraag implementeren](implementation/media-collection-api/mc-api-impl/mc-api-impl-events-req.md)
            + [JSON-validatieschema&#39;s](implementation/media-collection-api/mc-api-ref/mc-api-json-validation.md)
            + [Gebeurtenisverzoeken valideren](implementation/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
            + [Pingsgebeurtenissen verzenden](implementation/media-collection-api/mc-api-impl/mc-api-sed-pings.md)
            + [QoE-gegevens verzenden](implementation/media-collection-api/mc-api-impl/mc-api-sending-qoe.md)
            + [Ondersteuning voor aangepaste metagegevens](implementation/media-collection-api/mc-api-impl/mc-api-custom-meta.md)
            + [Tijdslimiet](implementation/media-collection-api/mc-api-impl/mc-api-timeout.md)
            + [De volgorde van gebeurtenissen bepalen](implementation/media-collection-api/mc-api-impl/mc-api-ctrl-order.md)
            + [Gebeurtenissen in wachtrij wanneer de reactie op sessies traag is](implementation/media-collection-api/mc-api-impl/mc-api-queuing.md)
   + Variabelen {#variables}
      + [Streaming mediaparameters](implementation/variables/audio-video-parameters.md)
      + [Advertentieparameters](implementation/variables/ad-parameters.md)
      + [Hoofdstukparameters](implementation/variables/chapter-parameters.md)
      + [Parameters spelerstatus](implementation/variables/player-state-parameters.md)
      + [Kwaliteitsparameters](implementation/variables/quality-parameters.md)
      + [Berekende standaarden](implementation/variables/calculated-metrics.md)
+ Rapportage {#media-reports}
   + [Media-rapporten inschakelen](reporting/media-reports-enable.md)
   + Media-deelvensters in Workspace {#media-workspace-panels}
      + [Deelvenster Gemiddelde media - geluid](reporting/workspace/average-minute-audience.md)
      + [Deelvenster Mediagelijktijdige viewers](reporting/workspace/media-concurrent-viewers-overview.md)
      + [Media afspelen tijd besteed, deelvenster](reporting/workspace/media-playback-time-spent.md)
   + [Mediarapporten in Workspace](reporting/workspace/media-workspace-templates.md)
   + [Mediasegmenten](reporting/segments.md)
   + Standaardrapporten voor media {#media-default-reports}
      + [Overzicht van standaardrapporten](reporting/reports-and-analytics/default-reports-overview.md)
      + [Overzicht van media](reporting/reports-and-analytics/media-reports-overview.md)
      + [Media-details](reporting/reports-and-analytics/media-reports-detail.md)
      + [Mediadagrapport](reporting/reports-and-analytics/media-reports-daypart.md)
      + [Rapport voor gelijktijdige viewers voor media](reporting/reports-and-analytics/media-concurrent-viewers-reports.md)
   + Media-API {#media-api}
      + [Gelijktijdige viewergegevens ophalen](reporting/reports-and-analytics/get-concurrent-json20.md)
      + [Betaalde gegevens voor afspeeltijd van media ophalen](reporting/reports-and-analytics/get-mediaplaybacktimespent-json20.md)
+ Gevallen gebruiken {#media-use-cases}
   + [Gebruiksscenario&#39;s van SDK voor media](use-cases/cookbook/sdk-cookbook-overview.md)
   + Player-status bijhouden {#player-state-tracking}
      + [Overzicht](use-cases/player-state-tracking/player-state-overview.md)
      + [Standaard- en aangepaste frames](use-cases/player-state-tracking/standard-and-custom-states.md)
      + [Uitvoering en verslaglegging](use-cases/player-state-tracking/implementation-and-reporting.md)
      + [Meerdere statussen van spelers bijhouden](use-cases/player-state-tracking/multiple-player-states.md)
      + [Voorbeelden van statussen van Player bijhouden](use-cases/player-state-tracking/player-state-examples.md)
   + [Gedownloade inhoud bijhouden](use-cases/track-downloaded-content.md)
   + [Federated Analytics](use-cases/federated-analytics.md)
   + [Toepassing onderbreekt tijdens afspelen](use-cases/cookbook/app-interrupts.md)
   + [Attributie van mediastroom](use-cases/media-analytics-cookbook/media-dimensions.md)
   + [Niet-actieve sessies hervatten](use-cases/cookbook/resuming-inactive.md)
   + [Roku-tracking in SceneGraph](use-cases/cookbook/sdk-track-scenegraph.md)
   + [Tussenruimten tussen advertenties verwerken](use-cases/cookbook/fix-ad-play-ad.md)
   + Tijdlijnen {#timelines}
      + [Begin en einde van hoofdstuk](use-cases/timelines/chapter-start-end.md)
      + [Weergeven naar einde inhoud](use-cases/timelines/view-to-end-of-content.md)
      + [Verlaten sessie](use-cases/timelines/user-abandons-session.md)
   + Analyses gebruiken in OTT-apps {#analytics-with-ott}
      + [App-statussen bijhouden](use-cases/analytics-with-ott/track-app-states.md)
      + [Toepassingshandelingen bijhouden](use-cases/analytics-with-ott/track-app-actions.md)
      + [Gebruikersnaam instellen](use-cases/analytics-with-ott/set-user-ids.md)
      + [OTT en Audience Manager](use-cases/analytics-with-ott/ott-am.md)
      + [OTT en Experience Cloud](use-cases/analytics-with-ott/ott-experience-cloud.md)
+ Tekstspatiëring {#tracking}
   + [Overzicht](use-cases/track-av-playback/track-core-overview.md)
   + Core Streaming Media afspelen {#track-core}
      + [Core Playback bijhouden op JavaScript 3.x](use-cases/track-av-playback/track-core/track-core-javascript/track-core-js3.md)
      + [Core Playback bijhouden op Chromecast](use-cases/track-av-playback/track-core/track-core-chromecast.md)
      + [Core Playback bijhouden op Roku](use-cases/track-av-playback/track-core/track-core-roku.md)
   + Buffer bijhouden {#track-buffering}
      + [Trackbuffering op JavaScript 3.x](use-cases/track-av-playback/track-buffering/track-buffering-js/track-buffering-js3.md)
      + [De Buffer van het spoor op Chromecast](use-cases/track-av-playback/track-buffering/track-buffering-chromecast.md)
      + [Buffering bijhouden op Roku](use-cases/track-av-playback/track-buffering/track-buffering-roku.md)
   + Zoekopdrachten bijhouden {#track-seeking}
      + [Trackzoekopdracht voor JavaScript 3.x](use-cases/track-av-playback/track-seeking/track-seeking-js/track-seeking-js3.md)
      + [Trackzoekopdracht op chroecast](use-cases/track-av-playback/track-seeking/track-seeking-chromecast.md)
      + [Track Seeking op Roku](use-cases/track-av-playback/track-seeking/track-seeking-roku.md)
   + Standaardmetadata implementeren {#impl-std-metadata}
      + [Standaardmetagegevens implementeren op JavaScript 3.x](use-cases/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js3.md)
      + [Standaardmetagegevens toepassen op Chromecast](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)
      + [Standaardmetagegevensparameters - Chromecast](use-cases/track-av-playback/impl-std-metadata/chromecast-metadata.md)
      + [Standaardmetagegevens implementeren op Roku](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)
      + [Standaardmetagegevensparameters - Roku](use-cases/track-av-playback/impl-std-metadata/roku-metadata.md)
   + Advertenties bijhouden {#track-ads}
      + [Overzicht](use-cases/track-ads/track-ads-overview.md)
      + [Advertenties bijhouden op JavaScript 3.x](use-cases/track-ads/track-ads-js/track-ads-js3.md)
      + [Advertenties bijhouden bij chroecast](use-cases/track-ads/track-ads-chromecast.md)
      + [Advertenties bijhouden op Roku](use-cases/track-ads/track-ads-roku.md)
      + Standaardmetadata voor advertenties implementeren {#impl-std-ad-metadata}
         + [Standaard en metagegevens implementeren op JavaScript 3.x](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
         + [Standaard en metagegevens implementeren op Roku](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   + Hoofdstukken en segmenten bijhouden {#track-chapters}
      + [Overzicht](use-cases/track-chapters/track-chapters-overview.md)
      + [Hoofdstukken en segmenten bijhouden op JavaScript 3.x](use-cases/track-chapters/track-chapters-js/track-chapters-js3.md)
      + [Hoofdstuk en segment bijhouden op Chromecast](use-cases/track-chapters/track-chapters-chromecast.md)
      + [Hoofdstukken en segmenten bijhouden op Roku](use-cases/track-chapters/track-chapters-roku.md)
   + Kwaliteit van Experience bijhouden {#track-qos}
      + [Overzicht](use-cases/track-qos/track-qos-overview.md)
      + [Trackkwaliteit van ervaring op JavaScript 3.x](use-cases/track-qos/track-qos-js/track-qos-js3.md)
      + [Trackkwaliteit van ervaring op chroomecast](use-cases/track-qos/track-qos-chromecast.md)
      + [Trackkwaliteit van ervaring op Roku](use-cases/track-qos/track-qos-roku.md)
   + Fouten bijhouden {#track-errors}
      + [Overzicht](use-cases/track-errors/track-errors-overview.md)
      + [Fouten bijhouden in JavaScript 3.x](use-cases/track-errors/track-errors-js/track-errors-js3.md)
      + [Fouten bijhouden op chroecast](use-cases/track-errors/track-errors-chromecast.md)
      + [Fouten bijhouden op Roku](use-cases/track-errors/track-errors-roku.md)
+ Privacy en beveiliging {#streaming-media-privacy}
   + [Instellingen voor Uitschakelen en Privacy](privacy/opt-out-privacy.md)
   + [Beveiliging](privacy/security.md)
+ Oudere implementaties {#legacy-implementations}
   + [Verouderd - Overzicht](legacy/setup/legacy-setup-overview.md)
   + [Verouderd — SDK&#39;s downloaden](legacy/legacy-download-sdks.md)
   + Verouderd - SDK&#39;s voor media {#legacy-media-sdks}
      + [Verouderd - Overzicht van Media SDK](legacy/media-sdk/setup/setup-overview.md)
      + [Android instellen](legacy/media-sdk/setup/set-up-android.md)
      + [IOS instellen](legacy/media-sdk/setup/set-up-ios.md)
      + JavaScript instellen {#setup-javascript}
         + [JavaScript 2.x instellen](legacy/media-sdk/setup/setup-javascript/set-up-js-2.md)
   + [Informatie over hartslagmeting](legacy/heartbeat-measurement.md)
   + [Adobe Primetime](legacy/intro-to-ava/implementation-paths/primetime-path.md)
   + [Adobe Audience Management Enablement](legacy/intro-to-ava/am-enablement.md)
   + [Implementatie van aangepaste koppeling](legacy/measurement-options/cl-in-aa/cl-impl-guide.md)
   + Legacy Mijlpaal-opvolging {#legacy-milestone-tracking}
      + [Legacy Mijlpaal-opvolging](legacy/measurement-options/mm-milestone-tracking/milestone-overview.md)
      + [Migrate migreren naar VA](legacy/measurement-options/mm-milestone-tracking/migrate-ms-to-va.md)
      + [Migrate migreren naar CL](legacy/measurement-options/mm-milestone-tracking/migrate-ms-to-cl.md)
   + Validatie {#validation}
      + [Validatieoverzicht](legacy/validation/validation-overview.md)
      + [Testen 1: Standaard afspelen](legacy/validation/test1-standard-playback.md)
      + [Test 2: Onderbreking van media](legacy/validation/test2-media-interrupt.md)
      + [Gegevens van testoproep](legacy/validation/test-call-details.md)
      + [Beschrijvingen van hartslagparameters](legacy/validation/heartbeat-params.md)
      + Foutopsporing {#debugging}
         + [Foutopsporing in SDK](legacy/validation/debugging/sdk-debugging.md)
   + [Oudere migratie: VHL 1.x naar VHL 2.x](legacy/va-1x-to-2x/mig-1x-2x-overview.md)
   + [Codevergelijking v1.x naar v2.x](legacy/va-1x-to-2x/code-comparison-1x-2x.md)
   + [API&#39;s 1x tot 2x bijhouden](legacy/va-1x-to-2x/1x-2x-api-change.md)
   + [Verouderd - Intro op AVA](legacy/intro-to-ava/implementation-paths/implementation-paths.md)
   + [Pad aan clientzijde](legacy/intro-to-ava/implementation-paths/client-side-path.md)
   + Oudere reeksspatiëring {#track-av-playback}
      + [Core Playback bijhouden op Android](use-cases/track-av-playback/track-core/track-core-android.md)
      + [Core Playback bijhouden op iOS](use-cases/track-av-playback/track-core/track-core-ios.md)
      + Core afspelen bijhouden in JavaScript {#track-core-javascript}
         + [Core Playback bijhouden op JavaScript 2.x](use-cases/track-av-playback/track-core/track-core-javascript/track-core-js.md)
         + [Buffering bijhouden op Android](use-cases/track-av-playback/track-buffering/track-buffering-android.md)
         + [Buffering bijhouden op iOS](use-cases/track-av-playback/track-buffering/track-buffering-ios.md)
         + Buffer bijhouden in JavaScript {#track-buffering-js}
            + [Trackbuffering op JavaScript 2.x](use-cases/track-av-playback/track-buffering/track-buffering-js/track-buffering-js.md)
         + [Zoeken volgen op Android](use-cases/track-av-playback/track-seeking/track-seeking-android.md)
         + [Zoeken volgen op iOS](use-cases/track-av-playback/track-seeking/track-seeking-ios.md)
         + Zoekopdrachten bijhouden in JavaScript {#track-seeking-js}
            + [Trackzoekopdrachten op JavaScript 2.x](use-cases/track-av-playback/track-seeking/track-seeking-js/track-seeking-js.md)
         + [Standaardmetagegevens implementeren op Android](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)
         + [Standaardmetagegevens implementeren op iOS](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
         + [iOS-metagegevenstoetsen](use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
         + Standaardmetadata implementeren in JavaScript {#impl-std-md-js}
            + [Standaardmetagegevens implementeren op JavaScript 2.x](use-cases/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)
      + Advertenties bijhouden {#track-ads}
         + [Advertenties volgen op Android](use-cases/track-ads/track-ads-android.md)
         + [Advertenties volgen op iOS](use-cases/track-ads/track-ads-ios.md)
         + Advertenties bijhouden in JavaScript {#track-ads-js}
            + [Advertenties bijhouden op JavaScript 2.x](use-cases/track-ads/track-ads-js/track-ads-js.md)
            + [Standaard en metagegevens implementeren op Android](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
            + [Standaard en metagegevens implementeren op iOS](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
            + Standaardmetadata voor advertenties implementeren in JavaScript {#impl-std-ad-md-js}
               + [Standaard en metagegevens implementeren op JavaScript 2.x](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js.md)
      + Hoofdstukken en segmenten bijhouden {#track-chapters}
         + [Hoofdstukken en segmenten bijhouden op Android](use-cases/track-chapters/track-chapters-android.md)
         + [Hoofdstukken en segmenten bijhouden op iOS](use-cases/track-chapters/track-chapters-ios.md)
         + Hoofdstukken en segmenten bijhouden in JavaScript {#track-chapters-js}
            + [Hoofdstukken en segmenten bijhouden op JavaScript 2.x](use-cases/track-chapters/track-chapters-js/track-chapters-js.md)
         + [Trackkwaliteit van ervaring op Android](use-cases/track-qos/track-qos-android.md)
         + [Trackkwaliteit van ervaring op iOS](use-cases/track-qos/track-qos-ios.md)
         + Kwaliteit van Experience bijhouden in JavaScript {#track-qos-js}
            + [Trackkwaliteit van ervaring op JavaScript 2.x](use-cases/track-qos/track-qos-js/track-qos-js.md)
      + Fouten bijhouden {#track-errors}
         + [Fouten bijhouden op Android](use-cases/track-errors/track-errors-android.md)
         + [Fouten bijhouden op iOS](use-cases/track-errors/track-errors-ios.md)
         + Fouten bijhouden in JavaScript {#track-errors-js}
            + [Fouten bijhouden in JavaScript 2.x](use-cases/track-errors/track-errors-js/track-errors-js.md)
      + Scenario&#39;s bijhouden {#tracking-scenarios}
         + [VOD afspelen zonder advertenties](use-cases/tracking-scenarios/vod-no-intrs-details.md)
         + [VOD afspelen met pre-roll-advertenties](use-cases/tracking-scenarios/vod-preroll-ads.md)
         + [VOD afspelen met overgeslagen advertenties](use-cases/tracking-scenarios/vod-skipped-ads.md)
         + [VOD afspelen met één hoofdstuk](use-cases/tracking-scenarios/vod-one-chapter.md)
         + [VOD afspelen met een overgeslagen hoofdstuk](use-cases/tracking-scenarios/vod-skipped-chapter.md)
         + [VOD afspelen met zoeken in de hoofdinhoud](use-cases/tracking-scenarios/vod-seeking.md)
         + [VOD afspelen met bufferen](use-cases/tracking-scenarios/vod-buffering.md)
         + [Meerdere VOD-trackers parallel](use-cases/tracking-scenarios/vod-multi-trackers.md)
         + [VOD één tracker voor meerdere sessies](use-cases/tracking-scenarios/vod-multi-track-one-session.md)
         + [Actieve hoofdinhoud](use-cases/tracking-scenarios/live-main-content.md)
         + [Actieve hoofdinhoud met opeenvolgende spatiëring](use-cases/tracking-scenarios/live-sequential.md)
