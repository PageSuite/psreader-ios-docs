<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Paywalls",
  "metadataVersion" : "0.1.0",
  "role" : "collectionGroup",
  "title" : "Paywalls"
}
-->

# Paywalls

Gate editions in the prebuilt UI behind your own subscription check and paywall screen.

## Overview

The SDK doesn’t restrict any content by itself. Give the prebuilt UI a
[`PaywallDelegate`](/documentation/PSReader/PaywallDelegate), and it asks the delegate before it opens an edition,
downloads one, or opens a search result. The delegate returns `nil` to
let the action through, or your paywall screen, which the SDK presents;
the action goes ahead only if the screen reports that the user got
access. Building a custom UI? See [Gating Editions Behind a Paywall](/documentation/PSReader/Gating-Editions-Behind-a-Paywall).

Set the delegate on the global configuration before you create any other
configuration or screen:

```swift
var globalConfig = GlobalConfiguration(apiKey: "API_KEY", accountGUID: "ACCOUNT_GUID")
globalConfig.paywallDelegate = AppPaywallDelegate()
```

![A sample paywall presented over the reader.](images/com.pagesuite.PSReader/paywall-over-reader~dark@2x.png)

A delegate that sends everyone without a subscription to the same
paywall:

```swift
import PSReader
import UIKit

struct AppPaywallDelegate: PaywallDelegate {

    func paywallViewControllerForAction(
        openFeedEdition published: PSEPublished
    ) -> PaywallViewController? {
        SubscriptionManager.shared.isSubscribed ? nil : SubscribeViewController()
    }

    func paywallViewControllerForAction(
        openSearchResult result: SearchResult
    ) -> PaywallViewController? {
        SubscriptionManager.shared.isSubscribed ? nil : SubscribeViewController()
    }

    // Required by the protocol, but asked only for legacy replica editions.
    func paywallViewControllerForAction(
        openReplicaEdition edition: PSEdition
    ) -> PaywallViewController? {
        SubscriptionManager.shared.isSubscribed ? nil : SubscribeViewController()
    }
}
```

