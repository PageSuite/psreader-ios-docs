<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultAssetProvider/headerLogo(for:currentTraitCollection:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13AssetDelegatePAAE10headerLogo3for22currentTraitCollection10Foundation3URLVSgAA12PSEPublishedC_So07UITraitI0CSgtF::SYNTHESIZED::s:8PSReader20DefaultAssetProviderV"
  },
  "title" : "headerLogo(for:currentTraitCollection:)"
}
-->

# headerLogo(for:currentTraitCollection:)

Returns `nil`, so the splash screen shows no logo and templates that
show a masthead use the header logo from the `PSAppConfig`.

```
func headerLogo(for published: PSEPublished, currentTraitCollection: UITraitCollection? = nil) -> URL?
```

## Parameters

`published`

The published edition.

`currentTraitCollection`

The current trait collection.

## Return Value

`nil`.