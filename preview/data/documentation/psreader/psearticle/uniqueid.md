<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEArticle/uniqueid",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEArticle(py)uniqueid"
  },
  "title" : "uniqueid"
}
-->

# uniqueid

A unique identifier for the article, as sent by the backend.

```
@objc var uniqueid: String?
```

## Discussion

It’s separate from [`articleguid`](/documentation/PSReader/PSEArticle/articleguid), the article’s identity within the
edition. The SDK stores it as a string even when the backend sends a
number.