---
audience: end-user
user-guide-title: Adobe Analytics for Audio and Video
product: adobe analytics
sub-product: media analytics
translation-type: tm+mt
source-git-commit: d9f6c99b26153ef81d4623c30361fc5b34385bf6

---


# Adobe Analytics voor audio en video {#using}

+ [Audio en video meten in Adobe Analytics](media-overview.md)
+ Meetopties {#measurement-options}
   + Mijlpalen bijhouden van mediamodule {#mm-milestone-tracking}
      + [Overzicht van mijlpaal](measurement-options/mm-milestone-tracking/milestone-overview.md)
      + [Migrate Migrate to Media Analytics](measurement-options/mm-milestone-tracking/migrate-ms-to-va.md)
      + [Migreren van mijlpaal naar aangepaste koppeling](measurement-options/mm-milestone-tracking/migrate-ms-to-cl.md)
   + Aangepaste koppeling in analyse {#cl-in-aa}
      + [Custom Link Implementation Guide](measurement-options/cl-in-aa/cl-impl-guide.md)
+ Inleiding tot audio- en videoanalysemogelijkheden {#intro-to-ava}
   + [Vereisten](intro-to-ava/prereqs.md)
   + Implementatiepaden {#implementation-paths}
      + [Overzicht](intro-to-ava/implementation-paths/implementation-paths.md)
      + [Client-kant](intro-to-ava/implementation-paths/client-side-path.md)
      + [Adobe Experience Platform Launch](intro-to-ava/implementation-paths/launch-path.md)
      + [Primetime](intro-to-ava/implementation-paths/primetime-path.md)
   + [Auditiebeheer inschakelen](intro-to-ava/am-enablement.md)
+ Media Analytics SDK {#sdk-implement}
   + [SDK&#39;s downloaden](sdk-implement/download-sdks.md)
   + Instellen en configureren {#setup}
      + [Overzicht](sdk-implement/setup/setup-overview.md)
      + [Android instellen](sdk-implement/setup/set-up-android.md)
      + [iOS instellen](sdk-implement/setup/set-up-ios.md)
      + [JavaScript instellen](sdk-implement/setup/set-up-js.md)
      + [Chromecast instellen](sdk-implement/setup/set-up-chromecast.md)
      + [Roku instellen](sdk-implement/setup/set-up-roku.md)
   + Audio en video afspelen {#track-av-playback}
      + [Overzicht](sdk-implement/track-av-playback/track-core-overview.md)
      + Core Audio en video afspelen {#track-core}
         + [Core Playback bijhouden op Android](sdk-implement/track-av-playback/track-core/track-core-android.md)
         + [Core Playback bijhouden op iOS](sdk-implement/track-av-playback/track-core/track-core-ios.md)
         + [Core Playback bijhouden op JavaScript](sdk-implement/track-av-playback/track-core/track-core-js.md)
         + [Core Playback bijhouden op chroecast](sdk-implement/track-av-playback/track-core/track-core-chromecast.md)
         + [Core Playback bijhouden op Roku](sdk-implement/track-av-playback/track-core/track-core-roku.md)
      + Trackbuffering {#track-buffering}
         + [Trackbuffering op Android](sdk-implement/track-av-playback/track-buffering/track-buffering-android.md)
         + [Buffering bijhouden op iOS](sdk-implement/track-av-playback/track-buffering/track-buffering-ios.md)
         + [Buffering bijhouden in JavaScript](sdk-implement/track-av-playback/track-buffering/track-buffering-js.md)
         + [De Buffer van het spoor op Chromecast](sdk-implement/track-av-playback/track-buffering/track-buffering-chromecast.md)
         + [Buffering bijhouden op Roku](sdk-implement/track-av-playback/track-buffering/track-buffering-roku.md)
      + Trackzoekopdracht {#track-seeking}
         + [Trackzoekopdracht op Android](sdk-implement/track-av-playback/track-seeking/track-seeking-android.md)
         + [Zoeken bijhouden op iOS](sdk-implement/track-av-playback/track-seeking/track-seeking-ios.md)
         + [Zoeken bijhouden in JavaScript](sdk-implement/track-av-playback/track-seeking/track-seeking-js.md)
         + [Trackzoekopdracht op chroecast](sdk-implement/track-av-playback/track-seeking/track-seeking-chromecast.md)
         + [Track Seeking op Roku](sdk-implement/track-av-playback/track-seeking/track-seeking-roku.md)
      + Standaardmetagegevens implementeren {#impl-std-metadata}
         + [Standaardmetagegevens implementeren op Android](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)
         + [Standaardmetagegevens implementeren op iOS](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
         + [iOS-metagegevenstoetsen](sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
         + [Standaardmetagegevens implementeren in JavaScript](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-js.md)
         + [Standaardmetagegevens toepassen op Chromecast](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)
         + [Standaardmetagegevensparameters - Chromecast](sdk-implement/track-av-playback/impl-std-metadata/chromecast-metadata.md)
         + [Standaardmetagegevens implementeren op Roku](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)
         + [Standaardmetagegevensparameters - Roku](sdk-implement/track-av-playback/impl-std-metadata/roku-metadata.md)
   + Advertenties bijhouden {#track-ads}
      + [Overzicht](sdk-implement/track-ads/track-ads-overview.md)
      + [Advertenties bijhouden op Android](sdk-implement/track-ads/track-ads-android.md)
      + [Advertenties bijhouden op iOS](sdk-implement/track-ads/track-ads-ios.md)
      + [Advertenties bijhouden in JavaScript](sdk-implement/track-ads/track-ads-js.md)
      + [Advertenties bijhouden bij chroecast](sdk-implement/track-ads/track-ads-chromecast.md)
      + [Advertenties bijhouden op Roku](sdk-implement/track-ads/track-ads-roku.md)
      + Standaardinstellingen en metagegevens implementeren {#impl-std-ad-metadata}
         + [Standaard- en metagegevens implementeren op Android](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
         + [Standaard en metagegevens implementeren op iOS](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
         + [Standaard en metagegevens implementeren in JavaScript](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-js.md)
         + [Standaard en metagegevens implementeren op Roku](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   + Hoofdstukken en segmenten bijhouden {#track-chapters}
      + [Overzicht](sdk-implement/track-chapters/track-chapters-overview.md)
      + [Hoofdstukken en segmenten bijhouden op Android](sdk-implement/track-chapters/track-chapters-android.md)
      + [Hoofdstukken en segmenten bijhouden op iOS](sdk-implement/track-chapters/track-chapters-ios.md)
      + [Hoofdstukken en segmenten bijhouden in JavaScript](sdk-implement/track-chapters/track-chapters-js.md)
      + [Hoofdstuk en segment bijhouden op Chromecast](sdk-implement/track-chapters/track-chapters-chromecast.md)
      + [Hoofdstukken en segmenten bijhouden op Roku](sdk-implement/track-chapters/track-chapters-roku.md)
   + Trackkwaliteit {#track-qos}
      + [Overzicht](sdk-implement/track-qos/track-qos-overview.md)
      + [Trackkwaliteit van ervaringen op Android](sdk-implement/track-qos/track-qos-android.md)
      + [Kwaliteit van ervaring bijhouden op iOS](sdk-implement/track-qos/track-qos-ios.md)
      + [Kwaliteit van ervaring bijhouden in JavaScript](sdk-implement/track-qos/track-qos-js.md)
      + [Trackkwaliteit van ervaring op chroomecast](sdk-implement/track-qos/track-qos-chromecast.md)
      + [Trackkwaliteit van ervaring op Roku](sdk-implement/track-qos/track-qos-roku.md)
   + Fouten bijhouden {#track-errors}
      + [Overzicht](sdk-implement/track-errors/track-errors-overview.md)
      + [Fouten bijhouden op Android](sdk-implement/track-errors/track-errors-android.md)
      + [Fouten bijhouden op iOS](sdk-implement/track-errors/track-errors-ios.md)
      + [Fouten bijhouden in JavaScript](sdk-implement/track-errors/track-errors-js.md)
      + [Fouten bijhouden op chroecast](sdk-implement/track-errors/track-errors-chromecast.md)
      + [Fouten bijhouden op Roku](sdk-implement/track-errors/track-errors-roku.md)
   + [Afmelden en Privacy](sdk-implement/opt-out-privacy.md)
   + Scenario&#39;s bijhouden {#tracking-scenarios}
      + [VOD afspelen zonder advertenties](sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
      + [VOD afspelen met pre-roll-advertenties](sdk-implement/tracking-scenarios/vod-preroll-ads.md)
      + [VOD afspelen met overgeslagen advertenties](sdk-implement/tracking-scenarios/vod-skipped-ads.md)
      + [VOD afspelen met één hoofdstuk](sdk-implement/tracking-scenarios/vod-one-chapter.md)
      + [VOD afspelen met een overgeslagen hoofdstuk](sdk-implement/tracking-scenarios/vod-skipped-chapter.md)
      + [VOD afspelen met zoeken in de hoofdinhoud](sdk-implement/tracking-scenarios/vod-seeking.md)
      + [VOD afspelen met bufferen](sdk-implement/tracking-scenarios/vod-buffering.md)
      + [Meerdere VOD-trackers parallel](sdk-implement/tracking-scenarios/vod-multi-trackers.md)
      + [VOD één tracker voor meerdere sessies](sdk-implement/tracking-scenarios/vod-multi-track-one-session.md)
      + [Actieve hoofdinhoud](sdk-implement/tracking-scenarios/live-main-content.md)
      + [Actieve hoofdinhoud met opeenvolgende spatiëring](sdk-implement/tracking-scenarios/live-sequential.md)
   + Validatie {#validation}
      + [Validatieoverzicht](sdk-implement/validation/validation-overview.md)
      + [Test 1: Standaard afspelen](sdk-implement/validation/test1-standard-playback.md)
      + [Test 2: Onderbreking media](sdk-implement/validation/test2-media-interrupt.md)
      + [Details van de Vraag van de test](sdk-implement/validation/test-call-details.md)
      + [Beschrijvingen van hartslagparameters](sdk-implement/validation/heartbeat-params.md)
      + Foutopsporing {#debugging}
         + [Foutopsporing in SDK](sdk-implement/validation/debugging/sdk-debugging.md)
         + [Adobe Debug configureren](sdk-implement/validation/debugging/config-adobe-debug.md)
         + [Nieuw foutopsporingsrapport maken](sdk-implement/validation/debugging/create-new-debug-report.md)
         + [Fouten opsporen in dashboards en rapporten](sdk-implement/validation/debugging/debug-dash-repts.md)
   + Analyses in OTT-apps {#analytics-with-ott}
      + [App-statussen bijhouden](sdk-implement/analytics-with-ott/track-app-states.md)
      + [Toepassingshandelingen bijhouden](sdk-implement/analytics-with-ott/track-app-actions.md)
      + [Gebruikersnaam instellen](sdk-implement/analytics-with-ott/set-user-ids.md)
      + [OTT en Audience Manager](sdk-implement/analytics-with-ott/ott-am.md)
      + [OTT en Experience Cloud](sdk-implement/analytics-with-ott/ott-experience-cloud.md)
   + Cookbook {#cookbook}
      + [SDK Cookbook](sdk-implement/cookbook/sdk-cookbook-overview.md)
      + [Toepassing onderbreekt tijdens afspelen](sdk-implement/cookbook/app-interrupts.md)
      + [Hoofdbestand omzetten:afspelen tussen advertenties](sdk-implement/cookbook/fix-ad-play-ad.md)
      + [Inactieve sessies hervatten](sdk-implement/cookbook/resuming-inactive.md)
      + [Tracking in SceneGraph (Roku)](sdk-implement/cookbook/sdk-track-scenegraph.md)
   + Migratie van media-analyse 1.x tot 2.x {#va-1x-to-2x}
      + [Migratieoverzicht](sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
      + [Codevergelijking: 1.x tot 2.x](sdk-implement/va-1x-to-2x/code-comparison-1x-2x.md)
      + [1.x naar 2.x API-conversie](sdk-implement/va-1x-to-2x/1x-2x-api-change.md)
   + Media Analytics SDK om migratie te starten {#sdk-to-launch}
      + [SDK om migratie te starten](sdk-implement/sdk-to-launch/sdk-to-launch-migration.md)
      + SDK voor starten van migratieplatformhulplijnen {#sdk-to-launch-migration-platforms}
         + [Android](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)
         + [iOS](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)
         + [JS](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-js.md)
+ Media Collection API (RESTful) {#media-collection-api}
   + [Overzicht](media-collection-api/mc-api-overview.md)
   + API-naslag {#mc-api-ref}
      + [Aanvraag sessie](media-collection-api/mc-api-ref/mc-api-sessions-req.md)
      + [Aanvraag voor gebeurtenissen](media-collection-api/mc-api-ref/mc-api-events-req.md)
      + [Parameters aanvragen](media-collection-api/mc-api-ref/mc-api-req-params.md)
      + [Gebeurtenistypen en beschrijvingen](media-collection-api/mc-api-ref/mc-api-event-types.md)
      + [JSON-validatieschema&#39;s](media-collection-api/mc-api-ref/mc-api-json-validation.md)
   + De API implementeren {#mc-api-impl}
      + [Snel starten](media-collection-api/mc-api-impl/mc-api-quick-start.md)
      + [Het HTTP-aanvraagtype instellen in de Player](media-collection-api/mc-api-impl/mc-api-set-http-req.md)
      + [Zitting-id verkrijgen](media-collection-api/mc-api-impl/mc-api-obtain-sid.md)
      + [Een Events-aanvraag implementeren](media-collection-api/mc-api-impl/mc-api-impl-events-req.md)
      + [Gebeurtenisverzoeken valideren](media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
      + [Pingsgebeurtenissen verzenden](media-collection-api/mc-api-impl/mc-api-sed-pings.md)
      + [QoE-gegevens verzenden](media-collection-api/mc-api-impl/mc-api-sending-qoe.md)
      + [Ondersteuning voor aangepaste metagegevens](media-collection-api/mc-api-impl/mc-api-custom-meta.md)
      + [Tijdslimiet](media-collection-api/mc-api-impl/mc-api-timeout.md)
      + [De volgorde van gebeurtenissen bepalen](media-collection-api/mc-api-impl/mc-api-ctrl-order.md)
      + [Gebeurtenissen in wachtrij wanneer de reactie op sessies traag is](media-collection-api/mc-api-impl/mc-api-queuing.md)
   + Tijdlijnen voor het bijhouden van media {#mc-api-timelines}
      + [Tijdlijn 1 - Weergeven tot einde van inhoud](media-collection-api/mc-api-timelines/mc-api-timeline-1.md)
      + [Tijdlijn 2 - Afloopsessie van gebruiker](media-collection-api/mc-api-timelines/mc-api-timeline-2.md)
      + [Tijdlijn 3 - Hoofdstukken](media-collection-api/mc-api-timelines/mc-api-timeline-3.md)
   + [Gedownloade inhoud bijhouden](media-collection-api/track-downloaded-content.md)
+ Cookbook {#media-analytics-cookbook}
   + [Cookbook](media-analytics-cookbook/media-analytics-cookbook.md)
   + [Attributie van mediastroom](media-analytics-cookbook/media-dimensions.md)
+ Metriek en metagegevens {#metrics-and-metadata}
   + [Parameters voor audio en video](metrics-and-metadata/audio-video-parameters.md)
   + [Ad-parameters](metrics-and-metadata/ad-parameters.md)
   + [Hoofdstukparameters](metrics-and-metadata/chapter-parameters.md)
   + [Kwaliteitsparameters](metrics-and-metadata/quality-parameters.md)
   + [Segmenten](metrics-and-metadata/segments.md)
   + [Berekende cijfers](metrics-and-metadata/calculated-metrics.md)
+ Rapportage en analyse {#media-reports}
   + [Inschakelen van mediabapporten](media-reports/media-reports-enable.md)
   + Standaardrapporten media {#media-default-reports}
      + [Overzicht van standaardrapporten](media-reports/media-default-reports/default-reports-overview.md)
      + [Overzicht van media](media-reports/media-default-reports/media-reports-overview.md)
      + [Details media](media-reports/media-default-reports/media-reports-detail.md)
      + [Media Daypart](media-reports/media-default-reports/media-reports-daypart.md)
      + [Mediagelijktijdige viewers](media-reports/media-default-reports/media-concurrent-viewers.md)
      + [JSON-rapportgegevens voor gelijktijdige viewers ophalen](media-reports/media-default-reports/get-concurrent-json.md)
   + [Sjablonen voor werkruimte van media](media-reports/media-workspace-templates.md)
+ [Federale analyse](federated-analytics.md)
+ Aanvullende bronnen {#additional-resources}
   + [Opmerkingen bij de release](additional-resources/doc-updates.md)
