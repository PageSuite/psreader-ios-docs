<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPublished/editionGUID",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEPublished(py)editionGUID"
  },
  "title" : "editionGUID"
}
-->

# editionGUID

Identifier of the edition content behind this catalog entry.

```
@objc var editionGUID: String
```

## Discussion

An edition published more than once has a catalog entry for each
publish. The entries share this GUID and differ in
[`publishedGUID`](/documentation/PSReader/PSEPublished/publishedGUID).