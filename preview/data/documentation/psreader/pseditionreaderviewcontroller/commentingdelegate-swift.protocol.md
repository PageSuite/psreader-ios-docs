<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionReaderViewController/CommentingDelegate-swift.protocol",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29PSEditionReaderViewControllerC18CommentingDelegateP"
  },
  "title" : "PSEditionReaderViewController.CommentingDelegate"
}
-->

# PSEditionReaderViewController.CommentingDelegate

Integrates an article-commenting system into the reader’s pages.

```
protocol CommentingDelegate : AnyObject
```

## Overview

When commenting is enabled for an article, the reader places the
delegate’s button view in the article layout and routes taps back
with the presentation context.

To add comment buttons with it, see [Adding Comment Buttons](/documentation/PSReader/Adding-Comment-Buttons).

## Topics

### Showing the Comment Button

[`isCommentingEnabled(article:)`](/documentation/PSReader/PSEditionReaderViewController/CommentingDelegate-swift.protocol/isCommentingEnabled(article:))

Whether the commenting affordance should appear for an article.

[`commentButtonView(forArticle:onTap:)`](/documentation/PSReader/PSEditionReaderViewController/CommentingDelegate-swift.protocol/commentButtonView(forArticle:onTap:))

The button view to embed for an article, or `nil` for none. Call
`onTap` from the view’s action to trigger
[`commentButtonTapped(forArticle:onPage:from:)`](/documentation/PSReader/PSEditionReaderViewController/CommentingDelegate-swift.protocol/commentButtonTapped(forArticle:onPage:from:)).

[`fetchCommentCount(forArticle:completion:)`](/documentation/PSReader/PSEditionReaderViewController/CommentingDelegate-swift.protocol/fetchCommentCount(forArticle:completion:))

Fetches the article’s comment count for display on the button;
pass `nil` to the completion when unavailable.

[`articleCommentTooltipViewController()`](/documentation/PSReader/PSEditionReaderViewController/CommentingDelegate-swift.protocol/articleCommentTooltipViewController())

A tooltip introducing commenting, presented as a popover anchored
to the comment button, or `nil` for none. The reader asks each
time an article page with a comment button appears, so return
`nil` once the user has seen it.

### Handling Taps

[`commentButtonTapped(forArticle:onPage:from:)`](/documentation/PSReader/PSEditionReaderViewController/CommentingDelegate-swift.protocol/commentButtonTapped(forArticle:onPage:from:))

Called when the user taps the comment button. Present your
commenting UI from `viewController`.

