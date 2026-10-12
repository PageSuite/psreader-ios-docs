<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AudioDelegate/audioBannerViewController()",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13AudioDelegateP25audioBannerViewControllerAA0befG0_pSgyF"
  },
  "title" : "audioBannerViewController()"
}
-->

# audioBannerViewController()

Provides a persistent banner view controller for audio controls.

```
func audioBannerViewController() -> AudioBannerViewController?
```

## Return Value

A `AudioBannerViewController` to display as a persistent banner, or `nil`
if no persistent banner should be shown.

## Discussion

This method should return a view controller that will be displayed as a persistent
banner in the reading interface. The banner’s visibility is controlled by its
intrinsic content size — return zero height to hide the banner.

Layout is determined by the returned controller’s `isFloating` property:

- When `true`, the banner floats above the reader content pinned to the bottom edge.
  The SDK applies matching bottom insets to the content so it is not obscured.
- When `false`, the banner is stacked below the reader, reducing the reader’s
  available height.

This approach is ideal for showing persistent audio controls that remain visible
as users navigate through content.