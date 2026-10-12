<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CommentingDelegate/fetchCommentCount(forArticle:inEdition:cacheStrategy:completion:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18CommentingDelegateP17fetchCommentCount10forArticle9inEdition13cacheStrategy10completionyAA10PSEArticleC_AA16PSEEditionSource_pAA0b5CacheL0Oys6ResultOySis5Error_pGctF"
  },
  "title" : "fetchCommentCount(forArticle:inEdition:cacheStrategy:completion:)"
}
-->

# fetchCommentCount(forArticle:inEdition:cacheStrategy:completion:)

Fetches the comment count for a single article using the given cache strategy.

```
func fetchCommentCount(forArticle article: PSEArticle, inEdition source: PSEEditionSource, cacheStrategy: CommentingCacheStrategy, completion: @escaping (Result<Int, Error>) -> Void)
```

## Parameters

`article`

The article to fetch the count for.

`source`

The edition containing the article.

`cacheStrategy`

How to resolve the count against the local cache.

`completion`

Handler called with the result.