<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionReaderViewController/currentPage()",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29PSEditionReaderViewControllerC11currentPageAA7PSEPageCSgyF"
  },
  "title" : "currentPage()"
}
-->

# currentPage()

The current spread’s reference page (in double-page mode, the page
that best represents the spread), or `nil` when no edition is open.

```
@MainActor func currentPage() -> PSEPage?
```

## Discussion

[`open(edition:openingPage:application:)`](/documentation/PSReader/PSEditionReaderViewController/open(edition:openingPage:application:)) settles the reader on its
opening page before it returns, so straight after that call this is
the opening page.