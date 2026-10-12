<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionReaderViewController/CommentingDelegate-swift.protocol/commentButtonView(forArticle:onTap:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29PSEditionReaderViewControllerC18CommentingDelegateP013commentButtonD010forArticle5onTapSo6UIViewCSgAA10PSEArticleC_yyctF"
  },
  "title" : "commentButtonView(forArticle:onTap:)"
}
-->

# commentButtonView(forArticle:onTap:)

The button view to embed for an article, or `nil` for none. Call
`onTap` from the view’s action to trigger
[`commentButtonTapped(forArticle:onPage:from:)`](/documentation/PSReader/PSEditionReaderViewController/CommentingDelegate-swift.protocol/commentButtonTapped(forArticle:onPage:from:)).

```
func commentButtonView(forArticle article: PSEArticle, onTap: @escaping () -> Void) -> UIView?
```