<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Localization",
  "metadataVersion" : "0.1.0",
  "role" : "collectionGroup",
  "title" : "Localization"
}
-->

# Localization

Translate the prebuilt UI’s text, or replace any of its strings with your own.

## Overview

The prebuilt UI asks [`LocalizationManager`](/documentation/PSReader/LocalizationManager) for every string it shows,
naming each one with a [`LocalizedStringKey`](/documentation/PSReader/LocalizedStringKey). The shared manager looks
the string up in your app with `NSLocalizedString`, using the SDK’s
English text as the key, and falls back to that English text. So
translations in your app’s `Localizable` strings file or String Catalog
reach the SDK without any code:

```
/* Localizable.strings (French) */
"Contents" = "Sommaire";
"Bookmarks" = "Signets";
"Search" = "Rechercher";
"Most Recent" = "Les plus récentes";
```

Building your own reader screen? The core reader asks the same manager
for the few strings it draws; see [Localizing the Reader’s Text](/documentation/PSReader/Hosting-the-Reader#Localizing-the-Readers-Text).

Text that comes from you or from PageSuite isn’t the SDK’s to translate:
the section names you give the carousel, archive names in a dynamic
archive’s configuration, and the editions themselves.

## Adding Translations

Each case of [`LocalizedStringKey`](/documentation/PSReader/LocalizedStringKey) documents its English text. Use that
text, exactly, as the key in a `Localizable.strings` file or a
`Localizable.xcstrings` String Catalog in your app target. Xcode doesn’t
find the SDK’s strings when it scans your code, so add the entries
yourself.

Two strings take a number: `"%lld comments"` and `"View comments (%lld)"`.
In a String Catalog, vary them by plural.

Some keys share their English text, so one translation covers both:

|English text      |Keys                                                                                                                                                                                        |
|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|`"Search"`        |``doc://com.pagesuite.PSReader/documentation/PSReader/LocalizedStringKey/search``, ``doc://com.pagesuite.PSReader/documentation/PSReader/LocalizedStringKey/searchBarPlaceholder``          |
|`"You're offline"`|``doc://com.pagesuite.PSReader/documentation/PSReader/LocalizedStringKey/offlineTitle``, ``doc://com.pagesuite.PSReader/documentation/PSReader/LocalizedStringKey/errorLoadingOfflineTitle``|
|`"Order by added"`|``doc://com.pagesuite.PSReader/documentation/PSReader/LocalizedStringKey/orderByDownloaded``, ``doc://com.pagesuite.PSReader/documentation/PSReader/LocalizedStringKey/orderByBookmarked``  |

To word them differently, replace them in code.

## Replacing Strings in Code

Subclass [`LocalizationManager`](/documentation/PSReader/LocalizationManager) and override
[`localizedString(for:)`](/documentation/PSReader/LocalizationManager/localizedString(for:)) to supply your own text for
some keys, from your own strings or your server, and call `super` for the
rest:

```swift
final class BrandLocalizationManager: LocalizationManager {
    override func localizedString(for key: LocalizedStringKey) -> String {
        switch key {
        case .bookmarks:
            return NSLocalizedString("Saved", comment: "Title of the saved pages screen")
        case .searchBarPlaceholder:
            return NSLocalizedString("Search past editions", comment: "Search field placeholder")
        case .commentButtonByline(let count?) where count > 99:
            return "99+"
        default:
            return super.localizedString(for: key)
        }
    }
}
```

Install it as the shared manager before you create any of the SDK’s view
controllers, for example when your app launches:

```swift
LocalizationManager.shared = BrandLocalizationManager()
```

Screens created earlier keep the text they already showed.

> Note: In the Swift 6 language mode, the compiler rejects setting
> `shared` because it’s mutable global state. Import the SDK with
> `@preconcurrency import PSReader` in the file that sets it.

## Keeping Translations Current

SDK releases sometimes add keys. After updating, check
[`LocalizedStringKey`](/documentation/PSReader/LocalizedStringKey) for new cases and add their translations; until
you do, those strings show in English.

> Note: Two strings don’t go through the manager yet: the Copy Link
> action in the share sheet, and the “Top stories” section that heads
> some editions in the content browser.

> Replica: Some of the legacy replica reader’s text is in English only
> and doesn’t go through the manager. The modern reader, which
> ``doc://com.pagesuite.PSReader/documentation/PSReader/ReaderConfiguration/useLegacyReplicaReader`` set to `false` uses for
> replica editions, does.

## Topics

### Strings

[`LocalizationManager`](/documentation/PSReader/LocalizationManager)

Provides localized strings.

[`LocalizedStringKey`](/documentation/PSReader/LocalizedStringKey)

Defines keys used to identify localizable strings in the SDK.

