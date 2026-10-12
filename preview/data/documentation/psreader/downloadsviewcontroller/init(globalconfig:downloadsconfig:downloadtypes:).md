<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DownloadsViewController/init(globalConfig:downloadsConfig:downloadTypes:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader23DownloadsViewControllerC12globalConfig09downloadsF013downloadTypesAcA19GlobalConfigurationV_AA0bK0VSgAJ12DownloadTypeVtcfc"
  },
  "title" : "init(globalConfig:downloadsConfig:downloadTypes:)"
}
-->

# init(globalConfig:downloadsConfig:downloadTypes:)

Initializes a new instance of the downloads view controller with the provided configurations.

```
@MainActor init(globalConfig: GlobalConfiguration, downloadsConfig: DownloadsConfiguration? = nil, downloadTypes: DownloadsConfiguration.DownloadType)
```

## Parameters

`globalConfig`

The global SDK configuration supplying defaults for fonts, colors, delegates, and credentials.

`downloadsConfig`

An optional custom configuration specific to the downloads view.
If `nil`, defaults derived from `globalConfig` are used.

`downloadTypes`

Specifies which types of downloadable content should be displayed (editions on PageSuite’s current system, legacy replica editions, or both).