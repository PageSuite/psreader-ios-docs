<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEBookmarkManager/toggleBookmark(context:edition:published:application:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18PSEBookmarkManagerC14toggleBookmark7context7edition9published11applicationAA0B6ChangeOSgAC0E7ContextO_AA10PSEEditionCAA12PSEPublishedCAA11PSAppConfigCSgtKF"
  },
  "title" : "toggleBookmark(context:edition:published:application:)"
}
-->

# toggleBookmark(context:edition:published:application:)

Toggles the bookmark for whatever the context holds; returns `nil`
for [`PSEBookmarkManager.BookmarkContext.none`](/documentation/PSReader/PSEBookmarkManager/BookmarkContext/none). See
[`toggleBookmark(forArticle:in:edition:published:application:)`](/documentation/PSReader/PSEBookmarkManager/toggleBookmark(forArticle:in:edition:published:application:)) for
the parameters.

```
@discardableResult func toggleBookmark(context: BookmarkContext, edition: PSEEdition, published: PSEPublished, application: PSAppConfig? = nil) throws -> PSEBookmarkChange?
```