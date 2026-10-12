<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionReaderViewController/scrollTo(index:source:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29PSEditionReaderViewControllerC8scrollTo5index6sourceySi_ypSgtF"
  },
  "title" : "scrollTo(index:source:)"
}
-->

# scrollTo(index:source:)

Scrolls to the spread at `index` (a spread index in the active
paging mode). The `source` token is echoed to [`PSEditionReaderViewController.ScrollDelegate`](/documentation/PSReader/PSEditionReaderViewController/ScrollDelegate-swift.protocol).

```
@MainActor func scrollTo(index: Int, source: Any? = nil)
```