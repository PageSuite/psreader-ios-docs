<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Setting-Up-the-Carousel",
  "metadataVersion" : "0.1.0",
  "role" : "collectionGroup",
  "title" : "Setting Up the Carousel"
}
-->

# Setting Up the Carousel

Show the whole prebuilt UI from one view controller: your publications’ archives, bookmarks, downloads, and search.

## Overview

[`CarouselViewController`](/documentation/PSReader/CarouselViewController) is the SDK’s whole reader app in one view
controller. Give it a [`GlobalConfiguration`](/documentation/PSReader/GlobalConfiguration) and a list of sections. Each
section is a tab in the section ribbon along the top; a section with
subsections adds a second ribbon of pills beneath it. Editions open in the
prebuilt reader.

```swift
import PSReader
import UIKit

let globalConfig = GlobalConfiguration(
    apiKey: "API_KEY",
    accountGUID: "ACCOUNT_GUID",
    primaryFont: UIFont(name: "Georgia", size: 12)!,
    secondaryFont: .systemFont(ofSize: 12),
    brandColor: .systemBlue
)

let carousel = CarouselViewController(
    globalConfig: globalConfig,
    sections: [
        .dynamicArchive("Editions", shortcode: "SHORTCODE"),
        .subsections("My Content", [
            .init(name: "Bookmarks", type: .bookmarks(type: .all)),
            .init(name: "Downloads", type: .downloads(type: .all))
        ])
    ]
)
```

**iPhone:**

![The carousel showing a dynamic archive: the section ribbon, subsection pills, and a grid of edition covers, with callouts for the ribbons and header.](images/com.pagesuite.PSReader/carousel-dynamic-archive-annotated~dark@2x.png)

**iPad:**

![The carousel showing a dynamic archive: the section ribbon, subsection pills, and a grid of edition covers, with callouts for the ribbons and header.](images/com.pagesuite.PSReader/carousel-dynamic-archive-ipad-annotated@2x.png)

