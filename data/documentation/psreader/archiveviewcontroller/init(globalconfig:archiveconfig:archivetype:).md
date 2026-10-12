<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ArchiveViewController/init(globalConfig:archiveConfig:archiveType:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader21ArchiveViewControllerC12globalConfig07archiveF00G4TypeAcA19GlobalConfigurationV_AA0bJ0VSgAC0bH0Otcfc"
  },
  "title" : "init(globalConfig:archiveConfig:archiveType:)"
}
-->

# init(globalConfig:archiveConfig:archiveType:)

Initializes a new instance of the archive view controller with the provided configurations.

```
@MainActor init(globalConfig: GlobalConfiguration, archiveConfig: ArchiveConfiguration? = nil, archiveType: ArchiveType)
```

## Parameters

`globalConfig`

The global SDK configuration supplying defaults for fonts, colors, delegates, and credentials.

`archiveConfig`

An optional custom configuration specific to the archive view.
If `nil`, defaults derived from `globalConfig` are used.

`archiveType`

Specifies which type of archive content should be displayed.