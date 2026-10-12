<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionReaderViewController/ScrollDelegate-swift.protocol/willScrollTo(pageIndex:pagingMode:source:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29PSEditionReaderViewControllerC14ScrollDelegateP04willF2To9pageIndex10pagingMode6sourceySi_AA0b6PagingM0OypSgtF"
  },
  "title" : "willScrollTo(pageIndex:pagingMode:source:)"
}
-->

# willScrollTo(pageIndex:pagingMode:source:)

Called before the reader moves to a page, whether from a user
swipe or a `scrollTo` call. Programmatic navigation forwards the
`source` token passed to `scrollTo`; user swipes report `nil`.

```
func willScrollTo(pageIndex: Int, pagingMode: PSEditionPagingMode, source: Any?)
```