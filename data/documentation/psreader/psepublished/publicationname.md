<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPublished/publicationName",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEPublished(py)publicationName"
  },
  "title" : "publicationName"
}
-->

# publicationName

The publication’s display name.

```
@objc var publicationName: String
```

## Discussion

[`FeedEditionService`](/documentation/PSReader/FeedEditionService) fills it in only from the `publicationName`
you pass when you load a publication’s catalog; without one, it’s
empty. It’s also empty on an edition resolved with
[`published(forEditionGUID:)`](/documentation/PSReader/FeedEditionService/published(forEditionGUID:)). When you know the
name, set it yourself.