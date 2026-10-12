<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEEdition/pageIndex(for:inPagingMode:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader10PSEEditionC9pageIndex3for12inPagingModeSiSgAA7PSEPageC_AA09PSEditiongH0OtF"
  },
  "title" : "pageIndex(for:inPagingMode:)"
}
-->

# pageIndex(for:inPagingMode:)

The spread index presenting `page` in a paging mode, or `nil` if the
page isn’t in the edition.

```
func pageIndex(for page: PSEPage, inPagingMode pagingMode: PSEditionPagingMode) -> Int?
```

## Discussion

Use this to translate page-level state into the spread indices the
reader navigates by — for example, highlighting the current row in a
page browser while in double-page mode.