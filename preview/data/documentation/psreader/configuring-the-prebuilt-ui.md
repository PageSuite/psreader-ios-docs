<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Configuring-the-Prebuilt-UI",
  "metadataVersion" : "0.1.0",
  "role" : "collectionGroup",
  "title" : "Configuring the Prebuilt UI"
}
-->

# Configuring the Prebuilt UI

Set the prebuilt UI’s appearance and behavior once, globally, and override it where a screen needs something different.

## Overview

The prebuilt UI reads its fonts, colors, delegates, and behavior from a
cascade of configuration values. [`GlobalConfiguration`](/documentation/PSReader/GlobalConfiguration) sits at the top.
Every other configuration is created from it, starts with its values, and
can override any of them:

```swift
let globalConfig = GlobalConfiguration(
    apiKey: "API_KEY",
    accountGUID: "ACCOUNT_GUID",
    primaryFont: UIFont(name: "Georgia", size: 12)!,
    secondaryFont: .systemFont(ofSize: 12),
    brandColor: .systemBlue
)

var archiveConfig = ArchiveConfiguration(globalConfig: globalConfig)
archiveConfig.readerConfig.backgroundColor = .black   // only this archive's reader
```

The archive configuration above inherits the Georgia font and the blue
brand color, and so does the reader configuration inside it. Only the
reader’s background differs. [Theming](/documentation/PSReader/Theming) covers the appearance values
themselves.

A custom UI has no cascade: [`PSEditionReaderViewController`](/documentation/PSReader/PSEditionReaderViewController) takes its
few settings directly; see [Hosting the Reader](/documentation/PSReader/Hosting-the-Reader).

## The Cascade

Each configuration covers one part of the prebuilt UI, and the reader’s
configuration nests inside the screens that open it:

```
GlobalConfiguration                 credentials, fonts, brand color, delegates, app configuration
├─ CarouselConfiguration            section and subsection ribbons, header
├─ ArchiveConfiguration             one archive: grid, labels, date picker
│  └─ ReaderConfiguration           the reader this archive opens
│     ├─ ReaderNavigationBarConfiguration
│     ├─ ReaderBrowserConfiguration
│     ├─ ReaderSplashConfiguration
│     ├─ SettingsConfiguration
│     └─ LegacyReaderConfiguration
├─ BookmarksConfiguration
│  └─ ReaderConfiguration           the reader bookmarks open
├─ DownloadsConfiguration
│  └─ ReaderConfiguration           the reader downloads open
└─ SearchConfiguration
```

|Configuration                                                                                                                                                 |Configures                                                                                   |Pass it to                                                                                                                                                                                     |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|``doc://com.pagesuite.PSReader/documentation/PSReader/GlobalConfiguration``                                                                                   |Credentials, fonts, brand color, time zone, date format, delegates, and the app configuration|Every prebuilt view controller                                                                                                                                                                 |
|``doc://com.pagesuite.PSReader/documentation/PSReader/CarouselConfiguration``                                                                                 |The carousel’s ribbons, header, and navigation                                               |``doc://com.pagesuite.PSReader/documentation/PSReader/CarouselViewController``                                                                                                                 |
|``doc://com.pagesuite.PSReader/documentation/PSReader/ArchiveConfiguration``                                                                                  |One archive’s grid, labels, and date picker, plus its reader                                 |A carousel section’s `config`, ``doc://com.pagesuite.PSReader/documentation/PSReader/ArchiveViewController``, ``doc://com.pagesuite.PSReader/documentation/PSReader/KioskFeedPublication``     |
|``doc://com.pagesuite.PSReader/documentation/PSReader/ReaderConfiguration``                                                                                   |The reader screen and its parts                                                              |`readerConfig` on an archive, bookmarks, or downloads configuration; ``doc://com.pagesuite.PSReader/documentation/PSReader/FeedReaderViewController``                                          |
|``doc://com.pagesuite.PSReader/documentation/PSReader/BookmarksConfiguration``, ``doc://com.pagesuite.PSReader/documentation/PSReader/DownloadsConfiguration``|Those screens, plus their readers                                                            |A carousel section’s `config`, ``doc://com.pagesuite.PSReader/documentation/PSReader/BookmarksViewController``, ``doc://com.pagesuite.PSReader/documentation/PSReader/DownloadsViewController``|
|``doc://com.pagesuite.PSReader/documentation/PSReader/SearchConfiguration``                                                                                   |Search, in its own screen or in the reader                                                   |`.search(config:)`, ``doc://com.pagesuite.PSReader/documentation/PSReader/SearchViewController``, ``doc://com.pagesuite.PSReader/documentation/PSReader/ReaderConfiguration/search``           |

