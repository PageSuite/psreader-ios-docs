<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEBookmarkManager/toggleBookmark(forArticle:in:edition:published:application:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18PSEBookmarkManagerC14toggleBookmark10forArticle2in7edition9published11applicationAA0B6ChangeOAA10PSEArticleC_AA7PSEPageCAA10PSEEditionCAA12PSEPublishedCAA11PSAppConfigCSgtKF"
  },
  "title" : "toggleBookmark(forArticle:in:edition:published:application:)"
}
-->

# toggleBookmark(forArticle:in:edition:published:application:)

Bookmarks the article, or removes its bookmark if one exists.

```
@discardableResult func toggleBookmark(forArticle article: PSEArticle, in page: PSEPage, edition: PSEEdition, published: PSEPublished, application: PSAppConfig? = nil) throws -> PSEBookmarkChange
```

## Discussion

`page`, `edition`, and `published` identify where the article lives
so the bookmark can be reopened later; `application` supplies the
header logo recorded as the bookmark’s
[`bookmarkLogo`](/documentation/PSReader/PSEBookmarkArticle/bookmarkLogo) (`nil` for none).
Throws only when creating the bookmark fails to cache the article’s
content.