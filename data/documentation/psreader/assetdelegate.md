<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AssetDelegate",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13AssetDelegateP"
  },
  "title" : "AssetDelegate"
}
-->

# AssetDelegate

A delegate protocol for providing custom images and logos used within the SDK.

```
protocol AssetDelegate
```

## Overview

Implement this delegate to override default UI assets such as icons and logos used
by the reader. If no delegate is provided, the SDK will use its built-in default assets.

## Usage

```swift
struct MyAssetDelegate: AssetDelegate {
    func imageResource(for name: ImageResourceName) -> UIImage? {
        switch name {
        case .share: return UIImage(named: "my-share-icon")
        case .bookmark: return UIImage(named: "my-bookmark-icon")
        default: return name.defaultImage()
        }
    }
}
```

> Important: Always call ``doc://com.pagesuite.PSReader/documentation/PSReader/ImageResourceName/defaultImage()`` in the `default`
> case to preserve SDK defaults for icons you do not customize.

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Theming>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/ImageResourceName``

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/DefaultAssetProvider``

## Topics

### Replacing Icons

[`imageResource(for:)`](/documentation/PSReader/AssetDelegate/imageResource(for:))

Provides a custom image for the specified asset used in the SDK.

### Providing Logos and Placeholders

[`headerLogo(for:currentTraitCollection:)`](/documentation/PSReader/AssetDelegate/headerLogo(for:currentTraitCollection:))

Provides a URL to a custom logo / masthead for a given published edition.
Used in the splash screen. Can be used by some templates.

[`placeholderImage(size:with:completion:)`](/documentation/PSReader/AssetDelegate/placeholderImage(size:with:completion:))

Provides a placeholder image for content that is unavailable.

### Using the Built-In Assets

[`DefaultAssetProvider`](/documentation/PSReader/DefaultAssetProvider)

A default implementation of the [`AssetDelegate`](/documentation/PSReader/AssetDelegate) protocol that provides the SDK’s built-in assets.

### Replica Editions

[`legacyImageResource(for:)`](/documentation/PSReader/AssetDelegate/legacyImageResource(for:))

Provides a custom image for legacy reader components.

[`headerLogo(publicationGUID:editionGUID:currentTraitCollection:)`](/documentation/PSReader/AssetDelegate/headerLogo(publicationGUID:editionGUID:currentTraitCollection:))

Provides a URL to a custom logo / masthead for a replica edition.
Used in the splash screen for replica readers.

