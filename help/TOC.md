---
audience: end-user
user-guide-title: Adobe Analytics voor audio en video
user-guide-description: Implement Analytics on audio or video sources. Includes the Media SDK and the Media Collection API.
product: adobe analytics
sub-product: media-analytics
translation-type: tm+mt
source-git-commit: e93a39fb76c3ccca2c05e5d1590a53394e50b29b
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 98%

---


# Adobe Analytics voor audio en video {#using}

+ [Audio en video meten in Adobe Analytics](media-overview.md)
+ [Ondersteunde apparaten en platforms](measurement-options/supported-devices.md)
+ Inleiding tot Analytics voor audio en video {#intro-to-ava}
   + [Vereisten](intro-to-ava/prereqs.md)
   + Implementatiepaden {#implementation-paths}
      + [Overzicht](intro-to-ava/implementation-paths/implementation-paths.md)
      + [Clientzijde](intro-to-ava/implementation-paths/client-side-path.md)
      + Andere implementatiepaden {#other-paths}
         + Mediamodule Milestone-tracking {#mm-milestone-tracking}
            + [Milestone: overzicht](measurement-options/mm-milestone-tracking/milestone-overview.md)
            + [Milestone migreren naar Media Analytics](measurement-options/mm-milestone-tracking/migrate-ms-to-va.md)
            + [Migreren van Milestone naar Custom Link](measurement-options/mm-milestone-tracking/migrate-ms-to-cl.md)
         + Custom Link in Analytics {#cl-in-aa}
            + [Custom Link Implementatiehandleiding](measurement-options/cl-in-aa/cl-impl-guide.md)
         + Primetime {#primetime}
            + [Primetime](intro-to-ava/implementation-paths/primetime-path.md)
         + [Audience Manager inschakelen](intro-to-ava/am-enablement.md)
+ Media Analytics SDK {#sdk-implement}
   + [Veelgestelde vragen over einde van ondersteuning voor Media Analytics SDK](sdk-implement/end-of-support-faqs.md)
   + [SDK&#39;s downloaden](sdk-implement/download-sdks.md)
   + Instellen en configureren {#setup}
      + [Overzicht](sdk-implement/setup/setup-overview.md)
      + [Android instellen](sdk-implement/setup/set-up-android.md)
      + [iOS instellen](sdk-implement/setup/set-up-ios.md)
      + JavaScript instellen {#setup-javascript}
         + [JavaScript 2.x instellen](sdk-implement/setup/setup-javascript/set-up-js-2.md)
         + [JavaScript 3.x instellen](sdk-implement/setup/setup-javascript/set-up-js-3.md)
      + [Chromecast instellen](sdk-implement/setup/set-up-chromecast.md)
      + [Roku instellen](sdk-implement/setup/set-up-roku.md)
   + Afspelen voor audio en video bijhouden {#track-av-playback}
      + [Overzicht](sdk-implement/track-av-playback/track-core-overview.md)
      + Core afspelen voor audio en video bijhouden {#track-core}
         + [Core afspelen bijhouden in Android](sdk-implement/track-av-playback/track-core/track-core-android.md)
         + [Core afspelen bijhouden in iOS](sdk-implement/track-av-playback/track-core/track-core-ios.md)
         + Core afspelen bijhouden in JavaScript {#track-core-javascript}
            + [Core afspelen bijhouden in JavaScript 2.x](sdk-implement/track-av-playback/track-core/track-core-javascript/track-core-js.md)
            + [Core afspelen bijhouden in JavaScript 3.x](sdk-implement/track-av-playback/track-core/track-core-javascript/track-core-js3.md)
         + [Core afspelen bijhouden in Chromecast](sdk-implement/track-av-playback/track-core/track-core-chromecast.md)
         + [Core afspelen bijhouden in Roku](sdk-implement/track-av-playback/track-core/track-core-roku.md)
      + Buffer bijhouden {#track-buffering}
         + [Buffer bijhouden in Android](sdk-implement/track-av-playback/track-buffering/track-buffering-android.md)
         + [Buffer bijhouden in iOS](sdk-implement/track-av-playback/track-buffering/track-buffering-ios.md)
         + Buffer bijhouden in JavaScript {#track-buffering-js}
            + [Buffer bijhouden in JavaScript 2.x](sdk-implement/track-av-playback/track-buffering/track-buffering-js/track-buffering-js.md)
            + [Buffer bijhouden in JavaScript 3.x](sdk-implement/track-av-playback/track-buffering/track-buffering-js/track-buffering-js3.md)
         + [Buffer bijhouden in Chromecast](sdk-implement/track-av-playback/track-buffering/track-buffering-chromecast.md)
         + [Buffer bijhouden in Roku](sdk-implement/track-av-playback/track-buffering/track-buffering-roku.md)
      + Zoekopdrachten bijhouden {#track-seeking}
         + [Zoekopdrachten bijhouden in Android](sdk-implement/track-av-playback/track-seeking/track-seeking-android.md)
         + [Zoekopdrachten bijhouden in iOS](sdk-implement/track-av-playback/track-seeking/track-seeking-ios.md)
         + Zoekopdrachten bijhouden in JavaScript {#track-seeking-js}
            + [Zoekopdrachten bijhouden in JavaScript 2.x ](sdk-implement/track-av-playback/track-seeking/track-seeking-js/track-seeking-js.md)
            + [Zoekopdrachten bijhouden in JavaScript 3.x ](sdk-implement/track-av-playback/track-seeking/track-seeking-js/track-seeking-js3.md)
         + [Zoekopdrachten bijhouden in Chromecast](sdk-implement/track-av-playback/track-seeking/track-seeking-chromecast.md)
         + [Zoekopdrachten bijhouden in Roku](sdk-implement/track-av-playback/track-seeking/track-seeking-roku.md)
      + Standaardmetadata implementeren {#impl-std-metadata}
         + [Standaardmetadata implementeren in Android](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)
         + [Standaardmetadata implementeren in iOS](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
         + [iOS-metadatatoetsen](sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
         + Standaardmetadata implementeren in JavaScript {#impl-std-md-js}
            + [Standaardmetadata implementeren in JavaScript 2.x](sdk-implement/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)
            + [Standaardmetadata implementeren in JavaScript 3.x](sdk-implement/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js3.md)
         + [Standaardmetadata implementeren in Chromecast](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)
         + [Standaardmetadataparameters - Chromecast](sdk-implement/track-av-playback/impl-std-metadata/chromecast-metadata.md)
         + [Standaardmetadata implementeren in Roku](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)
         + [Standaardmetadataparameters - Roku](sdk-implement/track-av-playback/impl-std-metadata/roku-metadata.md)
   + Advertenties bijhouden {#track-ads}
      + [Overzicht](sdk-implement/track-ads/track-ads-overview.md)
      + [Advertenties bijhouden in Android](sdk-implement/track-ads/track-ads-android.md)
      + [Advertenties bijhouden in iOS](sdk-implement/track-ads/track-ads-ios.md)
      + Advertenties bijhouden in JavaScript {#track-ads-js}
         + [Advertenties bijhouden in JavaScript 2.x ](sdk-implement/track-ads/track-ads-js/track-ads-js.md)
         + [Advertenties bijhouden in JavaScript 3.x ](sdk-implement/track-ads/track-ads-js/track-ads-js3.md)
      + [Advertenties bijhouden in Chromecast](sdk-implement/track-ads/track-ads-chromecast.md)
      + [Advertenties bijhouden in Roku](sdk-implement/track-ads/track-ads-roku.md)
      + Standaardmetadata voor advertenties implementeren {#impl-std-ad-metadata}
         + [Standaardmetadata voor advertenties implementeren in Android](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
         + [Standaardmetadata voor advertenties implementeren in iOS](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
         + Standaardmetadata voor advertenties implementeren in JavaScript {#impl-std-ad-md-js}
            + [Standaardmetadata implementeren in JavaScript 2.x](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js.md)
            + [Standaardmetadata implementeren in JavaScript 3.x](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
         + [Standaardmetadata voor advertenties implementeren in Roku](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   + Hoofdstukken en segmenten bijhouden {#track-chapters}
      + [Overzicht](sdk-implement/track-chapters/track-chapters-overview.md)
      + [Hoofdstukken en segmenten bijhouden in Android](sdk-implement/track-chapters/track-chapters-android.md)
      + [Hoofdstukken en segmenten bijhouden in iOS](sdk-implement/track-chapters/track-chapters-ios.md)
      + Hoofdstukken en segmenten bijhouden in JavaScript {#track-chapters-js}
         + [Hoofdstukken en segmenten bijhouden in JavaScript 2.x](sdk-implement/track-chapters/track-chapters-js/track-chapters-js.md)
         + [Hoofdstukken en segmenten bijhouden in JavaScript 3.x](sdk-implement/track-chapters/track-chapters-js/track-chapters-js3.md)
      + [Hoofdstuk en segment bijhouden in Chromecast](sdk-implement/track-chapters/track-chapters-chromecast.md)
      + [Hoofdstukken en segmenten bijhouden in Roku](sdk-implement/track-chapters/track-chapters-roku.md)
   + Kwaliteit van Experience bijhouden {#track-qos}
      + [Overzicht](sdk-implement/track-qos/track-qos-overview.md)
      + [Kwaliteit van Experience bijhouden in Android](sdk-implement/track-qos/track-qos-android.md)
      + [Kwaliteit van Experience bijhouden in iOS](sdk-implement/track-qos/track-qos-ios.md)
      + Kwaliteit van Experience bijhouden in JavaScript {#track-qos-js}
         + [Kwaliteit van Experience bijhouden in JavaScript 2.x](sdk-implement/track-qos/track-qos-js/track-qos-js.md)
         + [Kwaliteit van Experience bijhouden in JavaScript 3.x](sdk-implement/track-qos/track-qos-js/track-qos-js3.md)
      + [Kwaliteit van Experience bijhouden in Chromecast](sdk-implement/track-qos/track-qos-chromecast.md)
      + [Kwaliteit van Experience bijhouden in Roku](sdk-implement/track-qos/track-qos-roku.md)
   + Fouten bijhouden {#track-errors}
      + [Overzicht](sdk-implement/track-errors/track-errors-overview.md)
      + [Fouten bijhouden in Android](sdk-implement/track-errors/track-errors-android.md)
      + [Fouten bijhouden in iOS](sdk-implement/track-errors/track-errors-ios.md)
      + Fouten bijhouden in JavaScript {#track-errors-js}
         + [Fouten bijhouden in JavaScript 2.x ](sdk-implement/track-errors/track-errors-js/track-errors-js.md)
         + [Fouten bijhouden in JavaScript 3.x ](sdk-implement/track-errors/track-errors-js/track-errors-js3.md)
      + [Fouten bijhouden in Chromecast](sdk-implement/track-errors/track-errors-chromecast.md)
      + [Fouten bijhouden in Roku](sdk-implement/track-errors/track-errors-roku.md)
   + [Afmelden en privacy](sdk-implement/opt-out-privacy.md)
   + Scenario&#39;s bijhouden {#tracking-scenarios}
      + [VOD afspelen zonder advertenties](sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
      + [VOD afspelen met pre-roll-advertenties](sdk-implement/tracking-scenarios/vod-preroll-ads.md)
      + [VOD afspelen met overgeslagen advertenties](sdk-implement/tracking-scenarios/vod-skipped-ads.md)
      + [VOD afspelen met één hoofdstuk](sdk-implement/tracking-scenarios/vod-one-chapter.md)
      + [VOD afspelen met een overgeslagen hoofdstuk](sdk-implement/tracking-scenarios/vod-skipped-chapter.md)
      + [VOD afspelen met zoeken in de hoofdinhoud](sdk-implement/tracking-scenarios/vod-seeking.md)
      + [VOD afspelen met bufferen](sdk-implement/tracking-scenarios/vod-buffering.md)
      + [Meerdere parallelle VOD-trackers](sdk-implement/tracking-scenarios/vod-multi-trackers.md)
      + [Eén VOD-tracker voor meerdere sessies](sdk-implement/tracking-scenarios/vod-multi-track-one-session.md)
      + [Live hoofdcontent](sdk-implement/tracking-scenarios/live-main-content.md)
      + [Live hoofdcontent met sequentiële tracking](sdk-implement/tracking-scenarios/live-sequential.md)
   + Validatie {#validation}
      + [Validatieoverzicht](sdk-implement/validation/validation-overview.md)
      + [Test 1: Standaard afspelen](sdk-implement/validation/test1-standard-playback.md)
      + [Test 2: Onderbreking media](sdk-implement/validation/test2-media-interrupt.md)
      + [Details testoproep](sdk-implement/validation/test-call-details.md)
      + [Beschrijvingen van hartslagparameters](sdk-implement/validation/heartbeat-params.md)
      + Foutopsporing {#debugging}
         + [Foutopsporing in SDK](sdk-implement/validation/debugging/sdk-debugging.md)
         + [Adobe Debug configureren](sdk-implement/validation/debugging/config-adobe-debug.md)
         + [Nieuw foutopsporingsrapport maken](sdk-implement/validation/debugging/create-new-debug-report.md)
         + [Foutopsporing voor dashboards en rapporten](sdk-implement/validation/debugging/debug-dash-repts.md)
   + Analytics in OTT-apps {#analytics-with-ott}
      + [App-statussen bijhouden](sdk-implement/analytics-with-ott/track-app-states.md)
      + [App-acties bijhouden](sdk-implement/analytics-with-ott/track-app-actions.md)
      + [Gebruikers-ID&#39;s instellen](sdk-implement/analytics-with-ott/set-user-ids.md)
      + [OTT en Audience Manager](sdk-implement/analytics-with-ott/ott-am.md)
      + [OTT en Experience Cloud](sdk-implement/analytics-with-ott/ott-experience-cloud.md)
   + Cookbook {#cookbook}
      + [SDK-cookbook](sdk-implement/cookbook/sdk-cookbook-overview.md)
      + [Handlingstoepassing onderbreekt tijdens afspelen](sdk-implement/cookbook/app-interrupts.md)
      + [Hoofdcontent omzetten:afspelen tussen advertenties](sdk-implement/cookbook/fix-ad-play-ad.md)
      + [Inactieve sessies hervatten](sdk-implement/cookbook/resuming-inactive.md)
      + [Tracking in SceneGraph (Roku)](sdk-implement/cookbook/sdk-track-scenegraph.md)
   + Migratie van Media Analytics 1.x naar 2.x {#va-1x-to-2x}
      + [Migratieoverzicht](sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
      + [Codevergelijking: 1.x naar 2.x](sdk-implement/va-1x-to-2x/code-comparison-1x-2x.md)
      + [1.x naar 2.x API-conversie](sdk-implement/va-1x-to-2x/1x-2x-api-change.md)
   + Migratie van Media Analytics SDK naar Launch {#sdk-to-launch}
      + [Migratie van SDK naar Launch](sdk-implement/sdk-to-launch/sdk-to-launch-migration.md)
      + Platformhandleidingen voor migratie van SDK naar Launch {#sdk-to-launch-migration-platforms}
         + [Android](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)
         + [iOS](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)
         + [JS](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-js.md)
+ Media Collection API (RESTful) {#media-collection-api}
   + [Overzicht](media-collection-api/mc-api-overview.md)
   + API-referentie {#mc-api-ref}
      + [Aanvraag voor sessies](media-collection-api/mc-api-ref/mc-api-sessions-req.md)
      + [Aanvraag voor gebeurtenissen](media-collection-api/mc-api-ref/mc-api-events-req.md)
      + [Parameters aanvragen](media-collection-api/mc-api-ref/mc-api-req-params.md)
      + [Gebeurtenistypen en beschrijvingen](media-collection-api/mc-api-ref/mc-api-event-types.md)
      + [JSON-validatieschema&#39;s](media-collection-api/mc-api-ref/mc-api-json-validation.md)
   + De API implementeren {#mc-api-impl}
      + [Snel starten](media-collection-api/mc-api-impl/mc-api-quick-start.md)
      + [Het HTTP-aanvraagtype instellen in de Player](media-collection-api/mc-api-impl/mc-api-set-http-req.md)
      + [Een sessie-ID verkrijgen](media-collection-api/mc-api-impl/mc-api-obtain-sid.md)
      + [Een gebeurtenissenverzoek implementeren](media-collection-api/mc-api-impl/mc-api-impl-events-req.md)
      + [Gebeurtenisverzoeken valideren](media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
      + [Ping-gebeurtenissen verzenden](media-collection-api/mc-api-impl/mc-api-sed-pings.md)
      + [QoE-data verzenden](media-collection-api/mc-api-impl/mc-api-sending-qoe.md)
      + [Ondersteuning voor aangepaste metadata](media-collection-api/mc-api-impl/mc-api-custom-meta.md)
      + [Time-outvoorwaarden](media-collection-api/mc-api-impl/mc-api-timeout.md)
      + [De volgorde van gebeurtenissen bepalen](media-collection-api/mc-api-impl/mc-api-ctrl-order.md)
      + [Gebeurtenissen in wachtrij plaatsen wanneer de reactie op sessies traag is](media-collection-api/mc-api-impl/mc-api-queuing.md)
   + Tijdlijnen voor mediatracking {#mc-api-timelines}
      + [Tijdlijn 1 - Weergeven tot einde van content](media-collection-api/mc-api-timelines/mc-api-timeline-1.md)
      + [Tijdlijn 2 - Gebruiker verlaat sessie](media-collection-api/mc-api-timelines/mc-api-timeline-2.md)
      + [Tijdlijn 3 - Hoofdstukken](media-collection-api/mc-api-timelines/mc-api-timeline-3.md)
+ Cookbook {#media-analytics-cookbook}
   + [Cookbook](media-analytics-cookbook/media-analytics-cookbook.md)
   + [Attributie van mediastream](media-analytics-cookbook/media-dimensions.md)
+ Statistieken en metadata {#metrics-and-metadata}
   + [Parameters voor audio en video](metrics-and-metadata/audio-video-parameters.md)
   + [Parameters voor advertenties](metrics-and-metadata/ad-parameters.md)
   + [Hoofdstukparameters](metrics-and-metadata/chapter-parameters.md)
   + [Parameters voor Player-status](metrics-and-metadata/player-state-parameters.md)
   + [Kwaliteitsparameters](metrics-and-metadata/quality-parameters.md)
   + [Segmenten](metrics-and-metadata/segments.md)
   + [Berekende statistieken](metrics-and-metadata/calculated-metrics.md)
+ Rapportage en analyse {#media-reports}
   + [Mediarapporten inschakelen](media-reports/media-reports-enable.md)
   + Standaardrapporten van media {#media-default-reports}
      + [Overzicht van standaardrapporten](media-reports/media-default-reports/default-reports-overview.md)
      + [Overzicht van media](media-reports/media-default-reports/media-reports-overview.md)
      + [Details van media](media-reports/media-default-reports/media-reports-detail.md)
      + [Rapport Mediaoverdag](media-reports/media-default-reports/media-reports-daypart.md)
      + [Rapport Mediagelijktijdige viewers](media-reports/media-default-reports/media-concurrent-viewers.md)
   + Deelvensters voor Media-werkruimte {#media-workspace-panels}
      + [Deelvenster voor gelijktijdige mediaviewers](media-reports/media-workspace-panels/media-concurrent-viewers.md)
   + [Sjablonen voor Media-werkruimte](media-reports/media-workspace-templates.md)
   + [Gegevens van gelijktijdige viewers ophalen via API](media-reports/media-default-reports/get-concurrent-json20.md)
+ [Gedownloade content bijhouden](media-collection-api/track-downloaded-content.md)
+ [Federated Analytics](federated-analytics.md)
+ Player-status bijhouden {#player-state-tracking}
   + [Overzicht](sdk-implement/player-state-tracking/player-state-overview.md)
   + [Standaard en aangepaste statussen](sdk-implement/player-state-tracking/standard-and-custom-states.md)
   + [Implementatie en rapportage](sdk-implement/player-state-tracking/implementation-and-reporting.md)
   + [Voorbeelden van Player-statussen bijhouden](sdk-implement/player-state-tracking/player-state-examples.md)
+ Aanvullende bronnen {#additional-resources}
   + [Release-opmerkingen](additional-resources/doc-updates.md)