Wherever a configuration is optional and you pass `nil`, the SDK creates
one from your global configuration. You only build the ones you change.

## How Values Flow

A configuration copies its values from the global configuration when you
create it. It doesn’t watch the global configuration afterward:

```swift
var globalConfig = GlobalConfiguration(apiKey: "API_KEY", accountGUID: "ACCOUNT_GUID")
let archiveConfig = ArchiveConfiguration(globalConfig: globalConfig)

globalConfig.brandColor = .systemRed   // archiveConfig keeps the old brand color
```

So finish the global configuration first, then create the rest from it.
To change one screen, change its own configuration; to change everything,
change the global configuration before you create anything else.

Delegates flow the same way. A [`ReaderConfiguration`](/documentation/PSReader/ReaderConfiguration) starts with all
eight of the global configuration’s delegates:

- ``doc://com.pagesuite.PSReader/documentation/PSReader/GlobalConfiguration/shareDelegate``, see <doc://com.pagesuite.PSReader/documentation/PSReader/Sharing>
- ``doc://com.pagesuite.PSReader/documentation/PSReader/GlobalConfiguration/assetDelegate``, see <doc://com.pagesuite.PSReader/documentation/PSReader/Theming#Icons>
- ``doc://com.pagesuite.PSReader/documentation/PSReader/GlobalConfiguration/audioDelegate``, see <doc://com.pagesuite.PSReader/documentation/PSReader/Text-to-Speech>
- ``doc://com.pagesuite.PSReader/documentation/PSReader/GlobalConfiguration/paywallDelegate``, see <doc://com.pagesuite.PSReader/documentation/PSReader/Paywalls>
- ``doc://com.pagesuite.PSReader/documentation/PSReader/GlobalConfiguration/advertDelegate``, see <doc://com.pagesuite.PSReader/documentation/PSReader/Advertisements>
- ``doc://com.pagesuite.PSReader/documentation/PSReader/GlobalConfiguration/mediaDelegate``, see <doc://com.pagesuite.PSReader/documentation/PSReader/Media-and-Links>
- ``doc://com.pagesuite.PSReader/documentation/PSReader/GlobalConfiguration/navigationDelegate``, see
  <doc://com.pagesuite.PSReader/documentation/PSReader/Customizing-the-Reader-Screen#Replica-Editions>
- ``doc://com.pagesuite.PSReader/documentation/PSReader/GlobalConfiguration/commentingDelegate``, see <doc://com.pagesuite.PSReader/documentation/PSReader/Commenting>

Set a different one on a reader configuration to change it for that
reader only. Other configurations copy the delegates their screen uses,
such as the carousel’s paywall delegate and the search screen’s asset
delegate.

