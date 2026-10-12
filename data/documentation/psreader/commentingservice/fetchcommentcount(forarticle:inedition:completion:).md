<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CommentingService/fetchCommentCount(forArticle:inEdition:completion:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader17CommentingServiceP17fetchCommentCount10forArticle9inEdition10completionyAA10PSEArticleC_AA16PSEEditionSource_pys6ResultOySis5Error_pGctF"
  },
  "title" : "fetchCommentCount(forArticle:inEdition:completion:)"
}
-->

# fetchCommentCount(forArticle:inEdition:completion:)

Fetches the comment count for a single article.

```
func fetchCommentCount(forArticle article: PSEArticle, inEdition source: PSEEditionSource, completion: @escaping (Result<Int, Error>) -> Void)
```

## Parameters

`article`

The article to fetch the count for.

`source`

The edition containing the article.

`completion`

Handler called with the result.

## Discussion

Call the completion handler with `.success(count)` or `.failure(error)`.
Does not need to dispatch to the main thread — [`DefaultCommentingProvider`](/documentation/PSReader/DefaultCommentingProvider)
handles that.