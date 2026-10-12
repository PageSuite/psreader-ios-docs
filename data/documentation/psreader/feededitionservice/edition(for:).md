<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/FeedEditionService/edition(for:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18FeedEditionServiceV7edition3forAA10PSEEditionCAA12PSEPublishedC_tYaKF"
  },
  "title" : "edition(for:)"
}
-->

# edition(for:)

Loads the full content of a published edition, including its
templates. For reading, present the edition through the SDK’s reader
view controllers rather than consuming this directly.

```
func edition(for published: PSEPublished) async throws -> PSEEdition
```