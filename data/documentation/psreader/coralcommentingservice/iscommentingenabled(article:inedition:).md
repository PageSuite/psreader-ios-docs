<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CoralCommentingService/isCommentingEnabled(article:inEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22CoralCommentingServiceC02isC7Enabled7article9inEditionSbAA10PSEArticleC_AA16PSEEditionSource_ptF"
  },
  "title" : "isCommentingEnabled(article:inEdition:)"
}
-->

# isCommentingEnabled(article:inEdition:)

Returns whether the article has Coral commenting turned on.

```
func isCommentingEnabled(article: PSEArticle, inEdition source: PSEEditionSource) -> Bool
```

## Parameters

`article`

The article to evaluate.

`source`

The edition containing the article.

## Return Value

`true` if the article supports commenting; otherwise,
`false`.

## Discussion

Reads `article.metadata?.coralCommenting?.enabled`, and returns `false`
when the article has no Coral metadata. Override this method to decide
by other criteria.