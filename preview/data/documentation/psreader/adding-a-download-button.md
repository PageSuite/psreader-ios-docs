<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Adding-a-Download-Button",
  "metadataVersion" : "0.1.0",
  "role" : "collectionGroup",
  "title" : "Adding a Download Button"
}
-->

# Adding a Download Button

Add a download button to your own reader screen or archive that stores editions for offline reading, and list what’s on the device, with the SDK’s download manager.

## Overview

The prebuilt UI puts a download button on each edition in its archive,
shows the download’s progress in the reader, and lists stored editions
on a Downloads screen. In your own screens you build the button and the
list, and [`shared`](/documentation/PSReader/PSEDownloadManager/shared) does the downloading: it fetches
editions one at a time, keeps the stored copies, and reports each
edition’s state to observers.

Using the prebuilt UI? See [Downloads and Offline Reading](/documentation/PSReader/Downloads-and-Offline-Reading).

```swift
// Follow one edition's download. The call returns its current state.
let state = PSEDownloadManager.shared.addObserver(self, published: published)

// On a tap: queue, cancel, or delete, depending on the state.
try PSEDownloadManager.shared.toggleDownloadState(for: published)
```

A downloaded edition is a complete copy on the device, and it opens
offline. Your opening code doesn’t change:
[`openEditionSource(onProgress:)`](/documentation/PSReader/PSEPublished/openEditionSource(onProgress:)) opens the stored copy when
there is one.

The prebuilt screens use the same manager. If your app mixes any of them
in, they show the downloads your button starts, and your screens show
theirs.

## Building the Button

This is the sample app’s button, in a file of its own: a bar button item
for one edition. Observing the edition returns its current state, so the
button draws itself at once, and a tap calls
[`toggleDownloadState(for:)`](/documentation/PSReader/PSEDownloadManager/toggleDownloadState(for:)):

```swift
import UIKit
import PSReader

/// A bar button that downloads an edition for offline reading, shows the
/// progress, and removes the download again.
final class DownloadButton: UIBarButtonItem, PSEDownloadObserver {

    /// Called when a download can't start: offline, or on cellular when
    /// downloads are limited to Wi-Fi.
    var onError: ((Error) -> Void)?

    private let published: PSEPublished

    init(published: PSEPublished) {
        self.published = published
        super.init()

        target = self
        action = #selector(toggleDownload)

        // Observing one edition returns its current state, so the button
        // can draw itself before the first update arrives.
        render(PSEDownloadManager.shared.addObserver(self, published: published))
    }

    required init?(coder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }

    @objc private func toggleDownload() {
        do {
            // Queues, cancels or deletes, depending on the current state.
            try PSEDownloadManager.shared.toggleDownloadState(for: published)
        } catch {
            onError?(error)
        }
    }

    func downloadManager(
        _ downloadManager: PSEDownloadManager,
        downloadFor published: PSEPublished,
        didChangeState state: PSEDownloadManager.DownloadState
    ) {
        render(state)
    }

    private func render(_ state: PSEDownloadManager.DownloadState) {
        switch state {
        case .queued:
            title = nil
            image = UIImage(systemName: "stop.circle")
            accessibilityLabel = "Cancel Download"
        case let .downloading(_, _, progress):
            title = progress.formatted(.percent.precision(.fractionLength(0)))
            image = nil
            accessibilityLabel = "Cancel Download"
        case .downloaded:
            title = nil
            image = UIImage(systemName: "checkmark.circle.fill")
            accessibilityLabel = "Remove Download"
        default:
            // Not downloaded, or a download that stopped.
            title = nil
            image = UIImage(systemName: "arrow.down.circle")
            accessibilityLabel = "Download"
        }
    }
}
```

The manager holds observers weakly, and the navigation bar keeps the
button alive. The button needs only the edition’s [`PSEPublished`](/documentation/PSReader/PSEPublished), so
it works as well on each cell of your archive screen, where the prebuilt
archive puts its download buttons.

## Adding the Button to Your Reader Screen

In `ReaderScreenViewController`, the reader screen from
[Hosting the Reader](/documentation/PSReader/Hosting-the-Reader), add the button as a property:

```swift
private lazy var downloadButton = DownloadButton(published: published)
```

In `addChrome()`, show an alert when a download can’t start, and put the
button in the navigation bar:

```swift
downloadButton.onError = { [weak self] error in
    self?.showAlert(title: "Couldn't Download Edition", error: error)
}
navigationItem.rightBarButtonItems = (navigationItem.rightBarButtonItems ?? []) + [downloadButton]
```

The button follows the manager itself, so `updateChrome()` needs nothing.

