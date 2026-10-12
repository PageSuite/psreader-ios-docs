<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionReaderViewController/AdvertDelegate-swift.protocol/advertViewController(forPage:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29PSEditionReaderViewControllerC14AdvertDelegateP06advertdE07forPageAA016PSEAdvertContentdE0_pSgAA7PSEPageC_tF"
  },
  "title" : "advertViewController(forPage:)"
}
-->

# advertViewController(forPage:)

The view controller to render an advert page, or `nil` to accept
the built-in rendering. To render nothing for a page, return an
empty view controller.

```
func advertViewController(forPage page: PSEPage) -> PSEAdvertContentViewController?
```