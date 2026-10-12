<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultCommentingProvider/articleIdentifier(for:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader25DefaultCommentingProviderC17articleIdentifier3forSSSgAA10PSEArticleC_tF"
  },
  "title" : "articleIdentifier(for:)"
}
-->

# articleIdentifier(for:)

Returns the article’s identifier from [`service`](/documentation/PSReader/DefaultCommentingProvider/service).

```
func articleIdentifier(for article: PSEArticle) -> String?
```

## Parameters

`article`

The article to identify.

## Return Value

The identifier, or `nil` if the service can’t identify the
article.