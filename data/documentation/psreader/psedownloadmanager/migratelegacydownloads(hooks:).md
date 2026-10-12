<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEDownloadManager/migrateLegacyDownloads(hooks:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18PSEDownloadManagerC22migrateLegacyDownloads5hooksyAA22PSLegacyMigrationHooks_p_tF"
  },
  "title" : "migrateLegacyDownloads(hooks:)"
}
-->

# migrateLegacyDownloads(hooks:)

Adds the editions downloaded with the legacy SDK to [`downloads`](/documentation/PSReader/PSEDownloadManager/downloads).

```
func migrateLegacyDownloads(hooks: PSLegacyMigrationHooks = PSLegacyDefaultMigrationHooks())
```

## Parameters

`hooks`

Sets the migrated entries’ identity, chooses which
editions migrate, and names extra cached files to keep. See
[`PSLegacyMigrationHooks`](/documentation/PSReader/PSLegacyMigrationHooks).

## Discussion

Call it once at startup. It does its work once and doesn’t use the
network. Each migrated edition gets a catalog entry flagged
[`isBridged`](/documentation/PSReader/PSEPublished/isBridged), built from what the legacy SDK recorded
about the download, and is reported to observers as
[`PSEDownloadManager.DownloadState.downloaded`](/documentation/PSReader/PSEDownloadManager/DownloadState/downloaded). Its pages are built only when the
edition opens, through [`PSLegacyBridgedEdition`](/documentation/PSReader/PSLegacyBridgedEdition). If the legacy
SDK’s download list exists but can’t be read yet, for example before
the device’s first unlock, the next call tries again.