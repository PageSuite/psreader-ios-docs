<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CoralCommentingService",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22CoralCommentingServiceC"
  },
  "title" : "CoralCommentingService"
}
-->

# CoralCommentingService

A [`CommentingService`](/documentation/PSReader/CommentingService) implementation for
[Coral Talk](https://coralproject.net/).

```
class CoralCommentingService
```

## Overview

Fetches comment counts from Coral’s `/api/v1/comments-count` endpoint.
Supports both single-article and batch lookups (batched in groups of 50).

## Quick Start

```swift
let service = CoralCommentingService(domain: "talk.example.com")

let provider = DefaultCommentingProvider(
    globalConfig: globalConfig,
    service: service,
    onCommentButtonTapped: { article, page, edition, viewController in
        // Present your Coral comment view
    }
)

globalConfig.commentingDelegate = provider
```

## Article Identifier

[`articleIdentifier(for:)`](/documentation/PSReader/CoralCommentingService/articleIdentifier(for:)) returns the article’s
`metadata.coralCommenting.assetId`. Override this method if your
publication uses a different field as the Coral asset ID.

## Customization

This is an `open class` — override any method to customize behavior:

- ``doc://com.pagesuite.PSReader/documentation/PSReader/CoralCommentingService/isCommentingEnabled(article:inEdition:)`` to change which articles
  support comments.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/CoralCommentingService/articleIdentifier(for:)`` to use a different article property as the
  Coral asset ID.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/CoralCommentingService/commentCountURL(for:)`` or ``doc://com.pagesuite.PSReader/documentation/PSReader/CoralCommentingService/commentCountURL(forIDs:)`` to modify
  the API endpoint.

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/CommentingService``

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/DefaultCommentingProvider``

## Topics

### Creating a Service

[`init(domain:)`](/documentation/PSReader/CoralCommentingService/init(domain:))

Creates a new Coral commenting service.

[`domain`](/documentation/PSReader/CoralCommentingService/domain)

The Coral Talk server domain (for example, `"talk.example.com"`).

### Enabling Commenting

[`isCommentingEnabled(article:inEdition:)`](/documentation/PSReader/CoralCommentingService/isCommentingEnabled(article:inEdition:))

Returns whether the article has Coral commenting turned on.

[`articleIdentifier(for:)`](/documentation/PSReader/CoralCommentingService/articleIdentifier(for:))

Returns the article’s Coral asset ID.

### Fetching Comment Counts

[`fetchCommentCount(forArticle:inEdition:completion:)`](/documentation/PSReader/CoralCommentingService/fetchCommentCount(forArticle:inEdition:completion:))

Fetches the article’s comment count from Coral.

[`prefetchCommentCounts(forArticles:inEdition:completion:)`](/documentation/PSReader/CoralCommentingService/prefetchCommentCounts(forArticles:inEdition:completion:))

Fetches comment counts for several articles from Coral.

[`commentCountURL(for:)`](/documentation/PSReader/CoralCommentingService/commentCountURL(for:))

Builds the comment count URL for a single article.

[`commentCountURL(forIDs:)`](/documentation/PSReader/CoralCommentingService/commentCountURL(forIDs:))

Builds the comment count URL for a comma-separated list of IDs.

### Errors

[`CoralCommentingService.CoralError`](/documentation/PSReader/CoralCommentingService/CoralError)

Errors [`CoralCommentingService`](/documentation/PSReader/CoralCommentingService) reports when it can’t fetch a
comment count.

