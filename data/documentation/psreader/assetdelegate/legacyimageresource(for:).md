<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AssetDelegate/legacyImageResource(for:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13AssetDelegateP19legacyImageResource3forSo7UIImageCSgAA06LegacyeF4NameO_tF"
  },
  "title" : "legacyImageResource(for:)"
}
-->

# legacyImageResource(for:)

Provides a custom image for legacy reader components.

```
func legacyImageResource(for name: LegacyImageResourceName) -> UIImage?
```

## Parameters

`name`

The identifier for the requested legacy image resource.

## Return Value

A custom UIImage, or `nil` to use the default asset.

## Discussion

Default implementation uses SDKs default assets.