Nothing asks a paywall before a download in a custom UI. If you gate
editions, check the user’s entitlement before a tap starts one; see
[Gating Downloads](/documentation/PSReader/Gating-Editions-Behind-a-Paywall#Gating-Downloads). Downloads need
no analytics code of your own: [`EventChannel`](/documentation/PSReader/EventChannel) observes the manager and
reports [`EventChannel.AnalyticsEvent.feedEditionDownloaded(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionDownloaded(_:)) when a
download completes, whichever screen started it. See
[Downloads and Bookmarks](/documentation/PSReader/Reporting-Analytics#Downloads-and-Bookmarks).

## Download States

Observers receive a [`PSEDownloadManager.DownloadState`](/documentation/PSReader/PSEDownloadManager/DownloadState) on the main
thread whenever an edition’s download changes, including every progress
update, and [`state(for:)`](/documentation/PSReader/PSEDownloadManager/state(for:)) returns the current one.
Each download runs in two phases: the
[`PSEDownloadManager.DownloadPhase.splash`](/documentation/PSReader/PSEDownloadManager/DownloadPhase/splash) phase fetches what the reader
needs to open the edition, and the
[`PSEDownloadManager.DownloadPhase.main`](/documentation/PSReader/PSEDownloadManager/DownloadPhase/main) phase fetches the rest.

|State                                                                                                                                    |Meaning                                                                                                                                                                                                   |
|-----------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager/DownloadState/notDownloaded``                                   |No copy is on the device and nothing is queued. Removing or deleting a copy returns an edition to this state.                                                                                             |
|``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager/DownloadState/queued``                                          |Waiting for the download ahead of it to finish.                                                                                                                                                           |
|``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager/DownloadState/downloading(phase:phaseProgress:globalProgress:)``|Downloading. `phaseProgress` runs from 0 to 1 within the current phase; `globalProgress` runs from 0 to 1 across the whole download and suits a progress bar.                                             |
|``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager/DownloadState/downloaded``                                      |A complete copy is on the device.                                                                                                                                                                         |
|``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager/DownloadState/errored``                                         |The download failed: the edition’s file list couldn’t be loaded, or a file still failed after ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager/maxDownloadRetryAttempts`` retries.|
|``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager/DownloadState/cancelled``                                       |The download was canceled before it finished.                                                                                                                                                             |

A few details matter when you render these states:

- `errored` carries no underlying error. Offer a retry by queuing the
  edition again.
- The manager never reports ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager/DownloadState/deleted``;
  deleting a copy reports `notDownloaded`. Treat `deleted` like
  `notDownloaded` in a `switch`.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager/queueDownload(published:)`` doesn’t report
  `queued`. An edition queued behind another download is silent until it
  starts, so read ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager/state(for:)`` after queuing it.
- A download that
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager/downloadImmediately(published:)`` moves back
  reports `cancelled` until it starts again.

[`toggleDownloadState(for:)`](/documentation/PSReader/PSEDownloadManager/toggleDownloadState(for:)) returns a
[`PSEDownloadManager.ToggleDownloadStatus`](/documentation/PSReader/PSEDownloadManager/ToggleDownloadStatus) that says what the tap did:
queued, canceled, or deleted.

## Listing Stored Editions

For a screen of stored editions, read [`downloads`](/documentation/PSReader/PSEDownloadManager/downloads)
and keep the entries that are on the device or on their way:

```swift
let onDevice = PSEDownloadManager.shared.downloads.filter { download in
    switch download.state {
    case .downloaded, .downloading, .queued:
        return true
    default:
        return false
    }
}
```

Each [`PSEDownloadManager.Download`](/documentation/PSReader/PSEDownloadManager/Download) carries the edition’s
[`PSEPublished`](/documentation/PSReader/PSEPublished) for its row, and the date it was queued for sorting.
Register with [`addObserver(_:)`](/documentation/PSReader/PSEDownloadManager/addObserver(_:)) to hear about every
edition, and update the screen as states change. In SwiftUI, observe the
manager itself: it’s an `ObservableObject` that publishes its
`downloads`.

Open a stored edition the way you open any other:
`ReaderScreenViewController(published:)` opens the stored copy, since
[`openEditionSource(onProgress:)`](/documentation/PSReader/PSEPublished/openEditionSource(onProgress:)) prefers it. To badge
editions in your archive, check
[`isDownloaded(published:)`](/documentation/PSReader/PSEDownloadManager/isDownloaded(published:)).

## Starting a Download Without a Button

To start a download from your own logic, such as downloading each new
edition as it’s published,
[`queueDownload(published:)`](/documentation/PSReader/PSEDownloadManager/queueDownload(published:)) adds an edition behind
any others, and [`downloadImmediately(published:)`](/documentation/PSReader/PSEDownloadManager/downloadImmediately(published:))
starts it now, moving the current download back to the front of the
queue. Neither checks the connection; see
[Connectivity and Background Behavior](/documentation/PSReader/Adding-a-Download-Button#Connectivity-and-Background-Behavior).

To open an edition before its download finishes, see
[Opening While Downloading](/documentation/PSReader/Opening-an-Edition#Opening-While-Downloading).

## Managing Stored Editions

Check an edition with [`isDownloaded(published:)`](/documentation/PSReader/PSEDownloadManager/isDownloaded(published:)) or
[`state(for:)`](/documentation/PSReader/PSEDownloadManager/state(for:)).
[`downloadedEdition(for:)`](/documentation/PSReader/PSEDownloadManager/downloadedEdition(for:)) returns the catalog entry
stored with the download, as it was when the edition downloaded.

- **Delete.** ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager/removeDownload(for:)`` deletes one
  downloaded edition. ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager/deleteDownloads()`` deletes
  every downloaded edition and leaves downloads in progress alone.
- **Cancel.** ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager/cancelDownload(for:)`` cancels a queued
  or running download and discards what it fetched.
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager/cancelAllDownloads()`` cancels them all.
- **Refresh.** Publishers sometimes update an edition after it’s
  published. Pass a fresh catalog entry to
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager/removeOutdatedDownload(for:)`` and it deletes a
  stored copy older than that update, so the next open streams the
  current content. The prebuilt archive does this for every edition it
  loads; do the same when you fetch the catalog, and queue the edition
  again if it should stay on the device.
- **Tune.** ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager/concurrentFileDownloads`` (16 by default)
  sets how many files one edition fetches at once, and
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager/maxDownloadRetryAttempts`` (3 by default) how often
  a failed file is retried. Changes apply from the next edition that
  starts downloading.

Stored editions, and the manager’s list of them, live in the app’s Caches
directory, which iOS may clear when the device runs low on storage.

## Connectivity and Background Behavior

[`toggleDownloadState(for:)`](/documentation/PSReader/PSEDownloadManager/toggleDownloadState(for:)) checks the connection
before it queues an edition, and throws a [`PSDownloadError`](/documentation/PSReader/PSDownloadError) when the
download can’t start:

```swift
do {
    try PSEDownloadManager.shared.toggleDownloadState(for: published)
} catch PSDownloadError.noNetwork {
    showMessage("Connect to the internet to download this edition.")
} catch PSDownloadError.noWiFi {
    showMessage("Connect to Wi-Fi to download this edition.")
} catch {
    showMessage("This edition can't be downloaded right now.")
}
```

`showMessage(_:)` stands for your own alert. The SDK starts monitoring the
connection when [`initialize(apiKey:completion:)`](/documentation/PSReader/initialize(apiKey:completion:)) runs; until its first reading,
every check reports `noNetwork`.

[`PSDownloadError.noWiFi`](/documentation/PSReader/PSDownloadError/noWiFi) follows the prebuilt reader’s “Mobile data
downloads” setting. A custom UI has no such setting, so store a
Wi-Fi-only preference of your own and check it before you queue a
download. [`queueDownload(published:)`](/documentation/PSReader/PSEDownloadManager/queueDownload(published:)) and
[`downloadImmediately(published:)`](/documentation/PSReader/PSEDownloadManager/downloadImmediately(published:)) don’t check the
connection at all.

When the connection drops, the manager pauses the current download, and
resumes it when the connection returns.

Downloads make progress only while your app runs. The manager uses a
standard URL session rather than a background session, so iOS doesn’t
continue a download while the app is suspended. Only completed downloads
persist: a download still queued or running when the app is terminated
doesn’t resume at the next launch, so queue it again.

## Migrating Downloads From the Legacy SDK

A custom UI that replaces the legacy SDK keeps its users’ downloads:
call [`migrateLegacyDownloads(hooks:)`](/documentation/PSReader/PSEDownloadManager/migrateLegacyDownloads(hooks:)) once at
startup. Each migrated entry reports
[`PSEDownloadManager.DownloadState.downloaded`](/documentation/PSReader/PSEDownloadManager/DownloadState/downloaded) and
[`isBridged`](/documentation/PSReader/PSEPublished/isBridged). Open it with [`PSLegacyBridgedEdition`](/documentation/PSReader/PSLegacyBridgedEdition), and
show the source in your reader screen.
[`openEditionSource(onProgress:)`](/documentation/PSReader/PSEPublished/openEditionSource(onProgress:)) can’t open it: it takes
the entry for an ordinary download, which needs files only the bridge
writes.

```swift
PSEDownloadManager.shared.migrateLegacyDownloads()

// Later, wherever your app opens an edition:
let screen = published.isBridged
    ? ReaderScreenViewController(source: try await PSLegacyBridgedEdition.open(published: published))
    : ReaderScreenViewController(published: published)
```

[Keeping Users’ Data](/documentation/PSReader/Migrating-From-the-Legacy-Core-SDK#Keeping-Users-Data) covers when to
call it, what each entry records, and customizing the migration.

## Topics

### Downloading Editions

[`PSEDownloadManager`](/documentation/PSReader/PSEDownloadManager)

Downloads editions for offline reading and manages the stored copies.

[`PSEDownloadObserver`](/documentation/PSReader/PSEDownloadObserver)

Receives download state changes from [`PSEDownloadManager`](/documentation/PSReader/PSEDownloadManager).

### Handling Errors

[`PSDownloadError`](/documentation/PSReader/PSDownloadError)

Reasons a download cannot start under the current connectivity policy.

