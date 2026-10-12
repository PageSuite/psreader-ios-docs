<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Presenting-the-Prebuilt-Reader",
  "metadataVersion" : "0.1.0",
  "role" : "collectionGroup",
  "title" : "Presenting the Prebuilt Reader"
}
-->

# Presenting the Prebuilt Reader

Open an edition in the prebuilt reader from your own interface: a button, a deep link, or a push notification.

## Overview

[`FeedReaderViewController`](/documentation/PSReader/FeedReaderViewController) opens one edition in the full prebuilt reader
screen, with its navigation bar, content browser, settings, and a close
button. It works with every edition on PageSuite’s current system,
classic PDF and responsive alike. Create it from what you know about the
edition, then present it full screen:

```swift
let reader = FeedReaderViewController(
    globalConfig: globalConfig,
    latestEditionForPublication: "PUBLICATION_GUID"
)
reader.modalPresentationStyle = .fullScreen
present(reader, animated: true)
```

The reader shows a splash screen while the edition loads, asks your
[`PaywallDelegate`](/documentation/PSReader/PaywallDelegate) before opening it, and reports the same analytics
events as a reader opened from the carousel.

This is how a prebuilt app handles deep links and push notifications:
whether the app is built on the carousel or on your own screens, open the
edition a link names in this reader.
[Routing Links and Notifications](/documentation/PSReader/Presenting-the-Prebuilt-Reader#Routing-Links-and-Notifications) shows the whole flow.
An app with a custom UI can open editions here too; see
[Mixing Prebuilt and Custom UI](/documentation/PSReader/Choosing-an-Integration#Mixing-Prebuilt-and-Custom-UI).

## Choosing an Initializer

Each initializer starts from a different piece of information, the most
common first:

|You have                                                                                                                                                               |Initializer                                                                                                                                                                              |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|A publication GUID, and want its latest edition                                                                                                                        |``doc://com.pagesuite.PSReader/documentation/PSReader/FeedReaderViewController/init(globalConfig:readerConfig:latestEditionForPublication:publicationName:publishedDomain:openingPage:)``|
|A shortcode and an edition GUID, as in a deep link                                                                                                                     |``doc://com.pagesuite.PSReader/documentation/PSReader/FeedReaderViewController/init(globalConfig:readerConfig:shortcode:editionGUID:openingPage:)``                                      |
|A publication GUID and an edition GUID                                                                                                                                 |``doc://com.pagesuite.PSReader/documentation/PSReader/FeedReaderViewController/init(globalConfig:readerConfig:publicationGUID:publicationName:editionGUID:publishedDomain:openingPage:)``|
|A ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPublished`` from ``doc://com.pagesuite.PSReader/documentation/PSReader/FeedEditionService`` or your own list|``doc://com.pagesuite.PSReader/documentation/PSReader/FeedReaderViewController/init(globalConfig:readerConfig:published:openingPage:)``                                                  |

The optional `publicationName` becomes the edition’s
[`publicationName`](/documentation/PSReader/PSEPublished/publicationName), which the reader’s analytics events
carry. Leave `publishedDomain` at its default unless PageSuite gives you
another.

## Setting the App Configuration

A few reader features read your app configuration from PageSuite,
in-article adverts among them. The shortcode initializer loads it for its
reader, as a dynamic archive does in the carousel. The other initializers
take it from [`remoteConfig`](/documentation/PSReader/GlobalConfiguration/remoteConfig) on the `globalConfig`
you pass. They never read it from a [`ReaderConfiguration`](/documentation/PSReader/ReaderConfiguration), which has no
app configuration of its own. So if your editions use those features,
load the configuration with [`AppConfigService`](/documentation/PSReader/AppConfigService) and set it on the global
configuration. You
don’t need to set [`baseURL`](/documentation/PSReader/ReaderConfiguration/baseURL) as well: with the app
configuration, the reader falls back to its advert domain and edition
base URL for pages that don’t carry their own.

```swift
var globalConfig = GlobalConfiguration(apiKey: "API_KEY", accountGUID: "ACCOUNT_GUID")
globalConfig.remoteConfig = try? await AppConfigService().configuration(forShortcode: "SHORTCODE")

let reader = FeedReaderViewController(
    globalConfig: globalConfig,
    latestEditionForPublication: "PUBLICATION_GUID"
)
```

Load it once, early in your app’s launch, and create every reader from
the global configuration you set it on: a reader keeps the value it had
when you created it. That holds in a carousel app too. The configuration
a dynamic archive loads stays with the carousel’s own screens, so a reader
you open here has it only if you set it or use the shortcode initializer.
[The App Configuration](/documentation/PSReader/Configuring-the-Prebuilt-UI#The-App-Configuration) lists the
features that need it.

## Opening an Edition From a Link

A deep link or a notification usually names an edition by its GUID. With
your app’s shortcode, that’s all the reader needs:

```swift
let reader = FeedReaderViewController(
    globalConfig: globalConfig,
    shortcode: "SHORTCODE",
    editionGUID: "EDITION_GUID"
)
reader.modalPresentationStyle = .fullScreen
present(reader, animated: true)
```

The reader loads the app configuration for the shortcode, searches the
publications it names for the edition, and keeps the configuration for
the features that read it. When [`remoteConfig`](/documentation/PSReader/GlobalConfiguration/remoteConfig) is
already the configuration for that shortcode, the reader uses it instead
of loading it again.

If the link carries the publication GUID too, open the edition from both:

```swift
let reader = FeedReaderViewController(
    globalConfig: globalConfig,
    publicationGUID: "PUBLICATION_GUID",
    editionGUID: "EDITION_GUID"
)
```

The reader looks the edition up first, and finds editions older than the
publication’s archive listing too. It takes the app configuration from
your global configuration; see [Setting the App Configuration](/documentation/PSReader/Presenting-the-Prebuilt-Reader#Setting-the-App-Configuration).

### Routing Links and Notifications

The payload and URL formats are your own: put the edition GUID in them,
and a page GUID when you want a specific page. This scene delegate reads a
link such as `yourapp://edition/EDITION_GUID?page=PAGE_GUID`:

```swift
func scene(_ scene: UIScene, openURLContexts URLContexts: Set<UIOpenURLContext>) {
    guard let url = URLContexts.first?.url,
          url.scheme == "yourapp",
          url.host == "edition",
          let editionGUID = url.pathComponents.dropFirst().first else { return }

    let pageGUID = URLComponents(url: url, resolvingAgainstBaseURL: false)?
        .queryItems?.first(where: { $0.name == "page" })?.value

    openEdition(editionGUID: editionGUID, pageGUID: pageGUID)
}

func openEdition(editionGUID: String, pageGUID: String?) {
    let reader = FeedReaderViewController(
        globalConfig: globalConfig,
        shortcode: "SHORTCODE",
        editionGUID: editionGUID,
        openingPage: pageGUID.map { .page(guid: $0) }
    )
    reader.modalPresentationStyle = .fullScreen
    window?.rootViewController?.present(reader, animated: true)
}
```

A link that launches your app arrives in `scene(_:willConnectTo:options:)`
instead. Once the window is set up there, pass it on with
`self.scene(scene, openURLContexts: connectionOptions.urlContexts)`.

A push notification arrives in your `UNUserNotificationCenter` delegate,
here the app delegate, with whatever keys your payload uses:

```swift
func userNotificationCenter(
    _ center: UNUserNotificationCenter,
    didReceive response: UNNotificationResponse,
    withCompletionHandler completionHandler: @escaping () -> Void
) {
    let userInfo = response.notification.request.content.userInfo

    if let editionGUID = userInfo["editionGUID"] as? String,
       let sceneDelegate = response.targetScene?.delegate as? SceneDelegate {
        sceneDelegate.openEdition(editionGUID: editionGUID, pageGUID: userInfo["pageGUID"] as? String)
    }

    completionHandler()
}
```

Send page GUIDs rather than printed labels such as “A3”: the reader’s
[`FeedReaderViewController.OpeningPage`](/documentation/PSReader/FeedReaderViewController/OpeningPage) takes GUIDs only.

Search results carry the same two identifiers. To open a result from a
search screen of your own, see
[Opening Results in the Prebuilt Reader](/documentation/PSReader/Building-a-Search-Screen#Opening-Results-in-the-Prebuilt-Reader);
the prebuilt search screens open their results themselves.

## Opening an Edition You Fetched

An edition you already fetched, from [`FeedEditionService`](/documentation/PSReader/FeedEditionService) or a list of
your own, opens without another request for it:

```swift
let service = FeedEditionService(accountGUID: "ACCOUNT_GUID")
let published = try await service.latestEdition(publicationGUID: "PUBLICATION_GUID")

let reader = FeedReaderViewController(globalConfig: globalConfig, published: published)
```

### Listing Editions Yourself

A list of your own needs only the catalog, a label for each row, and the
reader. This screen lists a publication’s editions, newest first, labels
each with the date the prebuilt screens show for it, and opens the one
the user taps:

```swift
final class EditionListViewController: UITableViewController {

    private let globalConfig: GlobalConfiguration
    private let service: FeedEditionService
    private var editions: [PSEPublished] = []

    init(globalConfig: GlobalConfiguration) {
        self.globalConfig = globalConfig
        self.service = FeedEditionService(accountGUID: globalConfig.accountGUID)
        super.init(style: .insetGrouped)
    }

    required init?(coder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }

    override func viewDidLoad() {
        super.viewDidLoad()
        tableView.register(UITableViewCell.self, forCellReuseIdentifier: "Edition")

        Task {
            do {
                // Grouped by publishing date, newest first. The name goes
                // on each edition, for the reader's analytics events.
                let dates = try await service.publishedEditions(
                    publicationGUID: "PUBLICATION_GUID",
                    publicationName: "The Daily"
                )
                editions = dates.flatMap { $0.editions ?? [] }
                tableView.reloadData()
            } catch {
                showMessage("Couldn't load the editions.")
            }
        }
    }

    override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        editions.count
    }

    override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell = tableView.dequeueReusableCell(withIdentifier: "Edition", for: indexPath)

        var content = cell.defaultContentConfiguration()
        content.text = globalConfig.dateFormatter.string(for: editions[indexPath.row])
        cell.contentConfiguration = content

        return cell
    }

    override func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
        tableView.deselectRow(at: indexPath, animated: true)

        let reader = FeedReaderViewController(globalConfig: globalConfig, published: editions[indexPath.row])
        reader.modalPresentationStyle = .fullScreen
        present(reader, animated: true)
    }
}
```

`showMessage(_:)` stands for your own alert. The date formatter is the
global configuration’s [`dateFormatter`](/documentation/PSReader/GlobalConfiguration/dateFormatter), so the
rows match the prebuilt screens; [Date Formatting](/documentation/PSReader/Theming#Date-Formatting) covers
changing it. For covers, errors, and listing one month at a time, see
[Fetching the Archive](/documentation/PSReader/Fetching-the-Archive); the sample app’s list, in
[Building a Reader App](/documentation/PSReader/Building-a-Reader-App), shows covers too.

## Choosing the Opening Page

Without an opening page, the reader reopens each edition on the page last
viewed on this device, or on the first page the first time. Pass an
[`FeedReaderViewController.OpeningPage`](/documentation/PSReader/FeedReaderViewController/OpeningPage) to choose the page instead; it
overrides the saved one:

```swift
// A specific page, by its pageguid.
let reader = FeedReaderViewController(
    globalConfig: globalConfig,
    publicationGUID: "PUBLICATION_GUID",
    editionGUID: "EDITION_GUID",
    openingPage: .page(guid: "PAGE_GUID")
)
```

`.section(guid:)` takes the `sectionguid` of one of the edition’s
[`sections`](/documentation/PSReader/PSEEdition/sections) and opens on the first article page in that
section.

### Adding a Continue Reading Button

The reader already resumes each edition where the user left it. For a
“Continue reading” button, remember which edition the user last viewed.
The prebuilt UI’s analytics events report every page view:

```swift
final class LastEditionTracker: EventSubscriber {
    private(set) var lastEditionGUID = UserDefaults.standard.string(forKey: "lastEditionGUID")

    func analytics(event: EventChannel.AnalyticsEvent) {
        switch event {
        case .feedEditionArticleView(let context),
             .feedEditionSectionView(let context),
             .feedEditionReplicaView(let context),
             .feedEditionOtherPageView(let context):
            guard let editionGUID = context.published?.editionGUID else { return }
            lastEditionGUID = editionGUID
            UserDefaults.standard.set(editionGUID, forKey: "lastEditionGUID")
        default:
            break
        }
    }
}

let tracker = LastEditionTracker()   // Keep a strong reference.
EventChannel.shared.subscribe(tracker)
```

Then open that edition without an opening page, and the reader picks up
the page itself:

```swift
@objc func continueReadingTapped() {
    guard let editionGUID = tracker.lastEditionGUID else { return }

    let reader = FeedReaderViewController(
        globalConfig: globalConfig,
        shortcode: "SHORTCODE",
        editionGUID: editionGUID
    )
    reader.modalPresentationStyle = .fullScreen
    present(reader, animated: true)
}
```

Show the button only when there’s an edition to continue, and refresh it
in `viewWillAppear(_:)` of the screen that shows it. The reader is
presented full screen, so that runs again when the user closes the
reader, after the tracker has recorded what they read:

```swift
override func viewWillAppear(_ animated: Bool) {
    super.viewWillAppear(animated)
    continueReadingButton.isHidden = tracker.lastEditionGUID == nil
}
```

Saved positions stay on the device; the reader doesn’t sync them between
devices.

## Presenting the Reader

[`FeedReaderViewController`](/documentation/PSReader/FeedReaderViewController) doesn’t set a modal presentation style, so a
plain `present(_:animated:completion:)` shows it as a sheet. Set
`.fullScreen` before presenting it. Its close button dismisses it, so
present it rather than pushing it onto a navigation stack:

```swift
reader.modalPresentationStyle = .fullScreen
present(reader, animated: true)
```

To open an edition over the carousel, present the reader from the
carousel or the view controller that hosts it.

Pass a [`ReaderConfiguration`](/documentation/PSReader/ReaderConfiguration) as `readerConfig` to change the reader’s
navigation bar, settings, and the rest; without one, the reader takes
everything from your global configuration. See
[Customizing the Reader Screen](/documentation/PSReader/Customizing-the-Reader-Screen).

> Replica: ``doc://com.pagesuite.PSReader/documentation/PSReader/FeedReaderViewController`` opens editions on the current
> system only. Editions on the legacy replica system open from a replica
> archive, in the carousel or an ``doc://com.pagesuite.PSReader/documentation/PSReader/ArchiveViewController``. See
> <doc://com.pagesuite.PSReader/documentation/PSReader/Edition-Platforms>.

## Topics

### The Prebuilt Reader

[`FeedReaderViewController`](/documentation/PSReader/FeedReaderViewController)

A standalone view controller for displaying an edition on PageSuite’s
current system, classic PDF or responsive.

