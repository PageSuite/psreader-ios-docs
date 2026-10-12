<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CommentingService",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader17CommentingServiceP"
  },
  "title" : "CommentingService"
}
-->

# CommentingService

Data provider protocol for fetching comment counts from a backend.

```
protocol CommentingService
```

## Overview

Implement this protocol to connect any commenting backend to the SDK.
A bundled implementation for Coral Talk is provided by [`CoralCommentingService`](/documentation/PSReader/CoralCommentingService).

## Usage

Create a type conforming to this protocol and inject it into a
[`DefaultCommentingProvider`](/documentation/PSReader/DefaultCommentingProvider):

```swift
class MyCommentingService: CommentingService {
    func isCommentingEnabled(article: PSEArticle, inEdition source: PSEEditionSource) -> Bool {
        return article.articleguid != nil
    }

    func articleIdentifier(for article: PSEArticle) -> String? {
        return article.articleguid
    }

    func fetchCommentCount(
        forArticle article: PSEArticle,
        inEdition source: PSEEditionSource,
        completion: @escaping (Result<Int, Error>) -> Void
    ) {
        // Fetch from your backend...
    }

    func prefetchCommentCounts(
        forArticles articles: [PSEArticle],
        inEdition source: PSEEditionSource,
        completion: ((Result<[String: Int], Error>) -> Void)?
    ) {
        // Fetch several counts from your backend...
    }
}

let provider = DefaultCommentingProvider(
    globalConfig: globalConfig,
    service: MyCommentingService(),
    onCommentButtonTapped: { article, page, edition, viewController in
        // Present your commenting UI
    }
)
globalConfig.commentingDelegate = provider
```

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/CommentingDelegate``

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/DefaultCommentingProvider``

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/CoralCommentingService``

## Topics

### Enabling Commenting

[`isCommentingEnabled(article:inEdition:)`](/documentation/PSReader/CommentingService/isCommentingEnabled(article:inEdition:))

Determines whether commenting is enabled for the given article.

[`articleIdentifier(for:)`](/documentation/PSReader/CommentingService/articleIdentifier(for:))

Returns a stable identifier for the article.

### Fetching Comment Counts

[`fetchCommentCount(forArticle:inEdition:completion:)`](/documentation/PSReader/CommentingService/fetchCommentCount(forArticle:inEdition:completion:))

Fetches the comment count for a single article.

[`prefetchCommentCounts(forArticles:inEdition:completion:)`](/documentation/PSReader/CommentingService/prefetchCommentCounts(forArticles:inEdition:completion:))

Fetches comment counts for multiple articles in a single operation.

