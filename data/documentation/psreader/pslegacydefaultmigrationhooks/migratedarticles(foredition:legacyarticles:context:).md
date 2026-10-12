<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSLegacyDefaultMigrationHooks/migratedArticles(forEdition:legacyArticles:context:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22PSLegacyMigrationHooksPAAE16migratedArticles10forEdition06legacyF07contextSayAA0B15MigratedArticleVGAA0bH7SummaryV_SayAA9PSArticleCGAA0bL7ContextVtYaF::SYNTHESIZED::s:8PSReader29PSLegacyDefaultMigrationHooksC"
  },
  "title" : "migratedArticles(forEdition:legacyArticles:context:)"
}
-->

# migratedArticles(forEdition:legacyArticles:context:)

Renders each legacy article that has a headline with a minimal
built-in template: the headline, the byline, the article’s image
when the legacy SDK’s cache holds it, and the body.

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

One article page per legacy article with a headline.