<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Downloads-and-Offline-Reading",
  "metadataVersion" : "0.1.0",
  "role" : "collectionGroup",
  "title" : "Downloads and Offline Reading"
}
-->

# Downloads and Offline Reading

Let users download editions from the prebuilt archive, manage them on a Downloads screen, and read them offline.

## Overview

The prebuilt UI downloads editions for offline reading. Each edition in
an archive has a download button, the reader shows a download’s progress
under its navigation bar, and a Downloads screen lists the editions on
the device. Building a custom UI? See [Adding a Download Button](/documentation/PSReader/Adding-a-Download-Button).

The download buttons need no setup. To give users a place to find their
downloads, add the Downloads screen to the carousel as a section, or as a
subsection beside your bookmarks:

```swift
let carousel = CarouselViewController(
    globalConfig: globalConfig,
    sections: [
        .dynamicArchive("Editions", shortcode: "SHORTCODE"),
        .section(.init(name: "Downloads", type: .downloads(type: .all)))
    ]
)
```

![The downloads screen with one edition downloading and one downloaded.](images/com.pagesuite.PSReader/downloads-screen@2x.png)

A tap on an edition’s download button downloads it, a tap during the
download cancels it, and a tap on a downloaded edition deletes the copy.
A downloaded edition is a complete copy, and the reader opens it without
a network connection, from whichever screen opens it. The reader can also
download editions as they open; see
[Download Settings in the Prebuilt Reader](/documentation/PSReader/Downloads-and-Offline-Reading#Download-Settings-in-the-Prebuilt-Reader).

The Downloads screen lists the editions that are downloaded,
downloading, or queued, and opens one in the reader when tapped. Each
item’s button cancels or deletes its download.

In the carousel, the section’s ribbon has a menu that sorts the list by
download date or edition date, and deletes every download after asking.
The menu appears in a section whose first subsection is Downloads or
Bookmarks.

Every screen shares one store of downloads, so an edition downloaded from
one screen shows as downloaded on every other.

## Showing Downloads in Your Own Navigation

[`DownloadsViewController`](/documentation/PSReader/DownloadsViewController) is the same Downloads screen for your own
navigation. Outside the carousel it has no menu, so give it a sort
control of your own through
[`sortMode`](/documentation/PSReader/DownloadsViewController/sortMode-swift.property). The chosen order
persists across launches.

```swift
let downloads = DownloadsViewController(globalConfig: globalConfig, downloadTypes: .all)
downloads.title = "Downloads"
downloads.navigationItem.rightBarButtonItem = UIBarButtonItem(
    image: UIImage(systemName: "arrow.up.arrow.down"),
    menu: UIMenu(children: [
        UIAction(title: "Recently Downloaded") { [weak downloads] _ in
            downloads?.sortMode = .byDownloaded
        },
        UIAction(title: "Edition Date") { [weak downloads] _ in
            downloads?.sortMode = .byDate
        }
    ])
)

navigationController?.pushViewController(downloads, animated: true)
```

If a container of yours covers part of the screen, such as a custom tab
bar, set [`additionalSafeAreaInsets`](/documentation/PSReader/DownloadsViewController/additionalSafeAreaInsets) to keep the
list clear of it.

[`ArchiveViewController`](/documentation/PSReader/ArchiveViewController) has the same download buttons as the carousel’s
archives, and [`FeedReaderViewController`](/documentation/PSReader/FeedReaderViewController) follows the reader’s download
settings (see [Download Settings in the Prebuilt Reader](/documentation/PSReader/Downloads-and-Offline-Reading#Download-Settings-in-the-Prebuilt-Reader)).

## Configuring the Downloads Screen

The content type says which editions the screen lists:
[`feedEdition`](/documentation/PSReader/DownloadsConfiguration/DownloadType/feedEdition) for editions on the
current system, [`replicaEdition`](/documentation/PSReader/DownloadsConfiguration/DownloadType/replicaEdition) for
replica editions, or `.all` for both. Pass it as `type` in the carousel,
or as `downloadTypes` to [`DownloadsViewController`](/documentation/PSReader/DownloadsViewController).

A [`DownloadsConfiguration`](/documentation/PSReader/DownloadsConfiguration) styles the screen and sets up the reader it
opens editions in. Pass one as `config` in the carousel, or as
`downloadsConfig` to [`DownloadsViewController`](/documentation/PSReader/DownloadsViewController). Its
[`readerConfig`](/documentation/PSReader/DownloadsConfiguration/readerConfig) starts with copies of your global
configuration’s delegates; change it to set up that reader alone:

```swift
var downloadsConfig = DownloadsConfiguration(globalConfig: globalConfig)
downloadsConfig.downloadIconColor = .systemOrange
downloadsConfig.readerConfig.settings.isClearEditionDataEnabled = false

let downloads = DownloadsViewController(
    globalConfig: globalConfig,
    downloadsConfig: downloadsConfig,
    downloadTypes: .feedEdition
)
```

[Theming](/documentation/PSReader/Theming) covers the screen’s colors, labels, and empty state, and
[Customizing the Reader Screen](/documentation/PSReader/Customizing-the-Reader-Screen) the reader’s.

The screen opens the editions it lists without asking your paywall
delegate; see [Where the Prebuilt UI Asks](/documentation/PSReader/Paywalls#Where-the-Prebuilt-UI-Asks).

> Replica: Replica editions download through the legacy replica system,
> not ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager``. A Downloads screen lists them when its type
> includes ``doc://com.pagesuite.PSReader/documentation/PSReader/DownloadsConfiguration/DownloadType/replicaEdition``, as
> `.all` does, and opens them in the replica reader.

## Download Settings in the Prebuilt Reader

The prebuilt reader’s settings menu has a Data Settings page for
downloads. Each row has a [`SettingsConfiguration`](/documentation/PSReader/SettingsConfiguration) property that hides
it; set them on the [`settings`](/documentation/PSReader/ReaderConfiguration/settings) of each reader
configuration you use, including each carousel section’s and screen’s
`readerConfig` (see [Customizing the Reader Screen](/documentation/PSReader/Customizing-the-Reader-Screen)).

|Row                       |What it does                                                                                                                                                                                                           |Hide with                                                                                                        |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|
|Download while reading    |Opening an edition that isn’t downloaded downloads it instead of streaming it. The reader opens once the splash phase is done, and the rest downloads as the user reads. Editions opened from a bookmark always stream.|``doc://com.pagesuite.PSReader/documentation/PSReader/SettingsConfiguration/isDownloadWhileReadingToggleEnabled``|
|Mobile data downloads     |When off, downloads can’t start on a cellular connection. The archive’s download button shows an alert, and “Download while reading” streams instead.                                                                  |``doc://com.pagesuite.PSReader/documentation/PSReader/SettingsConfiguration/isAllowCelluarDownloadEnabled``      |
|Clear edition data        |After asking, deletes every download and bookmark, and the reader’s cached content.                                                                                                                                    |``doc://com.pagesuite.PSReader/documentation/PSReader/SettingsConfiguration/isClearEditionDataEnabled``          |
|Auto delete editions after|When the user picks an age, deletes the downloads older than it.                                                                                                                                                       |``doc://com.pagesuite.PSReader/documentation/PSReader/SettingsConfiguration/isAutoDeleteEditionsEnabled``        |

Hiding a row only takes it out of the menu. Its setting stays as it was:
the user’s last choice, or the default. Mobile data downloads are
allowed until the user turns them off.

“Download while reading” starts off. To turn it on for new users, set
[`downloadWhileReadingDefault`](/documentation/PSReader/SettingsConfiguration/downloadWhileReadingDefault). The first time the
reader appears, it asks the user to choose, unless you set
[`isDownloadWhileReadingPreferenceAlertEnabled`](/documentation/PSReader/SettingsConfiguration/isDownloadWhileReadingPreferenceAlertEnabled) to
`false`. The user’s choices persist across launches and take precedence
over your defaults. “Download while reading” doesn’t ask your paywall
delegate’s download method; see
[Gating Downloads Separately](/documentation/PSReader/Paywalls#Gating-Downloads-Separately).

Whenever the edition on screen is downloading, from this setting or a
download button, the reader shows the download’s progress under its
navigation bar.

## Gating and Removing Download Buttons

Each tap on an archive’s download button first asks your paywall
delegate, which gates downloading like opening unless you give downloads
a check of their own; see [Gating Downloads Separately](/documentation/PSReader/Paywalls#Gating-Downloads-Separately).

To remove the buttons from an archive, set
[`downloadButtonEnabled`](/documentation/PSReader/ArchiveConfiguration/downloadButtonEnabled) to `false` on its
configuration:

```swift
var archiveConfig = ArchiveConfiguration(globalConfig: globalConfig)
archiveConfig.downloadButtonEnabled = false
```

## Managing Downloads From Your Code

The prebuilt screens keep their downloads in [`PSEDownloadManager`](/documentation/PSReader/PSEDownloadManager), so
a few calls reach them from your code. To clear a user’s downloads when
they sign out, cancel the downloads in progress, then delete the rest:

```swift
PSEDownloadManager.shared.cancelAllDownloads()
PSEDownloadManager.shared.deleteDownloads()
```

To badge an edition in a screen of your own, check
[`isDownloaded(published:)`](/documentation/PSReader/PSEDownloadManager/isDownloaded(published:)).

Downloads make progress only while your app runs, and the stored copies
live in the app’s Caches directory, which iOS may clear when the device
runs low on storage. [Adding a Download Button](/documentation/PSReader/Adding-a-Download-Button) covers the rest of
the manager: download states, storage, connectivity, and background
behavior.

> Replica: These calls don’t reach replica downloads, which the legacy
> replica system keeps.

## Downloads From the Legacy SDK

The prebuilt Downloads screen lists the legacy SDK’s downloads itself,
as replica content, when its type includes
[`replicaEdition`](/documentation/PSReader/DownloadsConfiguration/DownloadType/replicaEdition), and opens them in
the replica reader. Apps that use the prebuilt screens leave out
[`migrateLegacyDownloads(hooks:)`](/documentation/PSReader/PSEDownloadManager/migrateLegacyDownloads(hooks:)), the custom UI’s
migration call, which would list each download twice. See
[With the Prebuilt Screens](/documentation/PSReader/Migrating-From-the-Legacy-Core-SDK#With-the-Prebuilt-Screens).

## Topics

### Showing Downloads

[`DownloadsViewController`](/documentation/PSReader/DownloadsViewController)

A standalone view controller for displaying downloaded editions.

### Configuring the Downloads Screen

[`DownloadsConfiguration`](/documentation/PSReader/DownloadsConfiguration)

Configuration for customizing the appearance and behavior of download archives.

