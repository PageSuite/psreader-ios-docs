<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEBookmarkManager/toggleBookmark(forPage:edition:published:application:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18PSEBookmarkManagerC14toggleBookmark7forPage7edition9published11applicationAA0B6ChangeOAA7PSEPageC_AA10PSEEditionCAA12PSEPublishedCAA11PSAppConfigCSgtKF"
  },
  "title" : "toggleBookmark(forPage:edition:published:application:)"
}
-->

# toggleBookmark(forPage:edition:published:application:)

Bookmarks the page, or removes its bookmark if one exists. See
[`toggleBookmark(forArticle:in:edition:published:application:)`](/documentation/PSReader/PSEBookmarkManager/toggleBookmark(forArticle:in:edition:published:application:)) for
the parameters.

```
@discardableResult func toggleBookmark(forPage page: PSEPage, edition: PSEEdition, published: PSEPublished, application: PSAppConfig? = nil) throws -> PSEBookmarkChange
```