<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/KioskReplicaPublication/init(guid:archiveConfig:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader23KioskReplicaPublicationV4guid13archiveConfigACSS_AA20ArchiveConfigurationVSgtcfc"
  },
  "title" : "init(guid:archiveConfig:)"
}
-->

# init(guid:archiveConfig:)

Creates a replica publication entry for a kiosk grid.

```
init(guid: String, archiveConfig: ArchiveConfiguration? = nil)
```

## Parameters

`guid`

The publication guid to load the replica archive.

`archiveConfig`

Optional per-publication archive configuration override.