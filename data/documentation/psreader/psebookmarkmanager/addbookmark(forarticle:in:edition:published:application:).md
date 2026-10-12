<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEBookmarkManager/addBookmark(forArticle:in:edition:published:application:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18PSEBookmarkManagerC11addBookmark10forArticle2in7edition9published11applicationAA0bG0CAA10PSEArticleC_AA7PSEPageCAA10PSEEditionCAA12PSEPublishedCAA11PSAppConfigCSgtKF"
  },
  "title" : "addBookmark(forArticle:in:edition:published:application:)"
}
-->

# addBookmark(forArticle:in:edition:published:application:)

Bookmarks the article, replacing any existing bookmark for it. See
[`toggleBookmark(forArticle:in:edition:published:application:)`](/documentation/PSReader/PSEBookmarkManager/toggleBookmark(forArticle:in:edition:published:application:)) for
the parameters.

```
@discardableResult func addBookmark(forArticle article: PSEArticle, in page: PSEPage, edition: PSEEdition, published: PSEPublished, application: PSAppConfig? = nil) throws -> PSEBookmarkArticle
```