<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SearchDelegate/searchPublications(completion:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader14SearchDelegateP18searchPublications10completionyys6ResultOySayAA0B11PublicationVGs5Error_pGc_tF"
  },
  "title" : "searchPublications(completion:)"
}
-->

# searchPublications(completion:)

Provides the list of publications available for searching.

```
func searchPublications(completion: @escaping (Result<[SearchPublication], Error>) -> Void)
```

## Parameters

`completion`

A closure called with the list of searchable publications,
or an error if publications could not be determined.