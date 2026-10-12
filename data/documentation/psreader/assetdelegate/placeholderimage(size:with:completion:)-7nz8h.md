<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AssetDelegate/placeholderImage(size:with:completion:)-7nz8h",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13AssetDelegatePAAE16placeholderImage4size4with10completionySo6CGSizeV_So17UITraitCollectionCySo7UIImageCSgctF"
  },
  "title" : "placeholderImage(size:with:completion:)"
}
-->

# placeholderImage(size:with:completion:)

Calls `completion` with `nil`, so the SDK keeps showing its default
skeleton placeholder.

```
func placeholderImage(size: CGSize, with traits: UITraitCollection, completion: @escaping (UIImage?) -> Void)
```

## Parameters

`size`

The desired size of the placeholder image.

`traits`

The current trait collection.

`completion`

The closure to call with the placeholder image.