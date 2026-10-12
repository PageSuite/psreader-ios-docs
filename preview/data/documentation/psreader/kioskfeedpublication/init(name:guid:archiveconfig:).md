<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/KioskFeedPublication/init(name:guid:archiveConfig:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader20KioskFeedPublicationV4name4guid13archiveConfigACSS_SSAA20ArchiveConfigurationVSgtcfc"
  },
  "title" : "init(name:guid:archiveConfig:)"
}
-->

# init(name:guid:archiveConfig:)

Creates a publication entry for a kiosk grid.

```
init(name: String, guid: String, archiveConfig: ArchiveConfiguration? = nil)
```

## Parameters

`name`

The display name for the publication.

`guid`

The publication GUID used to load the publication’s archive.

`archiveConfig`

Optional per-publication archive configuration override.