<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Updating-the-SDK",
  "metadataVersion" : "0.1.0",
  "role" : "article",
  "title" : "Updating the SDK"
}
-->

# Updating the SDK

Move your app from one SDK release to the next: the breaking changes in each release, and what to change in your code.

## v26.8.0

**One module: PSReader**

PSReaderUI has merged into the `PSReader` module, which now holds the
prebuilt UI and the core SDK it’s built on.
[Migrating From PSReaderUI](/documentation/PSReader/Migrating-From-PSReaderUI) walks through each breaking change.

An app on the legacy Core SDK has a rewrite to do; see
[Migrating From the Legacy Core SDK](/documentation/PSReader/Migrating-From-the-Legacy-Core-SDK).

## v26.7.0

**Carousel headers replace `dismissButton`**

Breaking change: `CarouselConfiguration.dismissButton` has been removed. The
carousel now accepts a full header view controller, pinned above the carousel
content, via the new `header` parameter on the [`CarouselViewController`](/documentation/PSReader/CarouselViewController)
initializer.

To retain the previous dismiss button behavior, pass a
[`DismissHeaderViewController`](/documentation/PSReader/DismissHeaderViewController) as the header. It accepts the same
[`dismissButton(size:insets:position:tintColor:image:)`](/documentation/PSReader/ButtonConfiguration/dismissButton(size:insets:position:tintColor:image:))
configuration as before, and by default dismisses the carousel on tap. Supply
`onClose` to run custom behaviour instead (for example when the carousel is
embedded rather than presented).

```swift
// Before
var carouselConfig = PSReader.CarouselConfiguration(globalConfig: globalConfig)
carouselConfig.dismissButton = .dismissButton(position: .leading())

let carousel = CarouselViewController(
    globalConfig: globalConfig,
    carouselConfig: carouselConfig,
    sections: sections
)

// After
let carousel = CarouselViewController(
    globalConfig: globalConfig,
    carouselConfig: carouselConfig,
    header: DismissHeaderViewController(config: .dismissButton(position: .leading())),
    sections: sections
)
```

Headers can also hide as the content scrolls via
[`hidesHeaderOnScroll`](/documentation/PSReader/CarouselConfiguration/hidesHeaderOnScroll). Leave it `false` (the default)
when using a [`DismissHeaderViewController`](/documentation/PSReader/DismissHeaderViewController) so the close button stays
reachable.

**Search API changes**

To support replica search, [`SearchService`](/documentation/PSReader/SearchService) is now a protocol with two
implementations:

- ``doc://com.pagesuite.PSReader/documentation/PSReader/FeedSearchService`` — the previous `SearchService` struct, renamed. It
  searches feed edition publications.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/ReplicaSearchService`` — new. It searches replica publications.

If you use the service directly, replace `SearchService()` with
`FeedSearchService()`; the `search` method signature is unchanged. The nested
types have moved to the top level: `SearchService.SearchType` is now
[`SearchType`](/documentation/PSReader/SearchType) and `SearchService.Response` is now [`SearchResponse`](/documentation/PSReader/SearchResponse).

**Advert pages and analytics**

