<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultCommentingProvider/commentButton(forArticle:inEdition:onTap:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader25DefaultCommentingProviderC13commentButton10forArticle9inEdition5onTapAA0cF4View_pSgAA10PSEArticleC_AA16PSEEditionSource_pyyctF"
  },
  "title" : "commentButton(forArticle:inEdition:onTap:)"
}
-->

# commentButton(forArticle:inEdition:onTap:)

Returns a [`DefaultCommentingButton`](/documentation/PSReader/DefaultCommentingButton) styled with [`accentColor`](/documentation/PSReader/DefaultCommentingProvider/accentColor) and [`fontFamily`](/documentation/PSReader/DefaultCommentingProvider/fontFamily).

```
@MainActor func commentButton(forArticle article: PSEArticle, inEdition source: PSEEditionSource, onTap: @escaping () -> Void) -> (any CommentingButtonView)?
```