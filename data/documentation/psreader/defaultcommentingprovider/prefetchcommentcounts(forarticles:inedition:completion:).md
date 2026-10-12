<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultCommentingProvider/prefetchCommentCounts(forArticles:inEdition:completion:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader25DefaultCommentingProviderC21prefetchCommentCounts11forArticles9inEdition10completionySayAA10PSEArticleCG_AA16PSEEditionSource_pys6ResultOySDySSSiGs5Error_pGcSgtF"
  },
  "title" : "prefetchCommentCounts(forArticles:inEdition:completion:)"
}
-->

# prefetchCommentCounts(forArticles:inEdition:completion:)

Fetches and caches comment counts for the articles that support
commenting.

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

Skips articles that [`service`](/documentation/PSReader/DefaultCommentingProvider/service) can’t identify or has commenting
disabled for, asks the service for the rest in one call, and stores
the returned counts in the cache. If no article qualifies, the
completion handler receives an empty dictionary straight away;
otherwise it runs on the main queue once the service finishes.