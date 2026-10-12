<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPage/editionGUID",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEPage(py)editionGUID"
  },
  "title" : "editionGUID"
}
-->

# editionGUID

The GUID of the edition the page came from.

```
@objc var editionGUID: String?
```

## Discussion

Pages a [`PSEBookmarksEdition`](/documentation/PSReader/PSEBookmarksEdition) builds from article bookmarks carry
their bookmark’s edition GUID. On other pages it’s set only when the
backend payload includes one.