<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEBookmarkManager/isBookmarked(spread:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18PSEBookmarkManagerC12isBookmarked6spreadSbSgAA13PSEPageSpreadO_tF"
  },
  "title" : "isBookmarked(spread:)"
}
-->

# isBookmarked(spread:)

The spread’s bookmark state, or nil when it holds no bookmarkable
pages (e.g. an advert-only spread). True only when every
bookmarkable page in the spread is bookmarked.

```
func isBookmarked(spread: PSEPageSpread) -> Bool?
```