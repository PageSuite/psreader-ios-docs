<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPublished/applicationGUID",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEPublished(py)applicationGUID"
  },
  "title" : "applicationGUID"
}
-->

# applicationGUID

GUID of the publication this edition belongs to. The property
keeps the identifier’s historical name; the docs call it the
publication GUID.

```
@objc var applicationGUID: String
```

## Discussion

[`FeedEditionService`](/documentation/PSReader/FeedEditionService) fills it in from the publication GUID you
request the catalog with. It’s empty on an edition resolved with
[`published(forEditionGUID:)`](/documentation/PSReader/FeedEditionService/published(forEditionGUID:)); use the publication
GUID you already hold instead. [`publicationGUID`](/documentation/PSReader/PSEPublished/publicationGUID) is the backend’s
filing GUID and can differ, so use it only as a last resort.