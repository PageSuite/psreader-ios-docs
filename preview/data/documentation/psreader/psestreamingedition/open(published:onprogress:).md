<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEStreamingEdition/open(published:onProgress:)",
  "metadataVersion" : "0.1.0",
  "role" : "Type Method",
  "symbol" : {
    "kind" : "Type Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19PSEStreamingEditionC4open9published10onProgressAcA12PSEPublishedC_ySfcSgtYaKFZ"
  },
  "title" : "open(published:onProgress:)"
}
-->

# open(published:onProgress:)

Opens an edition for streaming.

```
static func open(published: PSEPublished, onProgress: ((Float) -> Void)? = nil) async throws -> PSEStreamingEdition
```

## Parameters

`published`

The catalog entry to open.

`onProgress`

Called on the main queue with 0…1 progress while the
opening assets download.

## Discussion

Most apps call [`openEditionSource(onProgress:)`](/documentation/PSReader/PSEPublished/openEditionSource(onProgress:))
instead, which opens the downloaded copy when there is one.

> Throws: When the manifest or opening assets cannot be fetched.