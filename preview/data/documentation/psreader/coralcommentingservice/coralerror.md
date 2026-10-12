<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CoralCommentingService/CoralError",
  "metadataVersion" : "0.1.0",
  "role" : "Enumeration",
  "symbol" : {
    "kind" : "Enumeration",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22CoralCommentingServiceC0B5ErrorO"
  },
  "title" : "CoralCommentingService.CoralError"
}
-->

# CoralCommentingService.CoralError

Errors [`CoralCommentingService`](/documentation/PSReader/CoralCommentingService) reports when it can’t fetch a
comment count.

```
enum CoralError
```

## Topics

### Errors

[`CoralCommentingService.CoralError.noURL`](/documentation/PSReader/CoralCommentingService/CoralError/noURL)

The article has no Coral identifier, or
[`commentCountURL(for:)`](/documentation/PSReader/CoralCommentingService/commentCountURL(for:)) returned `nil`.

[`CoralCommentingService.CoralError.invalidResponse`](/documentation/PSReader/CoralCommentingService/CoralError/invalidResponse)

Coral’s response was empty, wasn’t a JSON object of counts, or had
no count for the article.

### Describing the Error

[`errorDescription`](/documentation/PSReader/CoralCommentingService/CoralError/errorDescription)

A short English description of the error.

