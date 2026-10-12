<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CommentingDelegate/commentButtonTapped(forArticle:onPage:inEdition:from:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18CommentingDelegateP19commentButtonTapped10forArticle6onPage9inEdition4fromyAA10PSEArticleC_AA7PSEPageCAA16PSEEditionSource_pSo16UIViewControllerCtF"
  },
  "title" : "commentButtonTapped(forArticle:onPage:inEdition:from:)"
}
-->

# commentButtonTapped(forArticle:onPage:inEdition:from:)

Called when the user taps a comment button.

```
@MainActor func commentButtonTapped(forArticle article: PSEArticle, onPage page: PSEPage, inEdition source: PSEEditionSource, from viewController: UIViewController)
```

## Parameters

`article`

The article whose comment button was tapped.

`page`

The page containing the article.

`source`

The edition containing the article.

`viewController`

The presenting view controller.

## Discussion

Use this to present your commenting UI. This is called for both native
comment buttons and template-based (HTML) comment buttons.