The fonts and brand color style every screen the carousel shows; see
[Theming](/documentation/PSReader/Theming). The carousel relies on the call to
[`initialize(apiKey:completion:)`](/documentation/PSReader/initialize(apiKey:completion:)) your app makes at launch; see
[Initialize the SDK](/documentation/PSReader/Getting-Started#Initialize-the-SDK).

To place the archive, bookmarks, downloads, and search screens in your
own navigation instead of the carousel’s, see
[Embedding Prebuilt Screens](/documentation/PSReader/Embedding-Prebuilt-Screens).

## Showing the Carousel

The carousel is a plain view controller. Make it your window’s root view
controller, one tab of your tab bar controller, or a child of one of your
screens:

**UIKit:**

```swift
// Your window's root view controller, when your scene connects.
window.rootViewController = carousel

// One tab of your tab bar controller.
carousel.tabBarItem = UITabBarItem(title: "Editions", image: UIImage(systemName: "newspaper"), tag: 0)
tabBarController.viewControllers = [carousel, accountViewController]

// A child of one of your screens, filling its view.
addChild(carousel)
carousel.view.frame = view.bounds
carousel.view.autoresizingMask = [.flexibleWidth, .flexibleHeight]
view.addSubview(carousel.view)
carousel.didMove(toParent: self)
```

`accountViewController` stands for a screen of your own.

**SwiftUI:**

Wrap the carousel in a `UIViewControllerRepresentable`, then use
it like any other view, such as one tab of a `TabView`:

```swift
import PSReader
import SwiftUI

struct CarouselView: UIViewControllerRepresentable {
    let globalConfig: GlobalConfiguration

    func makeUIViewController(context: Context) -> CarouselViewController {
        CarouselViewController(
            globalConfig: globalConfig,
            sections: [.dynamicArchive("Editions", shortcode: "SHORTCODE")]
        )
    }

    func updateUIViewController(_ carousel: CarouselViewController, context: Context) {}
}
```

Delegates that need your app’s state fit best on the
representable’s coordinator; see
[Embedding a Screen](/documentation/PSReader/Embedding-Prebuilt-Screens#Embedding-a-Screen).

To present the carousel over your app instead, give it a close button;
see [Presenting the Carousel Modally](/documentation/PSReader/Setting-Up-the-Carousel#Presenting-the-Carousel-Modally).

## Loading Sections From a Shortcode

A dynamic archive, `.dynamicArchive(_:shortcode:config:)`, is the simplest
section. The SDK loads the app configuration that the shortcode names in
PageSuite and builds the section from it:

- Each archive in the configuration becomes a subsection named after it.
  With a single archive, the section has no subsection ribbon.
- An archive with the kiosk layout becomes a grid of its publications;
  tapping one opens that publication’s archive.
- Each publication shows the right way for its system, PageSuite’s
  current system or the legacy replica system, without you telling it
  which. See <doc://com.pagesuite.PSReader/documentation/PSReader/Edition-Platforms>.
- Publications that PageSuite configures with a date picker get one,
  starting from the archive’s configured start date.

**iPhone:**

![An edition archive with its date picker open on a month.](images/com.pagesuite.PSReader/archive-date-picker@2x.png)

**iPad:**

![An edition archive with its date picker open on a month.](images/com.pagesuite.PSReader/archive-date-picker-ipad@2x.png)

The configuration reaches the rest of the carousel too. Every reader the
carousel opens, from bookmarks, downloads, and search included, gets its
advert, widget, and logo settings, and readers opened from an archive get
the base URL their templated pages load from. That’s why a shortcode is
the recommended way to start: the carousel needs no app configuration
from you (see [The App Configuration](/documentation/PSReader/Configuring-the-Prebuilt-UI#The-App-Configuration)).
Readers you open yourself with [`FeedReaderViewController`](/documentation/PSReader/FeedReaderViewController) don’t share
the carousel’s; see
[Setting the App Configuration](/documentation/PSReader/Presenting-the-Prebuilt-Reader#Setting-the-App-Configuration).

Pass an [`ArchiveConfiguration`](/documentation/PSReader/ArchiveConfiguration) as `config` to style every archive in the
section. A few of its values come from PageSuite instead, such as the
archive limit; [Dynamic Archives](/documentation/PSReader/Configuring-the-Prebuilt-UI#Dynamic-Archives) lists them.

When the configuration changes in PageSuite, call
[`refreshDynamicArchives(completion:)`](/documentation/PSReader/CarouselViewController/refreshDynamicArchives(completion:)) to load it
again, for example when your app returns to the foreground. Sections you
define yourself aren’t affected.

## Defining Sections Yourself

To choose exactly what each tab shows, build sections from content types
instead. A `.section` is a tab with one screen; a `.subsections` group is a
tab with a subsection ribbon that switches between several:

```swift
let sections: [CarouselViewController.SectionItem] = [
    .section(.init(name: "Today", type: .feedArchive(guid: "PUBLICATION_GUID"))),
    .subsections("More", [
        .init(name: "Weekend", type: .feedArchive(guid: "WEEKEND_PUBLICATION_GUID", publicationName: "The Weekend")),
        .init(name: "Bookmarks", type: .bookmarks(type: .all)),
        .init(name: "Downloads", type: .downloads(type: .all))
    ])
]

let carousel = CarouselViewController(globalConfig: globalConfig, sections: sections)
```

You can mix both kinds, and dynamic archives, in one carousel. Each
[`CarouselViewController.ContentType`](/documentation/PSReader/CarouselViewController/ContentType) is one screen:

|Content type                                 |Shows                                                                                                                                      |
|---------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|
|`.feedArchive(guid:publicationName:config:)` |One publication’s editions, from its publication GUID. The publication name defaults to the section or subsection name.                    |
|`.feedPublicationKiosk(publications:config:)`|A grid of publications, each a ``doc://com.pagesuite.PSReader/documentation/PSReader/KioskFeedPublication``. Tapping one opens its archive.|
|`.bookmarks(type:config:)`                   |The user’s bookmarked pages and articles. See <doc://com.pagesuite.PSReader/documentation/PSReader/Bookmarks>.                             |
|`.downloads(type:config:)`                   |Editions downloaded for offline reading. See <doc://com.pagesuite.PSReader/documentation/PSReader/Downloads-and-Offline-Reading>.          |
|`.search(config:)`                           |Search across the carousel’s publications. See <doc://com.pagesuite.PSReader/documentation/PSReader/Search>.                               |

None of these needs a shortcode, but nothing comes from PageSuite either:
an archive shows a date picker only when you set
[`datePicker`](/documentation/PSReader/ArchiveConfiguration/datePicker), for example. Sections you define use
the app configuration a dynamic archive in the same carousel loads. A
carousel without one has no app configuration unless you set it, which
in-article adverts and a few other features need; see
[The App Configuration](/documentation/PSReader/Configuring-the-Prebuilt-UI#The-App-Configuration).

> Replica: Two content types show publications on the legacy replica
> system. `.replicaArchive(guid:supplements:config:)` lists a replica
> publication’s editions from its replica publication GUID. Name
> supplement publications in `supplements` to add a row of their latest
> editions below the publication’s latest edition, titled with
> ``doc://com.pagesuite.PSReader/documentation/PSReader/LocalizedStringKey/supplementsTitle``:
> 
> ```swift
> .section(.init(
>     name: "Today",
>     type: .replicaArchive(
>         guid: "REPLICA_PUBLICATION_GUID",
>         supplements: ["SUPPLEMENT_PUBLICATION_GUID"]
>     )
> ))
> ```
> 
> `.replicaPublicationKiosk(publications:config:)` is a kiosk of
> ``doc://com.pagesuite.PSReader/documentation/PSReader/KioskReplicaPublication`` entries. See <doc://com.pagesuite.PSReader/documentation/PSReader/Identifiers>.

## Configuring One Section

Every content type except search takes an optional configuration, which
replaces the one the carousel would create from your global configuration.
Use it to give one section a different look or reader:

```swift
var magazineConfig = ArchiveConfiguration(globalConfig: globalConfig)
magazineConfig.cellAspectRatio = 0.75
magazineConfig.thumbnailContentMode = .flexibleHeight(estimatedAspectRatio: 0.75)
magazineConfig.readerConfig.settings.isDoublePageEnabled = false

let magazine = CarouselViewController.Content(
    name: "Magazine",
    type: .feedArchive(guid: "MAGAZINE_PUBLICATION_GUID", config: magazineConfig)
)
```

A kiosk’s configuration applies to every publication in it, unless a
[`KioskFeedPublication`](/documentation/PSReader/KioskFeedPublication) carries its own.

## Adding a Header

Pass a view controller as `header` to pin it above the section ribbon,
such as a bar with your logo. Set
[`hidesHeaderOnScroll`](/documentation/PSReader/CarouselConfiguration/hidesHeaderOnScroll) to slide it away as the
user scrolls down, and back when they scroll up or change section:

```swift
var carouselConfig = CarouselConfiguration(globalConfig: globalConfig)
carouselConfig.hidesHeaderOnScroll = true

let carousel = CarouselViewController(
    globalConfig: globalConfig,
    carouselConfig: carouselConfig,
    header: BrandHeaderViewController(),
    sections: sections
)
```

`BrandHeaderViewController` stands for your own view controller. The
carousel sizes the header from its view’s Auto Layout constraints, so give
the view’s content constraints that determine its height.

## Presenting the Carousel Modally

A carousel you present needs a way to close.
[`DismissHeaderViewController`](/documentation/PSReader/DismissHeaderViewController) is a ready-made header with a single close
button. Tapping it dismisses the carousel, or calls the `onClose` closure
you pass instead:

```swift
let carousel = CarouselViewController(
    globalConfig: globalConfig,
    header: DismissHeaderViewController(config: .dismissButton(position: .trailing())),
    sections: sections
)
carousel.modalPresentationStyle = .fullScreen
present(carousel, animated: true)
```

Style the button with
[`dismissButton(size:insets:position:tintColor:image:)`](/documentation/PSReader/ButtonConfiguration/dismissButton(size:insets:position:tintColor:image:)).
Leave [`hidesHeaderOnScroll`](/documentation/PSReader/CarouselConfiguration/hidesHeaderOnScroll) at its default,
`false`, so the button never scrolls out of reach.

## Fitting the Carousel Into Your Layout

The carousel wraps itself in a navigation controller of its own, which it
uses to push a kiosk publication’s archive. If you place the carousel
inside your own `UINavigationController`, turn that off, or the screen
shows two navigation bars:

```swift
var carouselConfig = CarouselConfiguration(globalConfig: globalConfig)
carouselConfig.embedInNavigationController = false
```

Kiosk publications then open on your navigation controller. If it has no
delegate, the carousel becomes its delegate when it first pushes one, so
that it can show the navigation bar on publication archives only. Without
any navigation controller, tapping a kiosk publication does nothing, so
keep the default when you show kiosks without one of your own.

The carousel keeps its content inside the safe area. To let content run
to an edge instead, such as under a translucent tab bar, name that edge in
[`ignoreSafeArea`](/documentation/PSReader/CarouselConfiguration/ignoreSafeArea):

```swift
carouselConfig.ignoreSafeArea = .bottom
```

To keep content clear of something you draw over the carousel, such as a
mini player along the bottom, add the space to the carousel’s
`additionalSafeAreaInsets`:

```swift
carousel.additionalSafeAreaInsets.bottom = 64
```

> Note: The carousel passes its `overrideUserInterfaceStyle` on to every
> screen it shows, the reader included. See <doc://com.pagesuite.PSReader/documentation/PSReader/Theming#Dark-Mode>.

## Laying Out the Ribbons

The section ribbon lays out its tabs in one of three ways, set at
[`layout`](/documentation/PSReader/SectionRibbonConfiguration/layout):

- `.fitLeft`, the default, aligns the tabs to the leading edge.
- `.fitCenter` centers them.
- `.fillEqually` divides the ribbon’s width equally between the tabs, so
  it suits a few short section names.

With `.fitLeft` and `.fitCenter`, the ribbon scrolls when the tabs don’t
fit.

The subsection ribbon’s pills align `.left`, the default, or `.center`,
through [`alignment`](/documentation/PSReader/SubsectionRibbonConfiguration/alignment-swift.property). Leading alignment
suits a compact width and centered a regular width:

```swift
var carouselConfig = CarouselConfiguration(globalConfig: globalConfig)
carouselConfig.sectionRibbon.layout = .fitCenter
carouselConfig.subsectionRibbon.alignment = .center
```

The carousel reads these values when it loads. If your app runs on iPad,
the width can change afterward, for example as the app enters Split View.
Pass the new layout to
[`setRibbonLayout(section:subsectionAlignment:)`](/documentation/PSReader/CarouselViewController/setRibbonLayout(section:subsectionAlignment:))
when the horizontal size class changes. The call does nothing when the
layout hasn’t changed. You can’t subclass the carousel, so make the call
from its parent:

```swift
override func willTransition(to newCollection: UITraitCollection,
                             with coordinator: UIViewControllerTransitionCoordinator) {
    super.willTransition(to: newCollection, with: coordinator)

    let isRegularWidth = newCollection.horizontalSizeClass == .regular
    carousel.setRibbonLayout(
        section: isRegularWidth ? .fitCenter : .fitLeft,
        subsectionAlignment: isRegularWidth ? .center : .left
    )
}
```

Choose the initial layout the same way, from the size class of the window
the carousel appears in, such as
`windowScene.traitCollection.horizontalSizeClass` when your scene
connects.

In SwiftUI, read the size class from the environment. SwiftUI calls
`updateUIViewController(_:context:)` when it changes:

```swift
func makeUIViewController(context: Context) -> CarouselViewController {
    let isRegularWidth = context.environment.horizontalSizeClass == .regular

    var carouselConfig = CarouselConfiguration(globalConfig: globalConfig)
    carouselConfig.sectionRibbon.layout = isRegularWidth ? .fitCenter : .fitLeft
    carouselConfig.subsectionRibbon.alignment = isRegularWidth ? .center : .left

    return CarouselViewController(
        globalConfig: globalConfig,
        carouselConfig: carouselConfig,
        sections: [.dynamicArchive("Editions", shortcode: "SHORTCODE")]
    )
}

func updateUIViewController(_ carousel: CarouselViewController, context: Context) {
    let isRegularWidth = context.environment.horizontalSizeClass == .regular
    carousel.setRibbonLayout(
        section: isRegularWidth ? .fitCenter : .fitLeft,
        subsectionAlignment: isRegularWidth ? .center : .left
    )
}
```

## Topics

### The Carousel

[`CarouselViewController`](/documentation/PSReader/CarouselViewController)

The primary view controller provided by the SDK for presenting digital publication
content through an intuitive carousel interface.

### Configuration

[`CarouselConfiguration`](/documentation/PSReader/CarouselConfiguration)

Configuration object for customizing the prebuilt carousel interface.

[`SectionRibbonConfiguration`](/documentation/PSReader/SectionRibbonConfiguration)

Configuration object controlling the appearance and layout of the carousel section ribbon.

[`SubsectionRibbonConfiguration`](/documentation/PSReader/SubsectionRibbonConfiguration)

Configuration used to customize the appearance and layout of the carousel subsection ribbon.

### Presenting Modally

[`DismissHeaderViewController`](/documentation/PSReader/DismissHeaderViewController)

A prebuilt carousel header containing a single dismiss (close) button.

[`ButtonConfiguration`](/documentation/PSReader/ButtonConfiguration)

Configuration object used to customize buttons displayed within the SDK’s UI.

