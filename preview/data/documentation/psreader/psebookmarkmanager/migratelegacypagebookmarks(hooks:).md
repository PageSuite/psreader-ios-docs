<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEBookmarkManager/migrateLegacyPageBookmarks(hooks:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18PSEBookmarkManagerC26migrateLegacyPageBookmarks5hooksyAA22PSLegacyMigrationHooks_p_tF"
  },
  "title" : "migrateLegacyPageBookmarks(hooks:)"
}
-->

# migrateLegacyPageBookmarks(hooks:)

One-shot, idempotent. Converts every legacy saved page into a bridged page
bookmark: identity from the legacy `.dat`, best-effort thumbnail copy into the
shared saved-bookmarks folder (the cell falls back to the remote legacy image
when absent). Opening resolves lazily through `PSLegacyBridgedEdition`.

```
func migrateLegacyPageBookmarks(hooks: PSLegacyMigrationHooks = PSLegacyDefaultMigrationHooks())
```