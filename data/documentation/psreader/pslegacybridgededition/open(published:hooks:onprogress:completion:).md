<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSLegacyBridgedEdition/open(published:hooks:onProgress:completion:)",
  "metadataVersion" : "0.1.0",
  "role" : "Type Method",
  "symbol" : {
    "kind" : "Type Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22PSLegacyBridgedEditionC4open9published5hooks10onProgress10completionyAA12PSEPublishedC_AA0B14MigrationHooks_pySfcSgys6ResultOyACs5Error_pGctFZ"
  },
  "title" : "open(published:hooks:onProgress:completion:)"
}
-->

# open(published:hooks:onProgress:completion:)

Opens a bridged legacy download.

```
static func open(published: PSEPublished, hooks: PSLegacyMigrationHooks = PSLegacyDefaultMigrationHooks(), onProgress: ((Float) -> Void)? = nil, completion: @escaping (Result<PSLegacyBridgedEdition, Error>) -> Void)
```

## Parameters

`published`

A migrated catalog entry ([`isBridged`](/documentation/PSReader/PSEPublished/isBridged)).

`hooks`

The migration hooks that build the edition’s article pages
and supply the files they reference; the default renders each
article with a minimal built-in template.

`onProgress`

Called with 0…1 progress while opening assets resolve.

`completion`

Called on the main queue with the source or an error.