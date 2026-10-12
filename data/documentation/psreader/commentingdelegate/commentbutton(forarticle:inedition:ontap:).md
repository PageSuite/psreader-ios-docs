<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CommentingDelegate/commentButton(forArticle:inEdition:onTap:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18CommentingDelegateP13commentButton10forArticle9inEdition5onTapAA0bE4View_pSgAA10PSEArticleC_AA16PSEEditionSource_pyyctF"
  },
  "title" : "commentButton(forArticle:inEdition:onTap:)"
}
-->

# commentButton(forArticle:inEdition:onTap:)

Provides a comment button view for the given article.

```
@MainActor func commentButton(forArticle article: PSEArticle, inEdition source: PSEEditionSource, onTap: @escaping () -> Void) -> (any CommentingButtonView)?
```

## Parameters

`article`

The article the button is for.

`source`

The edition containing the article.

`onTap`

Closure to invoke when the button is tapped.

## Return Value

A [`CommentingButtonView`](/documentation/PSReader/CommentingButtonView) instance, or `nil` to suppress the button.

## Discussion

The SDK calls this method to obtain a button that is displayed at the
bottom of the article view. Return `nil` to suppress the button.

The SDK provides an `onTap` closure that your button must invoke when
tapped — wire it to [`onTap`](/documentation/PSReader/CommentingButtonView/onTap).