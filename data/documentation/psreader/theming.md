<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Theming",
  "metadataVersion" : "0.1.0",
  "role" : "collectionGroup",
  "title" : "Theming"
}
-->

# Theming

Match the prebuilt UI to your brand: fonts, colors, dark mode, icons, placeholders, dates, thumbnails, and Liquid Glass.

## Overview

Three values in [`GlobalConfiguration`](/documentation/PSReader/GlobalConfiguration) theme the whole prebuilt UI: a
primary font, a secondary font, and a brand color. Every screen and
reader starts from them:

```swift
let globalConfig = GlobalConfiguration(
    apiKey: "API_KEY",
    accountGUID: "ACCOUNT_GUID",
    primaryFont: UIFont(name: "Georgia", size: 12)!,
    secondaryFont: UIFont(name: "AvenirNext-Regular", size: 12)!,
    brandColor: UIColor(named: "BrandColor")!
)
```

![The prebuilt UI with callouts showing where the fonts, brand color, and label configurations apply.](images/com.pagesuite.PSReader/theming-overview-annotated~dark@2x.png)

Set these first, then adjust single screens through their own
configurations. Each configuration copies its starting values from the
global configuration when you create it; [Configuring the Prebuilt UI](/documentation/PSReader/Configuring-the-Prebuilt-UI)
explains the cascade and the order to build things in.

## Fonts

The **primary font** sets titles, headlines, publication names, and the
reader’s navigation buttons. The **secondary font** sets everything else:
dates, captions, ribbons, and the content browser. The SDK sets each
element’s point size and weight itself and takes only the typeface from
your fonts. Register custom fonts in your app as usual.

Each element’s text is a [`LabelConfiguration`](/documentation/PSReader/LabelConfiguration): a font, a point size, and
a color. Change one element without touching the rest by editing its
label configuration in place:

```swift
var archiveConfig = ArchiveConfiguration(globalConfig: globalConfig)
archiveConfig.titleLabel.font = UIFont(name: "Georgia-Bold", size: 14)!
archiveConfig.titleLabel.pointSize = 14
archiveConfig.titleLabel.color = .label
```

The label uses `font` at `pointSize`, whatever size the font itself has.

## Brand Color

The brand color is the accent: the selected section’s indicator, the
selected subsection pill, the reader’s selected navigation buttons, the
splash screen’s progress bar, and the date picker’s toggle. Give it a
color that works in both light and dark mode, from your asset catalog or
in code:

```swift
let brandColor = UIColor { traits in
    traits.userInterfaceStyle == .dark
        ? UIColor(red: 0.45, green: 0.65, blue: 1, alpha: 1)
        : UIColor(red: 0, green: 0.25, blue: 0.6, alpha: 1)
}
```

Backgrounds, dividers, and the remaining text colors have their own
properties on each configuration, such as
[`backgroundColor`](/documentation/PSReader/CarouselConfiguration/backgroundColor) and
[`backgroundColor`](/documentation/PSReader/ReaderConfiguration/backgroundColor).

## Dark Mode

The prebuilt UI follows the system’s light or dark appearance, and its
default colors adapt to both. Use dynamic colors for any you set, as in
the brand color above.

To force one appearance, set `overrideUserInterfaceStyle`. On the carousel,
it applies to every screen the carousel shows, the reader included:

```swift
carousel.overrideUserInterfaceStyle = .dark
```

