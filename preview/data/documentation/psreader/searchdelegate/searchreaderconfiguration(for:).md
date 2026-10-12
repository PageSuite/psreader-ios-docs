<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SearchDelegate/searchReaderConfiguration(for:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader14SearchDelegateP25searchReaderConfiguration3forAA0eF0VSgAA0B11PublicationV_tF"
  },
  "title" : "searchReaderConfiguration(for:)"
}
-->

# searchReaderConfiguration(for:)

Returns the reader configuration to use when opening a search result from the given publication.

```
func searchReaderConfiguration(for publication: SearchPublication) -> ReaderConfiguration?
```

## Parameters

`publication`

The publication the search result belongs to.

## Return Value

A reader configuration, or `nil` if the publication is not recognized.