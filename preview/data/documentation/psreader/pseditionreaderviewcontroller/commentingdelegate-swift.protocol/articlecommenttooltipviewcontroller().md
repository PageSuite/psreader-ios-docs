<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionReaderViewController/CommentingDelegate-swift.protocol/articleCommentTooltipViewController()",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29PSEditionReaderViewControllerC18CommentingDelegateP021articleCommentTooltipdE0So06UIViewE0CSgyF"
  },
  "title" : "articleCommentTooltipViewController()"
}
-->

# articleCommentTooltipViewController()

A tooltip introducing commenting, presented as a popover anchored
to the comment button, or `nil` for none. The reader asks each
time an article page with a comment button appears, so return
`nil` once the user has seen it.

```
func articleCommentTooltipViewController() -> UIViewController?
```