<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CommentingService/articleIdentifier(for:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader17CommentingServiceP17articleIdentifier3forSSSgAA10PSEArticleC_tF"
  },
  "title" : "articleIdentifier(for:)"
}
-->

# articleIdentifier(for:)

Returns a stable identifier for the article.

```
func articleIdentifier(for article: PSEArticle) -> String?
```

## Parameters

`article`

The article to identify.

## Return Value

A stable string identifier, or `nil`.

## Discussion

Used as the cache key for comment counts and for batch lookups.
Return `nil` if the article cannot be identified;
[`DefaultCommentingProvider`](/documentation/PSReader/DefaultCommentingProvider) then fetches no count for it.