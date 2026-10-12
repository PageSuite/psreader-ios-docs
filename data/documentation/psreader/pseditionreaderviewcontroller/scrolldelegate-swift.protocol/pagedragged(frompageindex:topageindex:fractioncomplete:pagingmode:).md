<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionReaderViewController/ScrollDelegate-swift.protocol/pageDragged(fromPageIndex:toPageIndex:fractionComplete:pagingMode:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29PSEditionReaderViewControllerC14ScrollDelegateP11pageDragged13fromPageIndex02tokL016fractionComplete10pagingModeySi_Si14CoreFoundation7CGFloatVAA0b6PagingQ0OtF"
  },
  "title" : "pageDragged(fromPageIndex:toPageIndex:fractionComplete:pagingMode:)"
}
-->

# pageDragged(fromPageIndex:toPageIndex:fractionComplete:pagingMode:)

Called continuously while the user drags between pages, with
`fractionComplete` running 0…1.

```
func pageDragged(fromPageIndex fromIndex: Int, toPageIndex toIndex: Int, fractionComplete: CGFloat, pagingMode: PSEditionPagingMode)
```