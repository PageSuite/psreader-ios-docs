<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionReaderViewController/MediaDelegate-swift.protocol/baseURL(for:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29PSEditionReaderViewControllerC13MediaDelegateP7baseURL3forSSSgAA7PSEPageC_tF"
  },
  "title" : "baseURL(for:)"
}
-->

# baseURL(for:)

The base URL a page’s HTML resolves relative references against.
The default returns the page’s own `baseURL`.

```
func baseURL(for page: PSEPage) -> String?
```