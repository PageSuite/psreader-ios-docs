<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEDownloadedEdition/open(published:completion:)",
  "metadataVersion" : "0.1.0",
  "role" : "Type Method",
  "symbol" : {
    "kind" : "Type Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader20PSEDownloadedEditionV4open9published10completionyAA12PSEPublishedC_ys6ResultOyACs5Error_pGctFZ"
  },
  "title" : "open(published:completion:)"
}
-->

# open(published:completion:)

Opens the downloaded copy of an edition.

```
static func open(published: PSEPublished, completion: @escaping (Result<PSEDownloadedEdition, Error>) -> Void)
```

## Discussion

The completion is called on the main queue with the source, or with
an error when no usable download exists or the stored edition fails
to load.