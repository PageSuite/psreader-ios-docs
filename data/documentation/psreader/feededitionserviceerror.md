<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/FeedEditionServiceError",
  "metadataVersion" : "0.1.0",
  "role" : "Enumeration",
  "symbol" : {
    "kind" : "Enumeration",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader23FeedEditionServiceErrorO"
  },
  "title" : "FeedEditionServiceError"
}
-->

# FeedEditionServiceError

Errors thrown by [`FeedEditionService`](/documentation/PSReader/FeedEditionService).

```
enum FeedEditionServiceError
```

## Topics

### Errors

[`FeedEditionServiceError.publicationNotFound`](/documentation/PSReader/FeedEditionServiceError/publicationNotFound)

The backend does not recognize the publication GUID.

[`FeedEditionServiceError.editionNotFound`](/documentation/PSReader/FeedEditionServiceError/editionNotFound)

No published edition matched the request.

[`FeedEditionServiceError.invalidResponse`](/documentation/PSReader/FeedEditionServiceError/invalidResponse)

The backend rejected the request or returned a response the service
could not read.

