<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSLegacyMigrationHooks/migratedArticles(forEdition:legacyArticles:context:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22PSLegacyMigrationHooksP16migratedArticles10forEdition06legacyF07contextSayAA0B15MigratedArticleVGAA0bH7SummaryV_SayAA9PSArticleCGAA0bL7ContextVtYaF"
  },
  "title" : "migratedArticles(forEdition:legacyArticles:context:)"
}
-->

# migratedArticles(forEdition:legacyArticles:context:)

Builds the article pages of a migrated edition from its legacy
articles.

```
func migratedArticles(forEdition edition: PSLegacyEditionSummary, legacyArticles: [PSArticle], context: PSLegacyArticleContext) async -> [PSLegacyMigratedArticle]
```

## Parameters

`edition`

The legacy edition being opened.

`legacyArticles`

The legacy edition’s articles.

`context`

Helpers for reading the legacy SDK’s cache and naming
image files.

## Return Value

The article pages to add, in order.

## Discussion

Called each time a migrated edition opens through
[`open(published:hooks:onProgress:completion:)`](/documentation/PSReader/PSLegacyBridgedEdition/open(published:hooks:onProgress:completion:)).
Each [`PSLegacyMigratedArticle`](/documentation/PSReader/PSLegacyMigratedArticle) becomes one article page after the
edition’s PDF pages, opened from regions on those pages (see
[`hotspots`](/documentation/PSReader/PSLegacyMigratedArticle/hotspots)).