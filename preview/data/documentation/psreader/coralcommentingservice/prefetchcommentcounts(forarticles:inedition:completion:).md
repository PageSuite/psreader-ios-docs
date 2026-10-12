<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CoralCommentingService/prefetchCommentCounts(forArticles:inEdition:completion:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22CoralCommentingServiceC21prefetchCommentCounts11forArticles9inEdition10completionySayAA10PSEArticleCG_AA16PSEEditionSource_pys6ResultOySDySSSiGs5Error_pGcSgtF"
  },
  "title" : "prefetchCommentCounts(forArticles:inEdition:completion:)"
}
-->

# prefetchCommentCounts(forArticles:inEdition:completion:)

Fetches comment counts for several articles from Coral.

```
func prefetchCommentCounts(forArticles articles: [PSEArticle], inEdition source: PSEEditionSource, completion: ((Result<[String : Int], Error>) -> Void)?)
```

## Parameters

`articles`

The articles to fetch counts for.

`source`

The edition containing the articles.

`completion`

Called with the counts keyed by article identifier, or
`nil` for a fire-and-forget prefetch.

## Discussion

Requests the counts for the articles’ [`articleIdentifier(for:)`](/documentation/PSReader/CoralCommentingService/articleIdentifier(for:))
values in batches of 50, skipping articles with no identifier. A batch
that fails is left out of the results rather than failing the whole
request, so the completion handler always receives `.success`.