<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEStreamingEdition/open(published:onProgress:completion:)",
  "metadataVersion" : "0.1.0",
  "role" : "Type Method",
  "symbol" : {
    "kind" : "Type Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19PSEStreamingEditionC4open9published10onProgress10completionyAA12PSEPublishedC_ySfcSgys6ResultOyACs5Error_pGctFZ"
  },
  "title" : "open(published:onProgress:completion:)"
}
-->

# open(published:onProgress:completion:)

Opens an edition for streaming.

```
static func open(published: PSEPublished, onProgress: ((Float) -> Void)? = nil, completion: @escaping (Result<PSEStreamingEdition, Error>) -> Void)
```

## Parameters

`published`

The catalog entry to open.

`onProgress`

Called on the main queue with 0…1 progress while the
opening assets download.

`completion`

Called on the main queue with the source, or an error
if the manifest or opening assets cannot be fetched.