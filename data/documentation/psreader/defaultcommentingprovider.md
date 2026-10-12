<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultCommentingProvider",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader25DefaultCommentingProviderC"
  },
  "title" : "DefaultCommentingProvider"
}
-->

# DefaultCommentingProvider

A ready-made [`CommentingDelegate`](/documentation/PSReader/CommentingDelegate) that wraps any [`CommentingService`](/documentation/PSReader/CommentingService).

```
class DefaultCommentingProvider
```

## Overview

`DefaultCommentingProvider` delegates data-fetching to an injected
[`CommentingService`](/documentation/PSReader/CommentingService), manages a local comment-count cache, and provides
default UI components: a [`DefaultCommentingButton`](/documentation/PSReader/DefaultCommentingButton) and
[`DefaultCommentTooltipViewController`](/documentation/PSReader/DefaultCommentTooltipViewController) instances for both the article view
and content browser.

Tooltips are shown once per app install. The provider tracks presentation
state in `UserDefaults` and returns `nil` on subsequent calls.

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

## Customization

This is an `open class` — override any method to customize a single aspect
while inheriting the rest. For example, override
[`commentButton(forArticle:inEdition:onTap:)`](/documentation/PSReader/DefaultCommentingProvider/commentButton(forArticle:inEdition:onTap:)) to provide a custom button
while keeping the default tooltip and caching behavior.

To turn on commenting in the prebuilt reader, see [Commenting](/documentation/PSReader/Commenting); to
use the provider in your own reader screen, see
[Adding Comment Buttons](/documentation/PSReader/Adding-Comment-Buttons).

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/CommentingService``

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/CommentingDelegate``

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/CoralCommentingService``

## Topics

### Creating a Provider

[`init(globalConfig:service:trendingThreshold:onCommentButtonTapped:)`](/documentation/PSReader/DefaultCommentingProvider/init(globalConfig:service:trendingThreshold:onCommentButtonTapped:))

Creates a new commenting provider using global SDK settings.

[`init(service:accentColor:fontFamily:trendingThreshold:onCommentButtonTapped:)`](/documentation/PSReader/DefaultCommentingProvider/init(service:accentColor:fontFamily:trendingThreshold:onCommentButtonTapped:))

Creates a new commenting provider with explicit styling.

### Handling Comment Taps

[`onCommentButtonTapped`](/documentation/PSReader/DefaultCommentingProvider/onCommentButtonTapped)

Called when the user taps a comment button (native or template-based).

[`commentButtonTapped(forArticle:onPage:inEdition:from:)`](/documentation/PSReader/DefaultCommentingProvider/commentButtonTapped(forArticle:onPage:inEdition:from:))

Forwards the tap to [`onCommentButtonTapped`](/documentation/PSReader/DefaultCommentingProvider/onCommentButtonTapped).

### Providing the Comment Button

[`commentButton(forArticle:inEdition:onTap:)`](/documentation/PSReader/DefaultCommentingProvider/commentButton(forArticle:inEdition:onTap:))

Returns a [`DefaultCommentingButton`](/documentation/PSReader/DefaultCommentingButton) styled with [`accentColor`](/documentation/PSReader/DefaultCommentingProvider/accentColor) and [`fontFamily`](/documentation/PSReader/DefaultCommentingProvider/fontFamily).

[`accentColor`](/documentation/PSReader/DefaultCommentingProvider/accentColor)

The accent color used for interactive commenting UI elements.

[`fontFamily`](/documentation/PSReader/DefaultCommentingProvider/fontFamily)

The font family used for commenting UI labels.

### Checking Articles

[`service`](/documentation/PSReader/DefaultCommentingProvider/service)

The data service used to fetch comment counts.

[`isCommentingEnabled(article:inEdition:)`](/documentation/PSReader/DefaultCommentingProvider/isCommentingEnabled(article:inEdition:))

Returns whether commenting is enabled for the article, as decided by
[`service`](/documentation/PSReader/DefaultCommentingProvider/service).

[`articleIdentifier(for:)`](/documentation/PSReader/DefaultCommentingProvider/articleIdentifier(for:))

Returns the article’s identifier from [`service`](/documentation/PSReader/DefaultCommentingProvider/service).

### Counting Comments

[`fetchCommentCount(forArticle:inEdition:completion:)`](/documentation/PSReader/DefaultCommentingProvider/fetchCommentCount(forArticle:inEdition:completion:))

Fetches the article’s comment count with the
[`CommentingCacheStrategy.preferNetwork`](/documentation/PSReader/CommentingCacheStrategy/preferNetwork) strategy.

[`fetchCommentCount(forArticle:inEdition:cacheStrategy:completion:)`](/documentation/PSReader/DefaultCommentingProvider/fetchCommentCount(forArticle:inEdition:cacheStrategy:completion:))

Fetches the article’s comment count through [`service`](/documentation/PSReader/DefaultCommentingProvider/service), using the
local cache as `cacheStrategy` directs.

[`prefetchCommentCounts(forArticles:inEdition:completion:)`](/documentation/PSReader/DefaultCommentingProvider/prefetchCommentCounts(forArticles:inEdition:completion:))

Fetches and caches comment counts for the articles that support
commenting.

[`cachedCommentCount(for:)`](/documentation/PSReader/DefaultCommentingProvider/cachedCommentCount(for:))

Returns the cached comment count for an article, or `nil` if not yet fetched.

[`clearCache()`](/documentation/PSReader/DefaultCommentingProvider/clearCache())

Removes all cached comment counts.

[`trendingThreshold`](/documentation/PSReader/DefaultCommentingProvider/trendingThreshold)

The comment count at which the trending icon appears in the content browser.

### Showing Tooltips

[`articleCommentTooltipViewController(inEdition:)`](/documentation/PSReader/DefaultCommentingProvider/articleCommentTooltipViewController(inEdition:))

Returns a [`DefaultCommentTooltipViewController`](/documentation/PSReader/DefaultCommentTooltipViewController) for the article view.

[`contentBrowserCommentTooltipViewController(inEdition:)`](/documentation/PSReader/DefaultCommentingProvider/contentBrowserCommentTooltipViewController(inEdition:))

Returns a [`DefaultCommentTooltipViewController`](/documentation/PSReader/DefaultCommentTooltipViewController) for the content browser.