Advert pages join the feed edition page flow as a new page type
(see [Full-Page Advert Pages](/documentation/PSReader/Advertisements#Full-Page-Advert-Pages)). If your editions contain
them, be aware of the analytics implications:

- An advert page settling on screen fires `feedEditionOtherPageView`, the same
  event as other non-article, non-section pages. If you report page views
  downstream, decide whether advert views should count — the event context’s
  page spread identifies advert pages (`referencePage()?.isAdvertPage`).
- In double-page mode, a spread’s reference page prefers editorial content: a
  spread pairing an advert with an editorial page reports the editorial page,
  so only advert-only spreads report an advert. The page-zero advert always
  shares its spread with the cover, so it never produces its own page-view
  event; single-page mode does not include the page-zero advert at all.

## v26.1.0

**Archive limit defaults**

`archiveLimit` now defaults to `nil`, with type-specific behavior:

- Replica archives: 30 editions (unchanged from previous releases).
- Feed archives: unbounded — shows the full backend archive (usually ~1 year).

This is a behavior change for feed edition clients who previously saw a default
of 30 editions. To restore the old behavior, explicitly set `archiveLimit`:

```swift
var archiveConfig = PSReader.ArchiveConfiguration(globalConfig: globalConfig)
archiveConfig.archiveLimit = 30
```

**Modern replica reader**

A modern replacement for the legacy replica reader is now available. It shares
delegates and navigation with the feed edition reader, giving end users the same
experience regardless of backend. Replica-specific analytics events still fire.

Opt in by setting `useLegacyReplicaReader` to `false` (defaults to `true` for
now). The modern reader will become the default in a future release, and the
legacy reader will be removed further out.

```swift
var archiveConfig = PSReader.ArchiveConfiguration(globalConfig: globalConfig)
archiveConfig.readerConfig.useLegacyReplicaReader = false
```

> Important: The legacy reader’s content browser next/previous button events are
> not reported in the modern reader:
> `replicaPageBrowserNextTapped`,
> `replicaPageBrowserPreviousTapped`,
> `replicaArticleBrowserNextTapped`,
> `replicaArticleBrowserPreviousTapped`.

> Note: `LegacyReaderConfiguration` properties (e.g. `shareTemplater`,
> `prefersStatusBarHidden`, `navigationBarItems`) do not apply to the modern
> reader — it uses the standard `ReaderConfiguration` delegates instead.

## v5.5.0

**Liquid Glass UI defaults**

On iOS 26 and later, the SDK defaults to a new Liquid Glass design. The SDK
respects the host app’s `UIDesignRequiresCompatibility` flag and will fall back
automatically on older OS versions. The new design can also be controlled via
the `LiquidGlassPolicy` option. You can apply this globally or more granularly
on specific configuration objects (for example, subsection ribbon, navigation
bar, page browser, etc.). To disable it globally:

```swift
var globalConfig = PSReader.GlobalConfiguration(apiKey: apiKey, accountGUID: accountGUID)
globalConfig.liquidGlassPolicy = .disabled // disable Liquid Glass across the SDK
```

**Archive thumbnail layout**

Archive thumbnails now offer a dynamic layout mode:
`ImageContentMode.flexibleHeight`. It lets edition artwork (including the
latest/hero card) grow or shrink to its true aspect ratio, keeping the full
image visible instead of cropping. Start with an estimated ratio for a steady
initial layout; the SDK tunes the size automatically once the real image
arrives. Example:

```swift
var archiveConfig = PSReader.ArchiveConfiguration(globalConfig: globalConfig)
archiveConfig.thumbnailContentMode = .flexibleHeight(estimatedAspectRatio: 0.9)
```

## v5.2.0

**Reader UI/UX Changes**

In PDF-driven editions, PDF pages and articles are now segmented. Users can no
longer swipe between them. Articles are accessed either via article hotspot
links or through the content browser. The content browser is also segmented in
the same way, with a toggle that allows switching between pages and articles.
This behavior now matches the web reader.

The navigation bar layout has also been updated:

- The right-side back arrow has been removed.
- The left-side icon now adapts to the current context:
  - Dismiss Article – If the user opened an article from a hotspot link, this
    action returns them to the PDF page containing that article.
  - Dismiss Reader – In all other cases, this action dismisses the reader
    view controller.

You can customize the icons for these actions via your `AssetDelegate`:

```swift
ImageResourceName.dismiss        // Default: back arrow
ImageResourceName.dismissArticle // Default: xmark
```

## v5.0.0

**Edition Download Behavior**

`5.0.0` introduces the ability to read editions without downloading them.
This is the new default behavior. It can be customized by users via the reader
settings menu. To retain the original default:

```swift
var archiveConfig = PSReader.ArchiveConfiguration(globalConfig: globalConfig)
archiveConfig.readerConfig.settings.downloadWhileReadingDefault = false

// To hide the user facing setting
archiveConfig.readerConfig.settings.isDownloadWhileReadingToggleEnabled = false
archiveConfig.readerConfig.settings.isDownloadWhileReadingPreferenceAlertEnabled = false
```

**Edition Date Formatting**

Breaking Change: `DateFormatter` objects in configuration structs have been
replaced with the `EditionDateFormatter` protocol. This enables more fine
grained customization and allows for alternative naming strategies such as
edition names, identifiers, or any other custom labeling approach.

The SDK provides a `DefaultEditionDateFormatter` that wraps a
`DateFormatter`. This allows

```swift
let dateFormatter = DateFormatter()
dateFormatter.dateFormat = "d MMMM yyyy"
dateFormatter.timeZone = .current
archiveConfig.dateFormatter = DefaultEditionDateFormatter(dateFormatter: dateFormatter)

// Alternative initializer
archiveConfig.dateFormatter = DefaultEditionDateFormatter(dateFormat: "d MMMM yyyy", timeZone: .current)
```

**Asset Customization**

Breaking Change: The `imageResourceForName` callbacks have been removed. They
have been replaced by `AssetDelegate`. To migrate to the new system implement
the delegate and set it as needed.

```
// Customize assets as desired
struct MyAssetDelegate: PSReader.AssetDelegate {
    func imageResource(for name: ImageResourceName) -> UIImage? {
        return name.defaultImage()
    }
}

var globalConfig = PSReader.GlobalConfiguration(apiKey: apiKey, accountGUID: accountGUID)
globalConfig.assetDelegate = MyAssetDelegate()
```