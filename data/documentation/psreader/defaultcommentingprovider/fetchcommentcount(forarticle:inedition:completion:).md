<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultCommentingProvider/fetchCommentCount(forArticle:inEdition:completion:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader25DefaultCommentingProviderC17fetchCommentCount10forArticle9inEdition10completionyAA10PSEArticleC_AA16PSEEditionSource_pys6ResultOySis5Error_pGctF"
  },
  "title" : "fetchCommentCount(forArticle:inEdition:completion:)"
}
-->

# fetchCommentCount(forArticle:inEdition:completion:)

Fetches the article’s comment count with the
[`CommentingCacheStrategy.preferNetwork`](/documentation/PSReader/CommentingCacheStrategy/preferNetwork) strategy.

```
func fetchCommentCount(forArticle article: PSEArticle, inEdition source: PSEEditionSource, completion: @escaping (Result<Int, Error>) -> Void)
```

## Parameters

`article`

The article to fetch the count for.

`source`

The edition containing the article.

`completion`

Called with the result.