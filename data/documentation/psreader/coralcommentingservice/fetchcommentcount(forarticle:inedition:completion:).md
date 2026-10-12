<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CoralCommentingService/fetchCommentCount(forArticle:inEdition:completion:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22CoralCommentingServiceC17fetchCommentCount10forArticle9inEdition10completionyAA10PSEArticleC_AA16PSEEditionSource_pys6ResultOySis5Error_pGctF"
  },
  "title" : "fetchCommentCount(forArticle:inEdition:completion:)"
}
-->

# fetchCommentCount(forArticle:inEdition:completion:)

Fetches the article’s comment count from Coral.

```
func fetchCommentCount(forArticle article: PSEArticle, inEdition source: PSEEditionSource, completion: @escaping (Result<Int, Error>) -> Void)
```

## Parameters

`article`

The article to fetch the count for.

`source`

The edition containing the article.

`completion`

Called with the count, or with an error:
[`CoralCommentingService.CoralError.noURL`](/documentation/PSReader/CoralCommentingService/CoralError/noURL) or [`CoralCommentingService.CoralError.invalidResponse`](/documentation/PSReader/CoralCommentingService/CoralError/invalidResponse), or the
network error.

## Discussion

Requests [`commentCountURL(for:)`](/documentation/PSReader/CoralCommentingService/commentCountURL(for:)) and reads the count stored under the
article’s [`articleIdentifier(for:)`](/documentation/PSReader/CoralCommentingService/articleIdentifier(for:)) in the JSON response. The
completion handler can run on a background queue;
[`DefaultCommentingProvider`](/documentation/PSReader/DefaultCommentingProvider) delivers results on the main queue.