<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CarouselViewController/ContentType/replicaArchive(guid:supplements:config:)",
  "metadataVersion" : "0.1.0",
  "role" : "Case",
  "symbol" : {
    "kind" : "Case",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22CarouselViewControllerC11ContentTypeO14replicaArchiveyAESS_SaySSGSgAA0H13ConfigurationVSgtcAEmF"
  },
  "title" : "CarouselViewController.ContentType.replicaArchive(guid:supplements:config:)"
}
-->

# CarouselViewController.ContentType.replicaArchive(guid:supplements:config:)

An archive screen for legacy replica editions.

```
case replicaArchive(guid: String, supplements: [String]? = nil, config: ArchiveConfiguration? = nil)
```

## Parameters

`guid`

The publication guid for the replica publication to load.

`supplements`

Optional an array of replica publication supplement guids.

`config`

Optional `ArchiveConfiguration` object.