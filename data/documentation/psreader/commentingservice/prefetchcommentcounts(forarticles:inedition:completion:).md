<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CommentingService/prefetchCommentCounts(forArticles:inEdition:completion:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader17CommentingServiceP21prefetchCommentCounts11forArticles9inEdition10completionySayAA10PSEArticleCG_AA16PSEEditionSource_pys6ResultOySDySSSiGs5Error_pGcSgtF"
  },
  "title" : "prefetchCommentCounts(forArticles:inEdition:completion:)"
}
-->

# prefetchCommentCounts(forArticles:inEdition:completion:)

Fetches comment counts for multiple articles in a single operation.

```
func prefetchCommentCounts(forArticles articles: [PSEArticle], inEdition source: PSEEditionSource, completion: ((Result<[String : Int], Error>) -> Void)?)
```

## Parameters

`articles`

The articles to fetch counts for.

`source`

The edition containing the articles.

`completion`

Handler called with the aggregated results, or `nil` for fire-and-forget.

## Discussion

The completion dictionary is keyed by the value returned from
[`articleIdentifier(for:)`](/documentation/PSReader/CommentingService/articleIdentifier(for:)). Pass `nil` for the completion to use
this as a fire-and-forget prefetch.