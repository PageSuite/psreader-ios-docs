<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CommentingService/isCommentingEnabled(article:inEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader17CommentingServiceP02isB7Enabled7article9inEditionSbAA10PSEArticleC_AA16PSEEditionSource_ptF"
  },
  "title" : "isCommentingEnabled(article:inEdition:)"
}
-->

# isCommentingEnabled(article:inEdition:)

Determines whether commenting is enabled for the given article.

```
func isCommentingEnabled(article: PSEArticle, inEdition source: PSEEditionSource) -> Bool
```

## Parameters

`article`

The article to evaluate.

`source`

The edition containing the article.

## Return Value

`true` if the article supports commenting; otherwise, `false`.

## Discussion

When this returns `false`, no commenting UI is shown for the article —
no button, no count, no icons.