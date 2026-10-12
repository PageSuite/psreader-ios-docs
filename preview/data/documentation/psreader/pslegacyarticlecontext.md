<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSLegacyArticleContext",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22PSLegacyArticleContextV"
  },
  "title" : "PSLegacyArticleContext"
}
-->

# PSLegacyArticleContext

Helpers handed to the hooks while they build migrated articles at open time.
Cache-first with network fallback (the edition is opening; the network layer is
available and self-heals the cache).

```
struct PSLegacyArticleContext
```

## Topics

### Edition

[`edition`](/documentation/PSReader/PSLegacyArticleContext/edition)

The legacy edition whose articles are being migrated.

### Reading Legacy Files

[`hasCachedData(forLegacyURL:)`](/documentation/PSReader/PSLegacyArticleContext/hasCachedData(forLegacyURL:))

Returns whether the legacy SDK’s cache holds a copy of the given
absolute legacy URL, without using the network.

[`cachedData(forLegacyURL:)`](/documentation/PSReader/PSLegacyArticleContext/cachedData(forLegacyURL:))

Synchronous disk-only lookup (no network).

[`fetchData(forLegacyURL:)`](/documentation/PSReader/PSLegacyArticleContext/fetchData(forLegacyURL:))

Bytes for the given absolute legacy URL: disk (sha1+md5) first, then network.

### Referencing Images

[`localImageReference(forLegacyURL:)`](/documentation/PSReader/PSLegacyArticleContext/localImageReference(forLegacyURL:))

The edition-folder-relative filename the given legacy image URL takes once
materialized. Include the URL in `imageURLsToMaterialize` for the file to exist.

