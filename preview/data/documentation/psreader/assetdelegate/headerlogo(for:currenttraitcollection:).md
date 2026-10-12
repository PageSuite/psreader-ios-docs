<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AssetDelegate/headerLogo(for:currentTraitCollection:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13AssetDelegateP10headerLogo3for22currentTraitCollection10Foundation3URLVSgAA12PSEPublishedC_So07UITraitI0CSgtF"
  },
  "title" : "headerLogo(for:currentTraitCollection:)"
}
-->

# headerLogo(for:currentTraitCollection:)

Provides a URL to a custom logo / masthead for a given published edition.
Used in the splash screen. Can be used by some templates.

```
func headerLogo(for published: PSEPublished, currentTraitCollection: UITraitCollection?) -> URL?
```

## Parameters

`published`

The published edition.

`currentTraitCollection`

The current trait collection, used to select a dark mode logo variant if available.

## Return Value

A URL pointing to the custom header logo image, or `nil` to omit the logo.