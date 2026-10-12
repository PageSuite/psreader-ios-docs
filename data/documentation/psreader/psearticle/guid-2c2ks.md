<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEArticle/guid-2c2ks",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEArticle(py)guid"
  },
  "title" : "guid"
}
-->

# guid

The identifier of the source feed item the article came from, as sent
by the backend under `guid`.

```
@objc var guid: String?
```

## Discussion

The SDK doesn’t use it. To identify the article, use [`articleguid`](/documentation/PSReader/PSEArticle/articleguid).