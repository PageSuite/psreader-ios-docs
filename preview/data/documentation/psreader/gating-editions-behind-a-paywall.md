<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Gating-Editions-Behind-a-Paywall",
  "metadataVersion" : "0.1.0",
  "role" : "article",
  "title" : "Gating Editions Behind a Paywall"
}
-->

# Gating Editions Behind a Paywall

Check the user’s entitlement before your own screens open or download an edition, and show your paywall when they need one.

## Overview

The prebuilt UI asks a paywall delegate before it opens or downloads an
edition, and shows your paywall screen when the answer is no. The core SDK
has no such hook: [`openEditionSource(onProgress:)`](/documentation/PSReader/PSEPublished/openEditionSource(onProgress:)) and
[`PSEDownloadManager`](/documentation/PSReader/PSEDownloadManager) open and download whatever you ask for. In a custom
UI, you check the user’s entitlement before each of those calls and show
your paywall however you like.

Using the prebuilt UI? See [Paywalls](/documentation/PSReader/Paywalls).

Check before you create your reader screen, `ReaderScreenViewController`
from [Hosting the Reader](/documentation/PSReader/Hosting-the-Reader), since it opens the edition as soon as it
loads:

```swift
// In your edition list's view controller:
func open(_ published: PSEPublished) async {
    guard await SubscriptionManager.shared.requestAccess(from: self) else {
        return
    }

    let reader = UINavigationController(
        rootViewController: ReaderScreenViewController(published: published)
    )
    reader.modalPresentationStyle = .fullScreen
    present(reader, animated: true)
}
```

