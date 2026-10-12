<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEDownloadedEdition/open(published:)",
  "metadataVersion" : "0.1.0",
  "role" : "Type Method",
  "symbol" : {
    "kind" : "Type Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader20PSEDownloadedEditionV4open9publishedAcA12PSEPublishedC_tYaKFZ"
  },
  "title" : "open(published:)"
}
-->

# open(published:)

Opens the downloaded copy of an edition.

```
static func open(published: PSEPublished) async throws -> PSEDownloadedEdition
```

## Discussion

Throws when no usable download exists or the stored edition fails
to load.