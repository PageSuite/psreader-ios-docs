<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ArticleJumpNavigationSource",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader27ArticleJumpNavigationSourceV"
  },
  "title" : "ArticleJumpNavigationSource"
}
-->

# ArticleJumpNavigationSource

The scroll-source token the reader passes when in-page content triggers
a jump to an article.

```
struct ArticleJumpNavigationSource
```

## Topics

### Reading the Jump

[`targetArticleGUID`](/documentation/PSReader/ArticleJumpNavigationSource/targetArticleGUID)

The GUID of the article the jump targets.

[`sourcePage`](/documentation/PSReader/ArticleJumpNavigationSource/sourcePage)

The page whose content triggered the jump, or `nil` when unknown.

[`mediaObject`](/documentation/PSReader/ArticleJumpNavigationSource/mediaObject)

The hotspot that triggered the jump, or `nil` when the jump didn’t
come from a hotspot. The reader’s own article jumps come from links
in templated pages, so they leave this `nil`.

### Tagging Your Own Jumps

[`init(sourcePage:mediaObject:targetArticleGUID:)`](/documentation/PSReader/ArticleJumpNavigationSource/init(sourcePage:mediaObject:targetArticleGUID:))

Creates an article-jump token.

