<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CarouselViewController/ContentType/feedArchive(guid:publicationName:config:)",
  "metadataVersion" : "0.1.0",
  "role" : "Case",
  "symbol" : {
    "kind" : "Case",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22CarouselViewControllerC11ContentTypeO11feedArchiveyAESS_SSSgAA0H13ConfigurationVSgtcAEmF"
  },
  "title" : "CarouselViewController.ContentType.feedArchive(guid:publicationName:config:)"
}
-->

# CarouselViewController.ContentType.feedArchive(guid:publicationName:config:)

An archive screen for editions on PageSuite’s current system,
classic PDF or responsive.

```
case feedArchive(guid: String, publicationName: String? = nil, config: ArchiveConfiguration? = nil)
```

## Parameters

`guid`

The application GUID of the publication to load.

`publicationName`

Optional publication name. By default, the publication name is derived from
the section or subsection name. If that differs from the actual publication name
(e.g. a section named “Back Issues”), use this parameter to set it explicitly.

`config`

Optional `ArchiveConfiguration` object.