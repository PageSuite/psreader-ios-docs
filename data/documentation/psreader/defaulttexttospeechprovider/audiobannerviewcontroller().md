<!--
{
  "availability" : [
    "iOS: 13.0.0 -",
    "iPadOS: 13.0.0 -",
    "macCatalyst: 13.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultTextToSpeechProvider/audioBannerViewController()",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader27DefaultTextToSpeechProviderC25audioBannerViewControllerAA05AudiohiJ0_pSgyF"
  },
  "title" : "audioBannerViewController()"
}
-->

# audioBannerViewController()

Returns the persistent banner view controller.

```
func audioBannerViewController() -> AudioBannerViewController?
```

## Return Value

Always returns `nil` as this provider uses overlay-based UI.

## Discussion

This implementation does not provide a persistent banner interface,
instead relying on the transient overlay approach.