The app configuration, [`remoteConfig`](/documentation/PSReader/GlobalConfiguration/remoteConfig), flows the
same way: each screen and reader keeps the value it had when you created
it. See [The App Configuration](/documentation/PSReader/Configuring-the-Prebuilt-UI#The-App-Configuration).

## Sharing One Reader Configuration

Archives, bookmarks, and downloads each open their own reader, with its
own [`ReaderConfiguration`](/documentation/PSReader/ReaderConfiguration). To make every reader match, build one reader
configuration and assign it to each:

```swift
var readerConfig = ReaderConfiguration(globalConfig: globalConfig)
readerConfig.backgroundColor = .black
readerConfig.settings.isDoublePageEnabled = false

var archiveConfig = ArchiveConfiguration(globalConfig: globalConfig)
archiveConfig.readerConfig = readerConfig

var bookmarksConfig = BookmarksConfiguration(globalConfig: globalConfig)
bookmarksConfig.readerConfig = readerConfig

var downloadsConfig = DownloadsConfiguration(globalConfig: globalConfig)
downloadsConfig.readerConfig = readerConfig
```

Then pass each one where it belongs, for example as the `config` of a
carousel section.

## The App Configuration

The app configuration is what PageSuite keeps for your shortcode: your
publications and archives, advert settings, article widgets, and logos.
The prebuilt UI holds it, as a [`PSAppConfig`](/documentation/PSReader/PSAppConfig), in
[`remoteConfig`](/documentation/PSReader/GlobalConfiguration/remoteConfig).

Most apps never set it. A dynamic archive loads it from its shortcode and
hands it to every screen and reader in the carousel, and
[`FeedReaderViewController`](/documentation/PSReader/FeedReaderViewController)’s shortcode initializer loads it for the
reader it opens.

Elsewhere it’s `nil` unless you set it: in a carousel without a dynamic
archive, in screens you embed, and in readers you open with
[`FeedReaderViewController`](/documentation/PSReader/FeedReaderViewController)’s other initializers, even in an app whose
carousel has a dynamic archive. The prebuilt UI works without it, apart
from the features that read it:

- In-article adverts, which PageSuite places in article pages, and their
  targeting.
- Third-party advert pages, which prefer the ad-stack scripts it lists to
  the page’s own copy, and load against the advert domain it names when
  neither the page nor ``doc://com.pagesuite.PSReader/documentation/PSReader/ReaderConfiguration/baseURL`` gives a base URL.
  A page with no base URL at all has no web origin, which blocks ad
  serving.
- Widgets that PageSuite adds to article pages.
- The masthead logo some page templates show, unless your asset
  delegate’s ``doc://com.pagesuite.PSReader/documentation/PSReader/AssetDelegate/headerLogo(for:currentTraitCollection:)``
  supplies one.

If your editions use any of them, load the configuration with
[`AppConfigService`](/documentation/PSReader/AppConfigService) and set it before you create any screen:

```swift
var globalConfig = GlobalConfiguration(apiKey: "API_KEY", accountGUID: "ACCOUNT_GUID")
globalConfig.remoteConfig = try? await AppConfigService().configuration(forShortcode: "SHORTCODE")
```

Each call fetches the configuration from PageSuite. If it fails, for
example when the device is offline, `try?` leaves the value `nil` and the
prebuilt UI opens editions without those features.

## Dynamic Archives

When a dynamic archive, `.dynamicArchive(_:shortcode:config:)`, loads the
app configuration, a few of its values win over yours:

- ``doc://com.pagesuite.PSReader/documentation/PSReader/ArchiveConfiguration/archiveLimit`` is ignored; the archive limit set
  in PageSuite applies.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/ArchiveConfiguration/feedPublicationType-swift.property`` comes from each
  publication’s type.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/ArchiveConfiguration/datePicker`` comes from PageSuite when you leave
  it `nil`. Set one to use it for every publication in the archive.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/ReaderConfiguration/baseURL`` and ``doc://com.pagesuite.PSReader/documentation/PSReader/GlobalConfiguration/remoteConfig``
  are replaced with the configured values.

Everything else in your configuration still applies.

> Replica: ``doc://com.pagesuite.PSReader/documentation/PSReader/LegacyReaderConfiguration``, at
> ``doc://com.pagesuite.PSReader/documentation/PSReader/ReaderConfiguration/legacyReader``, configures the legacy replica
> reader, which has its own navigation bar and icons. See
> <doc://com.pagesuite.PSReader/documentation/PSReader/Customizing-the-Reader-Screen>.

## Topics

### Global Configuration

[`GlobalConfiguration`](/documentation/PSReader/GlobalConfiguration)

A configuration object that provides global settings and delegates for
customizing the SDK’s behavior and appearance.

