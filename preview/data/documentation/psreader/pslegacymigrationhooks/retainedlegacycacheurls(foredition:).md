<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSLegacyMigrationHooks/retainedLegacyCacheURLs(forEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22PSLegacyMigrationHooksP23retainedLegacyCacheURLs10forEditionSaySSGSS_tF"
  },
  "title" : "retainedLegacyCacheURLs(forEdition:)"
}
-->

# retainedLegacyCacheURLs(forEdition:)

Returns the URLs of files your app cached through the legacy SDK for
an edition, such as article feeds, that must stay readable offline
after migration.

```
func retainedLegacyCacheURLs(forEdition editionGUID: String) -> [String]
```

## Parameters

`editionGUID`

The legacy edition’s GUID.

## Return Value

The absolute URLs the legacy SDK cached the files under.

## Discussion

Migration extends the expiry of each URL’s cached copy so later cache
refreshes don’t remove it. List content your app fetched itself, not
the SDK’s own files. Called for each legacy download that migrates.