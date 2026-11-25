<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionReaderViewController/AdvertDelegate-swift.protocol/canRenderAdvertPage(_:)-8w6zl",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29PSEditionReaderViewControllerC14AdvertDelegatePAAE09canRenderF4PageySbAA7PSEPageCF"
  },
  "title" : "canRenderAdvertPage(_:)"
}
-->

# canRenderAdvertPage(_:)

The delegate can render the page if `advertViewController(forPage:)`
supplies a view controller for it. The view controller is discarded.

```
func canRenderAdvertPage(_ page: PSEPage) -> Bool
```