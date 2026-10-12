<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultCommentingProvider/fetchCommentCount(forArticle:inEdition:cacheStrategy:completion:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader25DefaultCommentingProviderC17fetchCommentCount10forArticle9inEdition13cacheStrategy10completionyAA10PSEArticleC_AA16PSEEditionSource_pAA0c5CacheM0Oys6ResultOySis5Error_pGctF"
  },
  "title" : "fetchCommentCount(forArticle:inEdition:cacheStrategy:completion:)"
}
-->

# fetchCommentCount(forArticle:inEdition:cacheStrategy:completion:)

Fetches the article’s comment count through [`service`](/documentation/PSReader/DefaultCommentingProvider/service), using the
local cache as `cacheStrategy` directs.

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

Called with the count or an error. The error is
[`CommentingError.noIdentifier`](/documentation/PSReader/CommentingError/noIdentifier) when the service can’t identify
the article.

## Discussion

A successful fetch updates the cache. If the fetch fails and a cached
count exists, the completion handler receives the cached count instead
of the error. Results from the service arrive on the main queue; a
cached count returned under [`CommentingCacheStrategy.preferCache`](/documentation/PSReader/CommentingCacheStrategy/preferCache)
arrives immediately, on the calling queue.