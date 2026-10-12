<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultAssetProvider",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader20DefaultAssetProviderV"
  },
  "title" : "DefaultAssetProvider"
}
-->

# DefaultAssetProvider

A default implementation of the [`AssetDelegate`](/documentation/PSReader/AssetDelegate) protocol that provides the SDK’s built-in assets.

```
struct DefaultAssetProvider
```

## Overview

This is the default asset delegate used when none is specified in
[`GlobalConfiguration`](/documentation/PSReader/GlobalConfiguration). It returns the SDK’s built-in icons for all
[`ImageResourceName`](/documentation/PSReader/ImageResourceName) and [`LegacyImageResourceName`](/documentation/PSReader/LegacyImageResourceName) values.

## Topics

### Creating an Asset Provider

[`init()`](/documentation/PSReader/DefaultAssetProvider/init())

Creates an asset provider that returns the SDK’s built-in assets.

### Icons

[`imageResource(for:)`](/documentation/PSReader/DefaultAssetProvider/imageResource(for:))

Returns the SDK’s built-in image for the asset, from
[`defaultImage()`](/documentation/PSReader/ImageResourceName/defaultImage()).

### Logos and Placeholders

[`headerLogo(for:currentTraitCollection:)`](/documentation/PSReader/DefaultAssetProvider/headerLogo(for:currentTraitCollection:))

Returns `nil`, so the splash screen shows no logo and templates that
show a masthead use the header logo from the `PSAppConfig`.

[`placeholderImage(size:with:completion:)`](/documentation/PSReader/DefaultAssetProvider/placeholderImage(size:with:completion:))

Calls `completion` with `nil`, so the SDK keeps showing its default
skeleton placeholder.

### Replica Editions

[`legacyImageResource(for:)`](/documentation/PSReader/DefaultAssetProvider/legacyImageResource(for:))

Returns the legacy replica reader’s built-in image for the asset, from
[`defaultImage()`](/documentation/PSReader/LegacyImageResourceName/defaultImage()).

[`headerLogo(publicationGUID:editionGUID:currentTraitCollection:)`](/documentation/PSReader/DefaultAssetProvider/headerLogo(publicationGUID:editionGUID:currentTraitCollection:))

Returns `nil`, so the splash screen for replica editions shows no
logo.

