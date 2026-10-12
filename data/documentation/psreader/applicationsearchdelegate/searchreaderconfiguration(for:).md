<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ApplicationSearchDelegate/searchReaderConfiguration(for:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader25ApplicationSearchDelegateC25searchReaderConfiguration3forAA0fG0VSgAA0C11PublicationV_tF"
  },
  "title" : "searchReaderConfiguration(for:)"
}
-->

# searchReaderConfiguration(for:)

Returns the reader configuration for opening results from a
publication.

```
func searchReaderConfiguration(for publication: SearchPublication) -> ReaderConfiguration?
```

## Parameters

`publication`

A publication from
[`searchPublications(completion:)`](/documentation/PSReader/ApplicationSearchDelegate/searchPublications(completion:)).

## Return Value

The reader configuration, or `nil` if this delegate didn’t
list the publication.

## Discussion

The configuration is the `readerConfig` you passed at creation, with
its base URL set for the publication. If its search configuration has
no [`searchDelegate`](/documentation/PSReader/SearchConfiguration/searchDelegate), this delegate fills it, so
search stays available inside the reader.