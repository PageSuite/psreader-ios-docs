<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ApplicationSearchDelegate/searchPublications(completion:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader25ApplicationSearchDelegateC18searchPublications10completionyys6ResultOySayAA0C11PublicationVGs5Error_pGc_tF"
  },
  "title" : "searchPublications(completion:)"
}
-->

# searchPublications(completion:)

Provides a searchable publication for each publication in the archive
of the `PSAppConfig`.

```
func searchPublications(completion: @escaping (Result<[SearchPublication], Error>) -> Void)
```

## Parameters

`completion`

Called with the publications, with
[`SearchError.noPublications`](/documentation/PSReader/SearchError/noPublications) if the configuration lists none, or
with the error from fetching the configuration.

## Discussion

Publications on PageSuite’s current system are listed by publication
GUID, with the search type their configuration names, and legacy
replica publications by replica publication GUID. A delegate created from a shortcode fetches the
configuration on the first call; later calls reuse the result.