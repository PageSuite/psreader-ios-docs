<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CommentingDelegate",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18CommentingDelegateP"
  },
  "title" : "CommentingDelegate"
}
-->

# CommentingDelegate

Extends [`CommentingService`](/documentation/PSReader/CommentingService) with UI responsibilities for the commenting system.

```
protocol CommentingDelegate : CommentingService
```

## Overview

You do not typically implement this protocol directly. Instead, create a
[`CommentingService`](/documentation/PSReader/CommentingService) and pass it to [`DefaultCommentingProvider`](/documentation/PSReader/DefaultCommentingProvider), which
provides a complete implementation including a default comment button,
tooltips, and comment-count caching.

## Quick Start

```swift
let service = CoralCommentingService(domain: "talk.example.com")

let provider = DefaultCommentingProvider(
    globalConfig: globalConfig,
    service: service,
    onCommentButtonTapped: { article, page, edition, viewController in
        // Present your commenting UI
    }
)

globalConfig.commentingDelegate = provider
```

To set up commenting in the prebuilt reader, see [Commenting](/documentation/PSReader/Commenting).

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/CommentingService``

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/DefaultCommentingProvider``

## Topics

### Providing the Comment Button

[`commentButton(forArticle:inEdition:onTap:)`](/documentation/PSReader/CommentingDelegate/commentButton(forArticle:inEdition:onTap:))

Provides a comment button view for the given article.

[`commentButtonTapped(forArticle:onPage:inEdition:from:)`](/documentation/PSReader/CommentingDelegate/commentButtonTapped(forArticle:onPage:inEdition:from:))

Called when the user taps a comment button.

### Counting Comments

[`fetchCommentCount(forArticle:inEdition:cacheStrategy:completion:)`](/documentation/PSReader/CommentingDelegate/fetchCommentCount(forArticle:inEdition:cacheStrategy:completion:))

Fetches the comment count for a single article using the given cache strategy.

[`clearCache()`](/documentation/PSReader/CommentingDelegate/clearCache())

Removes all cached comment counts.

[`trendingThreshold`](/documentation/PSReader/CommentingDelegate/trendingThreshold)

The comment count at which the trending icon appears in the content browser.

[`CommentingError`](/documentation/PSReader/CommentingError)

Errors produced by [`DefaultCommentingProvider`](/documentation/PSReader/DefaultCommentingProvider) during comment-count operations.

### Showing Tooltips

[`articleCommentTooltipViewController(inEdition:)`](/documentation/PSReader/CommentingDelegate/articleCommentTooltipViewController(inEdition:))

Returns a view controller to present as a popover tooltip above the
comment button in the article view.

[`contentBrowserCommentTooltipViewController(inEdition:)`](/documentation/PSReader/CommentingDelegate/contentBrowserCommentTooltipViewController(inEdition:))

Returns a view controller to present as a popover tooltip anchored to
commenting icons in the content browser.

