<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AssetDelegate/placeholderImage(size:with:completion:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13AssetDelegateP16placeholderImage4size4with10completionySo6CGSizeV_So17UITraitCollectionCySo7UIImageCSgctF"
  },
  "title" : "placeholderImage(size:with:completion:)"
}
-->

# placeholderImage(size:with:completion:)

Provides a placeholder image for content that is unavailable.

```
func placeholderImage(size: CGSize, with traits: UITraitCollection, completion: @escaping (UIImage?) -> Void)
```

## Parameters

`size`

The desired size of the placeholder image.

`traits`

The current trait collection (such as display scale, user interface style, etc.)
that can be used to generate an appropriate placeholder.

`completion`

A closure to call with the generated placeholder image, or `nil` to leave the
current placeholder presentation unchanged.

## Discussion

If no custom placeholder is provided, the SDK displays a solid skeleton view
(a gray box that adapts to light or dark mode) as the default placeholder.