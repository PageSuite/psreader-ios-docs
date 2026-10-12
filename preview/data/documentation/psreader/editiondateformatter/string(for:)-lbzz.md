<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/EditionDateFormatter/string(for:)-lbzz",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader20EditionDateFormatterP6string3forSSAA15PSEBookmarkPageC_tF"
  },
  "title" : "string(for:)"
}
-->

# string(for:)

Provides a formatted string representation for a bookmarked page.

```
func string(for bookmark: PSEBookmarkPage) -> String
```

## Parameters

`bookmark`

The `PSEBookmarkPage` object to format.

## Return Value

A formatted string for the edition.

## Discussion

You may choose to format bookmarks based on their publish date, edition names,
or any custom naming strategy suitable for your publication.