`SubscriptionManager` stands for your app’s own entitlement check, and
`SubscribeViewController` is your paywall screen (see
[Building the Paywall Screen](/documentation/PSReader/Paywalls#Building-the-Paywall-Screen)). Search results have a method of
their own, because they open the edition without asking the open method
(see [Gating Search Results](/documentation/PSReader/Paywalls#Gating-Search-Results)). Downloads get the open method’s
answer unless you implement theirs (see
[Gating Downloads Separately](/documentation/PSReader/Paywalls#Gating-Downloads-Separately)). The replica method, which receives
a [`PSEdition`](/documentation/PSReader/PSEdition), the legacy replica system’s edition model, is a protocol
requirement even in an app without legacy replica editions; giving it the
same check keeps the delegate safe either way.

## Building the Paywall Screen

Your paywall screen is a view controller that conforms to
[`PaywallViewController`](/documentation/PSReader/PaywallViewController). Its one requirement,
[`onDismiss`](/documentation/PSReader/PaywallViewController/onDismiss), is a closure the SDK sets just before
it presents the screen. The SDK holds the action until you call it: pass
`true` when the user subscribed or signed in, and the edition opens or
downloads; pass `false`, and the action is dropped. The user stays where
they were, except that a [`FeedReaderViewController`](/documentation/PSReader/FeedReaderViewController) waiting on the
paywall closes.

`onDismiss` reports a decision; it doesn’t dismiss anything. Dismiss your
screen yourself, then call `onDismiss` exactly once:

```swift
final class SubscribeViewController: UIViewController, PaywallViewController {
    var onDismiss: ((Bool) -> Void)?

    @objc func subscribeTapped() {
        // After the purchase or sign-in succeeds:
        dismiss(animated: true) {
            self.onDismiss?(true)
        }
    }

    @objc func notNowTapped() {
        dismiss(animated: true) {
            self.onDismiss?(false)
        }
    }
}
```

The SDK presents your screen modally, from the screen the user is on or
from the reader’s splash screen, and doesn’t set a presentation style.
Set `modalPresentationStyle` on your view controller to change UIKit’s
default sheet.

### Dismissing the Paywall

UIKit’s default sheet can be swiped away, and that path has to call
`onDismiss` too, or the SDK keeps waiting. Calling it from
`viewDidDisappear(_:)` covers your buttons and the swipe in one place:

```swift
final class SubscribeViewController: UIViewController, PaywallViewController {
    var onDismiss: ((Bool) -> Void)?

    private var didGrantAccess = false

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
        guard isBeingDismissed else { return }
        onDismiss?(didGrantAccess)
        onDismiss = nil   // Report once.
    }
}
```

To rule out the swipe instead, set `isModalInPresentation = true` and
leave your buttons as the only way out.

> Warning: Do both halves. Calling `onDismiss` without dismissing leaves
> your paywall on screen while the SDK moves on. Dismissing without
> calling `onDismiss` leaves the SDK waiting, and the edition never
> opens.

## Deciding Who Sees a Paywall

Return `nil` for anything the user may open. The delegate receives the
edition’s [`PSEPublished`](/documentation/PSReader/PSEPublished), so the answer can depend on the edition:

```swift
func paywallViewControllerForAction(
    openFeedEdition published: PSEPublished
) -> PaywallViewController? {
    if SubscriptionManager.shared.isSubscribed { return nil }
    if published.isSupplement { return nil }
    if published.applicationGUID == "PUBLICATION_GUID" { return nil }   // a free title

    return SubscribeViewController()
}
```

[`applicationGUID`](/documentation/PSReader/PSEPublished/applicationGUID) holds the edition’s publication GUID;
see [Identifiers](/documentation/PSReader/Identifiers).

The SDK calls the delegate on the main actor and uses the answer at
once, so read the entitlement from state your app already holds. If the
decision needs a network call, make it inside your paywall screen and
report the result through `onDismiss`.

## Gating Search Results

[`paywallViewControllerForAction(openSearchResult:)`](/documentation/PSReader/PaywallDelegate/paywallViewControllerForAction(openSearchResult:))
returns `nil` unless you implement it, and the SDK opens a search result’s
edition without asking
[`paywallViewControllerForAction(openFeedEdition:)`](/documentation/PSReader/PaywallDelegate/paywallViewControllerForAction(openFeedEdition:)). If
your editions are paywalled, implement it too. The result identifies the
edition before anything loads: [`applicationId`](/documentation/PSReader/SearchResult/applicationId) holds its
publication GUID and [`editionId`](/documentation/PSReader/SearchResult/editionId) its edition GUID.

```swift
func paywallViewControllerForAction(
    openSearchResult result: SearchResult
) -> PaywallViewController? {
    if SubscriptionManager.shared.isSubscribed { return nil }
    if result.applicationId == "PUBLICATION_GUID" { return nil }   // a free title

    return SubscribeViewController()
}
```

A [`FeedReaderViewController`](/documentation/PSReader/FeedReaderViewController) you open from a result yourself asks the
open method as usual. [Where the Prebuilt UI Asks](/documentation/PSReader/Paywalls#Where-the-Prebuilt-UI-Asks) says which
delegate the search screen asks, and [Search](/documentation/PSReader/Search) covers the search
screens themselves.

> Replica: Results from replica editions don’t use this method. The
> replica reader asks
> ``doc://com.pagesuite.PSReader/documentation/PSReader/PaywallDelegate/paywallViewControllerForAction(openReplicaEdition:)``
> when it has loaded the edition.

## Gating Downloads Separately

The same paywall covers opening and downloading until you implement
[`paywallViewControllerForAction(downloadFeedEdition:)`](/documentation/PSReader/PaywallDelegate/paywallViewControllerForAction(downloadFeedEdition:)).
To let everyone read online but keep downloads for subscribers:

```swift
struct DownloadPaywallDelegate: PaywallDelegate {

    func paywallViewControllerForAction(
        openFeedEdition published: PSEPublished
    ) -> PaywallViewController? {
        nil
    }

    func paywallViewControllerForAction(
        downloadFeedEdition published: PSEPublished
    ) -> PaywallViewController? {
        SubscriptionManager.shared.isSubscribed ? nil : SubscribeViewController()
    }

    // Required by the protocol, but asked only for legacy replica editions.
    func paywallViewControllerForAction(
        openReplicaEdition edition: PSEdition
    ) -> PaywallViewController? {
        nil
    }
}
```

An archive’s download button asks on every tap, including the taps that
cancel a download in progress and delete a downloaded edition.

The reader’s “Download while reading” setting skips the download methods.
While it’s on, the reader downloads each edition it opens once the open
check passes, and switching it on downloads the edition being read. The
reader shows the setting in its settings menu and asks about it the first
time it opens. To keep downloads for subscribers, remove both the menu row
and the question in every reader configuration you use, including each
carousel section’s [`readerConfig`](/documentation/PSReader/ArchiveConfiguration/readerConfig):

```swift
readerConfig.settings.isDownloadWhileReadingToggleEnabled = false
readerConfig.settings.isDownloadWhileReadingPreferenceAlertEnabled = false
```

Removing the row doesn’t undo a choice the user already made: if they
switched the setting on before, it stays on. See
[Download Settings in the Prebuilt Reader](/documentation/PSReader/Downloads-and-Offline-Reading#Download-Settings-in-the-Prebuilt-Reader)
for the reader’s other download settings.

## Opening Editions Free

To exempt a carousel section or one screen, clear the delegate in the
configuration it opens editions with:

```swift
// A carousel section whose editions open free
var freeConfig = ArchiveConfiguration(globalConfig: globalConfig)
freeConfig.readerConfig.paywallDelegate = nil

let carousel = CarouselViewController(
    globalConfig: globalConfig,
    sections: [
        .dynamicArchive("Editions", shortcode: "SHORTCODE"),
        .section(.init(
            name: "Free",
            type: .feedArchive(guid: "PUBLICATION_GUID", config: freeConfig)
        )),
    ]
)

// A "Read a free sample" button
var sampleConfig = ReaderConfiguration(globalConfig: globalConfig)
sampleConfig.paywallDelegate = nil

let reader = FeedReaderViewController(
    globalConfig: globalConfig,
    readerConfig: sampleConfig,
    latestEditionForPublication: "PUBLICATION_GUID"
)
reader.modalPresentationStyle = .fullScreen
present(reader, animated: true)
```

## Where the Prebuilt UI Asks

Each screen asks the delegate in the [`ReaderConfiguration`](/documentation/PSReader/ReaderConfiguration) it opens
editions with, whether the carousel shows the screen or you do. That
configuration copies [`paywallDelegate`](/documentation/PSReader/GlobalConfiguration/paywallDelegate) when it’s
created, which is why the global delegate comes first (see
[Configuring the Prebuilt UI](/documentation/PSReader/Configuring-the-Prebuilt-UI)).

- **Archives.** ``doc://com.pagesuite.PSReader/documentation/PSReader/ArchiveViewController`` and the carousel’s archive and
  kiosk sections ask before they open an edition and when the user taps a
  download button, using ``doc://com.pagesuite.PSReader/documentation/PSReader/ArchiveConfiguration/readerConfig``.
- **The reader.** ``doc://com.pagesuite.PSReader/documentation/PSReader/FeedReaderViewController`` asks by itself once it has
  looked the edition up, presenting your paywall over its splash screen.
  If the user doesn’t get access, the reader dismisses itself.
- **Search.** ``doc://com.pagesuite.PSReader/documentation/PSReader/SearchViewController`` asks before it opens a result,
  using the reader configuration your ``doc://com.pagesuite.PSReader/documentation/PSReader/SearchDelegate`` returns for the
  result’s publication. For ``doc://com.pagesuite.PSReader/documentation/PSReader/ApplicationSearchDelegate``, that’s the
  `readerConfig` you created it with. The carousel’s search uses the
  reader configuration of the section that lists the result’s
  publication.
- **Bookmarks and downloads.** ``doc://com.pagesuite.PSReader/documentation/PSReader/BookmarksViewController``,
  ``doc://com.pagesuite.PSReader/documentation/PSReader/DownloadsViewController``, and the carousel’s bookmarks and downloads
  sections open editions without asking.

The carousel doesn’t read [`paywallDelegate`](/documentation/PSReader/CarouselConfiguration/paywallDelegate); set
the delegate on the global configuration or on a section’s reader
configuration.

> Replica: Replica editions ask
> ``doc://com.pagesuite.PSReader/documentation/PSReader/PaywallDelegate/paywallViewControllerForAction(openReplicaEdition:)``
> to open and
> ``doc://com.pagesuite.PSReader/documentation/PSReader/PaywallDelegate/paywallViewControllerForAction(downloadReplicaEdition:)``
> to download; the download method returns the open method’s answer
> unless you implement it. Both receive the legacy `PSEdition` instead of
> a ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPublished``.

## Complete Example

A paywall screen, a delegate, and a carousel that uses them:

```swift
import PSReader
import UIKit

// 1. The paywall screen
final class SubscribeViewController: UIViewController, PaywallViewController {
    var onDismiss: ((Bool) -> Void)?

    private var didGrantAccess = false

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
        guard isBeingDismissed else { return }
        onDismiss?(didGrantAccess)
        onDismiss = nil
    }
}

// 2. The delegate
struct AppPaywallDelegate: PaywallDelegate {
    let subscriptions: SubscriptionManager

    func paywallViewControllerForAction(
        openFeedEdition published: PSEPublished
    ) -> PaywallViewController? {
        if subscriptions.isSubscribed || published.isSupplement { return nil }
        return SubscribeViewController()
    }

    func paywallViewControllerForAction(
        openSearchResult result: SearchResult
    ) -> PaywallViewController? {
        subscriptions.isSubscribed ? nil : SubscribeViewController()
    }

    // Required by the protocol, but asked only for legacy replica editions.
    func paywallViewControllerForAction(
        openReplicaEdition edition: PSEdition
    ) -> PaywallViewController? {
        subscriptions.isSubscribed ? nil : SubscribeViewController()
    }
}

// 3. The carousel, with the delegate on the global configuration
@MainActor
func makeCarousel() -> CarouselViewController {
    var globalConfig = GlobalConfiguration(apiKey: "API_KEY", accountGUID: "ACCOUNT_GUID")
    globalConfig.paywallDelegate = AppPaywallDelegate(subscriptions: .shared)

    return CarouselViewController(
        globalConfig: globalConfig,
        sections: [
            .dynamicArchive("Editions", shortcode: "SHORTCODE"),
        ]
    )
}
```

## Troubleshooting

**The paywall closes, but the edition never opens.**
`onDismiss` never ran, usually because the user swiped the sheet away.
The SDK holds the action until the closure runs. Call it from
`viewDidDisappear(_:)`, as in [Dismissing the Paywall](/documentation/PSReader/Paywalls#Dismissing-the-Paywall).

**Access is granted, but the reader doesn’t open, or opens over the
paywall.**
`onDismiss(true)` ran while the paywall was still on screen: either you
never dismissed it, or you called the closure before the dismissal
finished. The SDK goes ahead the moment the closure runs and presents the
reader from the screen that’s showing your paywall. Depending on the
screen, the reader then fails to appear, or appears over the paywall,
which shows again when the reader closes. Call `onDismiss` from the
`dismiss(animated:completion:)` completion handler or from
`viewDidDisappear(_:)`.

**A section or screen shows the wrong paywall, or none.**
Each screen asks the delegate in its own [`ReaderConfiguration`](/documentation/PSReader/ReaderConfiguration), copied
from the global configuration when that configuration was created. Check
that you set [`paywallDelegate`](/documentation/PSReader/GlobalConfiguration/paywallDelegate) before creating
archive, reader, and search configurations, and look for a screen or
section that overrides it.

**Search results open without a paywall.**
Implement
[`paywallViewControllerForAction(openSearchResult:)`](/documentation/PSReader/PaywallDelegate/paywallViewControllerForAction(openSearchResult:)); see
[Gating Search Results](/documentation/PSReader/Paywalls#Gating-Search-Results).

**Editions download without the download paywall.**
“Download while reading” downloads opened editions without asking; see
[Gating Downloads Separately](/documentation/PSReader/Paywalls#Gating-Downloads-Separately).

## Topics

### Paywall Delegate

[`PaywallDelegate`](/documentation/PSReader/PaywallDelegate)

A delegate protocol used to provide paywall view controllers for controlling
access to premium content within the SDK.

### Paywall Screen

[`PaywallViewController`](/documentation/PSReader/PaywallViewController)

A view controller protocol used by the SDK to present paywalls when
accessing restricted content.

