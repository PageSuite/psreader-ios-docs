<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CarouselViewController/ContentType/replicaPublicationKiosk(publications:config:)",
  "metadataVersion" : "0.1.0",
  "role" : "Case",
  "symbol" : {
    "kind" : "Case",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22CarouselViewControllerC11ContentTypeO23replicaPublicationKioskyAESayAA0i7ReplicaH0VG_AA20ArchiveConfigurationVSgtcAEmF"
  },
  "title" : "CarouselViewController.ContentType.replicaPublicationKiosk(publications:config:)"
}
-->

# CarouselViewController.ContentType.replicaPublicationKiosk(publications:config:)

A grid of replica publications, each linking to a publication landing page.

```
case replicaPublicationKiosk(publications: [KioskReplicaPublication], config: ArchiveConfiguration? = nil)
```

## Parameters

`publications`

An array of replica publication entries.

`config`

Optional default `ArchiveConfiguration` applied when a publication does not provide its own override.