The standalone screens take it too; see
[Fitting Screens Into Your Layout](/documentation/PSReader/Embedding-Prebuilt-Screens#Fitting-Screens-Into-Your-Layout). To
force one appearance across your whole app, set it on your window.

## Icons

Every icon in the prebuilt UI has an [`ImageResourceName`](/documentation/PSReader/ImageResourceName). To replace
some, implement [`imageResource(for:)`](/documentation/PSReader/AssetDelegate/imageResource(for:)) and return the SDK’s
image for the rest:

```swift
struct BrandAssets: AssetDelegate {
    func imageResource(for name: ImageResourceName) -> UIImage? {
        switch name {
        case .share:
            return UIImage(named: "brand-share")
        case .bookmark:
            return UIImage(named: "brand-bookmark")
        case .bookmarked:
            return UIImage(named: "brand-bookmark-filled")
        default:
            return name.defaultImage()
        }
    }
}

globalConfig.assetDelegate = BrandAssets()
```

Don’t return `nil` to mean “use the default”. The reader’s navigation bar
leaves out a button whose icon is `nil`, which is also how you remove one,
and the archive’s date picker leaves out its calendar icon.

The asset delegate also supplies the splash screen’s logo, through
[`headerLogo(for:currentTraitCollection:)`](/documentation/PSReader/AssetDelegate/headerLogo(for:currentTraitCollection:)), and placeholder
images, below. Every method has a default, so implement only what you
change. The global asset delegate reaches every screen; a few
configurations, such as [`BookmarksConfiguration`](/documentation/PSReader/BookmarksConfiguration), take one of their own.

> Replica: The legacy replica reader asks for its icons through
> ``doc://com.pagesuite.PSReader/documentation/PSReader/AssetDelegate/legacyImageResource(for:)``, with
> ``doc://com.pagesuite.PSReader/documentation/PSReader/LegacyImageResourceName`` cases. Return `nil` there to keep the
> default icon.

## Placeholder Images

Until a thumbnail loads, or when an article has no image, the SDK shows
a gray skeleton that adapts to light and dark mode. To show your own
image instead, implement
[`placeholderImage(size:with:completion:)`](/documentation/PSReader/AssetDelegate/placeholderImage(size:with:completion:)):

```swift
struct BrandAssets: AssetDelegate {
    func placeholderImage(size: CGSize,
                          with traits: UITraitCollection,
                          completion: @escaping (UIImage?) -> Void) {
        let isDark = traits.userInterfaceStyle == .dark
        completion(UIImage(named: isDark ? "placeholder-dark" : "placeholder-light"))
    }
}
```

`size` is the size of the space to fill, and `traits` carries the
appearance, display scale, and size classes. Call `completion` with `nil`
to keep the skeleton.

## Date Formatting

Archives, the splash screen, bookmarks, downloads, and search show each
edition’s date through an [`EditionDateFormatter`](/documentation/PSReader/EditionDateFormatter). The default,
[`DefaultEditionDateFormatter`](/documentation/PSReader/DefaultEditionDateFormatter), formats dates with a `DateFormatter`
pattern, such as “September 14, 2026” by default:

```swift
var globalConfig = GlobalConfiguration(
    apiKey: "API_KEY",
    accountGUID: "ACCOUNT_GUID",
    timeZone: TimeZone(identifier: "America/New_York")!
)
globalConfig.dateFormatter = DefaultEditionDateFormatter(
    dateFormat: "EEEE d MMMM yyyy",
    timeZone: globalConfig.timeZone
)
```

Set [`timeZone`](/documentation/PSReader/GlobalConfiguration/timeZone) to your publication’s time zone, so
that an edition shows the same date for every user wherever they are.
Configurations copy the formatter when you create them, so set it before
creating any.

A [`PSEPublished`](/documentation/PSReader/PSEPublished) carries two dates. [`editionDate`](/documentation/PSReader/PSEPublished/editionDate) is the
date the edition is for, the one on its masthead;
[`datePublished`](/documentation/PSReader/PSEPublished/datePublished) is when it was published, which needn’t be
the same day. The default formatter shows the edition date, and falls
back to `datePublished` only when an edition has none. Show the
edition date in lists of your own too. Formatting it with your global
configuration’s formatter keeps it matching the prebuilt screens:

```swift
cell.dateLabel.text = globalConfig.dateFormatter.string(for: published)
```

Some publishers name editions instead of dating them, such as “Holiday
Special”. [`useCustomEditionName`](/documentation/PSReader/PSEPublished/useCustomEditionName) says when to show
[`name`](/documentation/PSReader/PSEPublished/name). The default formatter always shows the date, so
show names with a formatter of your own, forwarding everything else to
the default:

```swift
struct EditionNameFormatter: EditionDateFormatter {
    let dates = DefaultEditionDateFormatter(dateFormat: "d MMMM yyyy")

    func string(for published: PSEPublished) -> String {
        if published.useCustomEditionName, !published.name.isEmpty {
            return published.name
        }
        return dates.string(for: published)
    }

    func string(for bookmark: PSEBookmarkPage) -> String { dates.string(for: bookmark) }
    func string(for bookmark: PSEBookmarkArticle) -> String { dates.string(for: bookmark) }
    func string(for result: SearchResult) -> String { dates.string(for: result) }

    // Legacy replica editions and bookmarks.
    func string(for edition: PSEdition) -> String { dates.string(for: edition) }
    func string(for bookmark: PSBookmark) -> String { dates.string(for: bookmark) }
    func string(for bookmark: PSBookmarkArticle) -> String { dates.string(for: bookmark) }
}
```

## Thumbnails

[`ImageContentMode`](/documentation/PSReader/ImageContentMode) sets how edition thumbnails fit their cells in
archives, bookmarks, downloads, and the splash screen:

- ``doc://com.pagesuite.PSReader/documentation/PSReader/ImageContentMode/fitToWidth`` fills the cell’s width and crops the
  top and bottom if the shapes differ. It’s the default for archives,
  bookmarks, and downloads.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/ImageContentMode/fitToHeight`` fills the cell’s height and crops the
  sides if needed. It’s the default for the splash screen.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/ImageContentMode/flexibleHeight(estimatedAspectRatio:)`` fills the
  width and lets each cell’s height follow its image, so nothing is
  cropped. The estimate sizes cells while images load; the SDK refines
  it as they arrive.

```swift
var archiveConfig = ArchiveConfiguration(globalConfig: globalConfig)
archiveConfig.cellAspectRatio = 0.75
archiveConfig.thumbnailContentMode = .flexibleHeight(estimatedAspectRatio: 0.75)
```

Pair the mode with the cell shape: [`cellAspectRatio`](/documentation/PSReader/ArchiveConfiguration/cellAspectRatio)
in archives, `aspectRatio` in [`BookmarksConfiguration`](/documentation/PSReader/BookmarksConfiguration) and
[`DownloadsConfiguration`](/documentation/PSReader/DownloadsConfiguration). The archive’s large latest-edition cell
follows the same mode, except that a flexible height becomes
[`ImageContentMode.fitToHeight`](/documentation/PSReader/ImageContentMode/fitToHeight) there; set
[`latestPaperThumbnailContentMode`](/documentation/PSReader/ArchiveConfiguration/latestPaperThumbnailContentMode) to choose
another.

> Note: The bookmarks and downloads screens don’t support
> ``doc://com.pagesuite.PSReader/documentation/PSReader/ImageContentMode/flexibleHeight(estimatedAspectRatio:)``.

## Liquid Glass

On iOS 26 and later, the prebuilt UI uses Liquid Glass: the reader’s
navigation bar and the carousel’s subsection ribbon float over the
content, which scrolls beneath them. [`LiquidGlassPolicy`](/documentation/PSReader/LiquidGlassPolicy) controls it:

- ``doc://com.pagesuite.PSReader/documentation/PSReader/LiquidGlassPolicy/automatic``, the default, uses Liquid Glass when the
  system supports it, unless your app sets `UIDesignRequiresCompatibility`
  in its Info.plist.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/LiquidGlassPolicy/disabled`` keeps the earlier appearance on every
  version of iOS.

Set the policy once on [`liquidGlassPolicy`](/documentation/PSReader/GlobalConfiguration/liquidGlassPolicy), or on
one component, such as the subsection ribbon, the reader’s navigation
bar, content browser, or splash screen:

```swift
// Everywhere.
globalConfig.liquidGlassPolicy = .disabled

// Only the subsection ribbon.
carouselConfig.subsectionRibbon.liquidGlassPolicy = .disabled
```

## Empty Screens

When the user has no bookmarks or downloads yet, those screens show an
icon, a title, and a short explanation. Style them through
[`ContentUnavailableConfiguration`](/documentation/PSReader/ContentUnavailableConfiguration), at `noContentConfig` on
[`BookmarksConfiguration`](/documentation/PSReader/BookmarksConfiguration) and [`DownloadsConfiguration`](/documentation/PSReader/DownloadsConfiguration):

```swift
var bookmarksConfig = BookmarksConfiguration(globalConfig: globalConfig)
bookmarksConfig.noContentConfig.image = UIImage(systemName: "bookmark.slash")
bookmarksConfig.noContentConfig.imageSize = CGSize(width: 32, height: 32)
bookmarksConfig.noContentConfig.tintColor = .secondaryLabel
```

The icon is drawn in the tint color. The text comes from
[`LocalizationManager`](/documentation/PSReader/LocalizationManager), under keys such as
[`LocalizedStringKey.noBookmarksTitle`](/documentation/PSReader/LocalizedStringKey/noBookmarksTitle) and
[`LocalizedStringKey.noBookmarksMessage`](/documentation/PSReader/LocalizedStringKey/noBookmarksMessage); see [Localization](/documentation/PSReader/Localization).

## Topics

### Fonts

[`LabelConfiguration`](/documentation/PSReader/LabelConfiguration)

Configuration object that specifies the appearance of `UILabels` used
throughout the prebuilt UI.

### Icons and Placeholders

[`AssetDelegate`](/documentation/PSReader/AssetDelegate)

A delegate protocol for providing custom images and logos used within the SDK.

[`ImageResourceName`](/documentation/PSReader/ImageResourceName)

An enumeration of asset identifiers used by the SDK’s UI components.

### Date Formatting

[`EditionDateFormatter`](/documentation/PSReader/EditionDateFormatter)

A protocol defining methods for generating display strings to represent editions.

[`DefaultEditionDateFormatter`](/documentation/PSReader/DefaultEditionDateFormatter)

Default implementation of [`EditionDateFormatter`](/documentation/PSReader/EditionDateFormatter) using `DateFormatter`.

### Thumbnails

[`ImageContentMode`](/documentation/PSReader/ImageContentMode)

Defines how an image should be resized and positioned within its container.

### Liquid Glass

[`LiquidGlassPolicy`](/documentation/PSReader/LiquidGlassPolicy)

A policy describing how the SDK adopts the iOS Liquid Glass UI effect.

### Empty Screens

[`ContentUnavailableConfiguration`](/documentation/PSReader/ContentUnavailableConfiguration)

Configuration for customizing the appearance and behavior of content unavailable screens.

### Replica

[`LegacyImageResourceName`](/documentation/PSReader/LegacyImageResourceName)

Enumeration of asset identifiers used specifically by the legacy reader.

