<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PublicationGroupService/latestEditions(groupGUID:thumbnailWidth:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader23PublicationGroupServiceV14latestEditions9groupGUID14thumbnailWidthSayAA0bC7EditionVGSS_SitYaKF"
  },
  "title" : "latestEditions(groupGUID:thumbnailWidth:)"
}
-->

# latestEditions(groupGUID:thumbnailWidth:)

Returns the latest edition of each publication in a group, in the
order the group defines.

```
func latestEditions(groupGUID: String, thumbnailWidth: Int = 300) async throws -> [PublicationGroupEdition]
```

## Parameters

`groupGUID`

The publication group GUID.

`thumbnailWidth`

The width, in pixels, to render each edition’s
cover at.

## Return Value

One [`PublicationGroupEdition`](/documentation/PSReader/PublicationGroupEdition) per publication. A
publication with nothing published is left out.

## Discussion> Throws: ``doc://com.pagesuite.PSReader/documentation/PSReader/PublicationGroupService/ServiceError/invalidURL`` when the GUID can’t form a URL,
> or ``doc://com.pagesuite.PSReader/documentation/PSReader/PublicationGroupService/ServiceError/invalidResponse`` when the request fails with no
> stored copy to fall back to or the backend sends something the
> service can’t read.