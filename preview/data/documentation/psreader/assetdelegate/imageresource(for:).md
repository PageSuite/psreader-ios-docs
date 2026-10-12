<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AssetDelegate/imageResource(for:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13AssetDelegateP13imageResource3forSo7UIImageCSgAA05ImageE4NameO_tF"
  },
  "title" : "imageResource(for:)"
}
-->

# imageResource(for:)

Provides a custom image for the specified asset used in the SDK.

```
func imageResource(for name: ImageResourceName) -> UIImage?
```

## Parameters

`name`

The identifier for the requested image resource.

## Return Value

A custom image. Returning `nil` doesn’t restore the default:
the reader leaves out a navigation bar button whose icon is `nil`, and
the date picker drops its calendar icon. Return
[`defaultImage()`](/documentation/PSReader/ImageResourceName/defaultImage()) to keep the built-in image.

## Discussion

Default implementation uses SDKs default assets.