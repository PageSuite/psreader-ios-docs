<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SearchConfiguration/assetDelegate",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19SearchConfigurationV13assetDelegateAA05AssetE0_pvp"
  },
  "title" : "assetDelegate"
}
-->

# assetDelegate

Delegate providing custom images used within the search view.

```
var assetDelegate: AssetDelegate
```

## Discussion

Used to supply placeholder images for result cells when thumbnails are unavailable.
If the delegate’s [`placeholderImage(size:with:completion:)`](/documentation/PSReader/AssetDelegate/placeholderImage(size:with:completion:)) returns `nil`,
the current placeholder presentation is left unchanged.