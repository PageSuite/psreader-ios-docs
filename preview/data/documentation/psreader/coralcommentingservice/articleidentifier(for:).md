<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CoralCommentingService/articleIdentifier(for:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22CoralCommentingServiceC17articleIdentifier3forSSSgAA10PSEArticleC_tF"
  },
  "title" : "articleIdentifier(for:)"
}
-->

# articleIdentifier(for:)

Returns the article’s Coral asset ID.

```
func articleIdentifier(for article: PSEArticle) -> String?
```

## Parameters

`article`

The article to identify.

## Return Value

The Coral asset ID, or `nil` if the article has none.

## Discussion

Reads `article.metadata?.coralCommenting?.assetId`. The service sends
this value to Coral as the article’s ID and reads the article’s count
from the response under it. Override this method if your publication
stores the Coral asset ID elsewhere.