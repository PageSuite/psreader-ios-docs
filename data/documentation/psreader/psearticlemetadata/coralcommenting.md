<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEArticleMetadata/coralCommenting",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEArticleMetadata(py)coralCommenting"
  },
  "title" : "coralCommenting"
}
-->

# coralCommenting

The article’s Coral commenting identifiers, or `nil` when it has
none.

```
@objc var coralCommenting: PSECoralCommenting?
```

## Discussion

The value is a `PSECoralCommenting`: its `assetId` is the article’s
Coral asset ID, `publicUrl` is the URL associated with its comment
stream, and `enabled` says whether commenting is on for the article.
[`CoralCommentingService`](/documentation/PSReader/CoralCommentingService) reads `enabled` to decide whether the
article offers comments, and sends `assetId` to Coral as the
article’s ID.