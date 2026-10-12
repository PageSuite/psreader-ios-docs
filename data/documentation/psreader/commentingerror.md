<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CommentingError",
  "metadataVersion" : "0.1.0",
  "role" : "Enumeration",
  "symbol" : {
    "kind" : "Enumeration",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader15CommentingErrorO"
  },
  "title" : "CommentingError"
}
-->

# CommentingError

Errors produced by [`DefaultCommentingProvider`](/documentation/PSReader/DefaultCommentingProvider) during comment-count operations.

```
enum CommentingError
```

## Overview

These errors are passed to `fetchCommentCount` completion handlers when
the provider cannot fulfill a request.

## Topics

### Errors

[`CommentingError.noIdentifier`](/documentation/PSReader/CommentingError/noIdentifier)

The article has no valid identifier ([`articleIdentifier(for:)`](/documentation/PSReader/CommentingService/articleIdentifier(for:))
returned `nil`), so a comment count cannot be fetched.

### Describing the Error

[`errorDescription`](/documentation/PSReader/CommentingError/errorDescription)

A short English description of the error.

