<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEBookmarkManager/addBookmark(forPage:edition:published:application:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18PSEBookmarkManagerC11addBookmark7forPage7edition9published11applicationAA0bG0CAA7PSEPageC_AA10PSEEditionCAA12PSEPublishedCAA11PSAppConfigCSgtKF"
  },
  "title" : "addBookmark(forPage:edition:published:application:)"
}
-->

# addBookmark(forPage:edition:published:application:)

Bookmarks the page, replacing any existing bookmark for it.

```
@discardableResult func addBookmark(forPage page: PSEPage, edition: PSEEdition, published: PSEPublished, application: PSAppConfig? = nil) throws -> PSEBookmarkPage
```