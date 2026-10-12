<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionReaderViewController/currentPageIndex()",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29PSEditionReaderViewControllerC16currentPageIndexSiSgyF"
  },
  "title" : "currentPageIndex()"
}
-->

# currentPageIndex()

The index of the current reference page within `edition.pages`
(page-level, unlike [`PSEditionReaderViewController.ScrollDelegate`](/documentation/PSReader/PSEditionReaderViewController/ScrollDelegate-swift.protocol)’s spread indices), or `nil`
when no edition is open.

```
@MainActor func currentPageIndex() -> Int?
```