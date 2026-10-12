<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEBookmarkManager/BookmarkContext/article(_:_:)",
  "metadataVersion" : "0.1.0",
  "role" : "Case",
  "symbol" : {
    "kind" : "Case",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18PSEBookmarkManagerC15BookmarkContextO7articleyAeA7PSEPageC_AA10PSEArticleCtcAEmF"
  },
  "title" : "PSEBookmarkManager.BookmarkContext.article(_:_:)"
}
-->

# PSEBookmarkManager.BookmarkContext.article(_:_:)

An article to bookmark, with the page that holds it.

```
case article(PSEPage, PSEArticle)
```

## Discussion

[`bookmarkContext()`](/documentation/PSReader/PSEPage/bookmarkContext()) returns this for template pages
that hold a single article.