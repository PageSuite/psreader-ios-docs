<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPublished/openEditionSource(onProgress:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader12PSEPublishedC17openEditionSource10onProgressAA010PSEEditionE0_pySfcSg_tYaKF"
  },
  "title" : "openEditionSource(onProgress:)"
}
-->

# openEditionSource(onProgress:)

Opens a reader-ready source for this edition: the downloaded copy if
there is one, otherwise a network stream.

```
func openEditionSource(onProgress: ((Float) -> Void)? = nil) async throws -> PSEEditionSource
```

## Parameters

`onProgress`

Called on the main queue with 0…1 progress
while a streamed edition fetches the assets for its first pages;
not called for a downloaded copy.

## Discussion

Open a download migrated from the legacy SDK ([`isBridged`](/documentation/PSReader/PSEPublished/isBridged) is
`true`) with [`PSLegacyBridgedEdition`](/documentation/PSReader/PSLegacyBridgedEdition) instead. A migrated download
counts as downloaded, so this method takes the downloaded-copy path
for it, and that path expects files only [`PSLegacyBridgedEdition`](/documentation/PSReader/PSLegacyBridgedEdition)
writes.