`SubscriptionManager` stands for your app’s own entitlement check. Its
`requestAccess(from:)` shows your paywall when the user needs one and
returns whether they have access; [Showing Your Paywall](/documentation/PSReader/Gating-Editions-Behind-a-Paywall#Showing-Your-Paywall) sketches
it.

Run the check on every path that opens an edition: your archive, a
“continue reading” list, search results, bookmarks, and links resolved
with [`published(forEditionGUID:)`](/documentation/PSReader/FeedEditionService/published(forEditionGUID:)). Run it before a
download starts, too.

## Showing Your Paywall

Your paywall can be any screen; it doesn’t need to conform to
[`PaywallViewController`](/documentation/PSReader/PaywallViewController). Wrapping it in an `async` method keeps each
check to one line:

```swift
@MainActor
final class SubscriptionManager {
    static let shared = SubscriptionManager()

    private(set) var isSubscribed = false

    /// Returns whether the user has access, showing the paywall first if needed.
    func requestAccess(from presenter: UIViewController) async -> Bool {
        if isSubscribed {
            return true
        }

        return await withCheckedContinuation { continuation in
            let paywall = SubscribeViewController { granted in
                continuation.resume(returning: granted)
            }
            presenter.present(paywall, animated: true)
        }
    }
}
```

The paywall has to report exactly once, however it closes: a
continuation that never resumes leaves the open waiting for good, and one
that resumes twice crashes. Reporting from `viewDidDisappear(_:)` covers
your buttons and a swipe down the sheet in one place:

```swift
final class SubscribeViewController: UIViewController {
    private var onFinish: ((Bool) -> Void)?
    private var didGrantAccess = false

    init(onFinish: @escaping (Bool) -> Void) {
        self.onFinish = onFinish
        super.init(nibName: nil, bundle: nil)
    }

    required init?(coder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }

    @objc func subscribeTapped() {
        // After the purchase or sign-in succeeds:
        didGrantAccess = true
        dismiss(animated: true)
    }

    @objc func notNowTapped() {
        dismiss(animated: true)
    }

    override func viewDidDisappear(_ animated: Bool) {
        super.viewDidDisappear(animated)
        guard isBeingDismissed else {
            return
        }
        onFinish?(didGrantAccess)
        onFinish = nil   // Report once.
    }
}
```

Base `isSubscribed` on entitlement state your app has stored, not on a
network call at the moment of opening. Downloaded editions open offline,
and a check that needs the network would lock the user out of them.

If your app also shows prebuilt screens, the same paywall can serve them
by conforming to [`PaywallViewController`](/documentation/PSReader/PaywallViewController) too; see
[Building the Paywall Screen](/documentation/PSReader/Paywalls#Building-the-Paywall-Screen).

## Deciding per Edition

Supplements and free titles can skip the paywall. Decide before you ask
for access:

```swift
func open(_ published: PSEPublished) async {
    if !isFree(published) {
        guard await SubscriptionManager.shared.requestAccess(from: self) else {
            return
        }
    }

    let reader = UINavigationController(
        rootViewController: ReaderScreenViewController(published: published)
    )
    reader.modalPresentationStyle = .fullScreen
    present(reader, animated: true)
}

func isFree(_ published: PSEPublished) -> Bool {
    published.isSupplement
        || published.applicationGUID == "PUBLICATION_GUID"   // A free title.
}
```

[`applicationGUID`](/documentation/PSReader/PSEPublished/applicationGUID) holds the edition’s publication GUID
(see [Identifiers](/documentation/PSReader/Identifiers)). It’s empty on an edition resolved with
[`published(forEditionGUID:)`](/documentation/PSReader/FeedEditionService/published(forEditionGUID:)), so for search results
and links, decide from the publication GUID they carry, as the sections
below do.

The check also decides whether a lapsed subscriber can still read the
editions they downloaded. To let them, skip it when
[`isDownloaded(published:)`](/documentation/PSReader/PSEDownloadManager/isDownloaded(published:)) is `true`.

## Gating Downloads

Check before a download starts. The download button from
[Adding a Download Button](/documentation/PSReader/Adding-a-Download-Button) also cancels and removes downloads, which
need no check, so ask only when a tap starts one. In `DownloadButton`,
add a property for the check:

```swift
/// Asked before a tap starts a download; returns whether it may start.
var canStartDownload: (() async -> Bool)?
```

And replace its action, so a tap that starts a download waits for the
answer:

```swift
@objc private func toggleDownload() {
    Task {
        switch PSEDownloadManager.shared.state(for: published) {
        case .notDownloaded, .errored, .cancelled, .deleted:
            // This tap starts a download.
            if let canStartDownload, await canStartDownload() == false {
                return
            }
        default:
            // This tap cancels or removes one.
            break
        }

        do {
            // Queues, cancels or deletes, depending on the current state.
            try PSEDownloadManager.shared.toggleDownloadState(for: published)
        } catch {
            onError?(error)
        }
    }
}
```

Then in your reader screen’s `addChrome()`, ask your paywall:

```swift
downloadButton.canStartDownload = { [weak self] in
    guard let self else {
        return false
    }
    return await SubscriptionManager.shared.requestAccess(from: self)
}
```

Set the same check on the buttons in your archive’s cells. To let
everyone read online but keep downloads for subscribers, check here and
not before opening. Anything else that downloads for the user, such as
downloading each new edition as it’s published, needs the same check.

## Gating Search Results

A [`SearchResult`](/documentation/PSReader/SearchResult) names its edition before anything loads: its
[`applicationId`](/documentation/PSReader/SearchResult/applicationId) holds the publication GUID, and
[`editionId`](/documentation/PSReader/SearchResult/editionId) the edition GUID. Check before you resolve the
edition, at the top of the method that opens a result in
[Opening a Result](/documentation/PSReader/Building-a-Search-Screen#Opening-a-Result):

```swift
func open(_ result: SearchResult) async throws {
    if result.applicationId != "PUBLICATION_GUID" {   // A free title.
        guard await SubscriptionManager.shared.requestAccess(from: self) else {
            return
        }
    }

    // Resolve the edition and open it in your reader screen.
}
```

Links work the same way: decide from the publication GUID your link or
notification carries, before you resolve its edition GUID. See
[Routing Links and Notifications](/documentation/PSReader/Opening-an-Edition#Routing-Links-and-Notifications).

## Gating Bookmarks

[`editionSource(mode:among:onProgress:)`](/documentation/PSReader/PSEBookmark/editionSource(mode:among:onProgress:)) opens a bookmark’s
own edition when it can, downloaded or online, which gives the user the
whole edition. Check first, deciding from the bookmark’s
[`published`](/documentation/PSReader/PSEBookmark/published) entry when you need the edition:

```swift
func open(_ bookmark: PSEBookmark) async throws {
    guard await SubscriptionManager.shared.requestAccess(from: self) else {
        return
    }

    let (source, openingPage) = try await bookmark.editionSource()

    let reader = UINavigationController(
        rootViewController: ReaderScreenViewController(source: source, openingPage: openingPage)
    )
    reader.modalPresentationStyle = .fullScreen
    present(reader, animated: true)
}
```

The prebuilt bookmarks screen doesn’t ask the paywall delegate at all. To
let lapsed subscribers keep their saved items without the rest of each
edition, open a bookmarks edition for them instead. It’s built from the
saved content, one page per bookmark, and reads offline:

```swift
let mode: PSEBookmarkOpenMode = SubscriptionManager.shared.isSubscribed
    ? .preferSourceEdition
    : .alwaysBookmarksEdition
let (source, openingPage) = try await bookmark.editionSource(mode: mode)
```