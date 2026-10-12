<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionReaderViewController/CommentingDelegate-swift.protocol/fetchCommentCount(forArticle:completion:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29PSEditionReaderViewControllerC18CommentingDelegateP17fetchCommentCount10forArticle10completionyAA10PSEArticleC_ySiSgctF"
  },
  "title" : "fetchCommentCount(forArticle:completion:)"
}
-->

# fetchCommentCount(forArticle:completion:)

Fetches the article’s comment count for display on the button;
pass `nil` to the completion when unavailable.

```
func fetchCommentCount(forArticle article: PSEArticle, completion: @escaping (Int?) -> Void)
```