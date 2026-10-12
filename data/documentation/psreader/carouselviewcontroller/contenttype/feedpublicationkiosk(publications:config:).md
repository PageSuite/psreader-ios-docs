<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CarouselViewController/ContentType/feedPublicationKiosk(publications:config:)",
  "metadataVersion" : "0.1.0",
  "role" : "Case",
  "symbol" : {
    "kind" : "Case",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22CarouselViewControllerC11ContentTypeO20feedPublicationKioskyAESayAA0i4FeedH0VG_AA20ArchiveConfigurationVSgtcAEmF"
  },
  "title" : "CarouselViewController.ContentType.feedPublicationKiosk(publications:config:)"
}
-->

# CarouselViewController.ContentType.feedPublicationKiosk(publications:config:)

A grid of publications on PageSuite’s current system, each linking
to its archive.

```
case feedPublicationKiosk(publications: [KioskFeedPublication], config: ArchiveConfiguration? = nil)
```

## Parameters

`publications`

An array of publication entries.

`config`

Optional default `ArchiveConfiguration` applied when a publication does not provide its own override.