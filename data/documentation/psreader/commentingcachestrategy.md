<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CommentingCacheStrategy",
  "metadataVersion" : "0.1.0",
  "role" : "Enumeration",
  "symbol" : {
    "kind" : "Enumeration",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader23CommentingCacheStrategyO"
  },
  "title" : "CommentingCacheStrategy"
}
-->

# CommentingCacheStrategy

Controls how [`fetchCommentCount(forArticle:inEdition:cacheStrategy:completion:)`](/documentation/PSReader/CommentingDelegate/fetchCommentCount(forArticle:inEdition:cacheStrategy:completion:))
resolves comment counts against the local cache.

```
enum CommentingCacheStrategy
```

## Topics

### Strategies

[`CommentingCacheStrategy.preferNetwork`](/documentation/PSReader/CommentingCacheStrategy/preferNetwork)

Always fetch from the network and update the cache. Falls back to a
cached value if the network request fails.

[`CommentingCacheStrategy.preferCache`](/documentation/PSReader/CommentingCacheStrategy/preferCache)

Return the cached count immediately if available; fetch from the
network only on a cache miss.

