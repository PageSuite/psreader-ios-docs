<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPage/contenturlOriginal",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEPage(py)contenturlOriginal"
  },
  "title" : "contenturlOriginal"
}
-->

# contenturlOriginal

A URL for the page’s original HTML, as sent by the backend.

```
@objc var contenturlOriginal: String?
```

## Discussion

For HTML advert pages, the built-in advert rendering fetches the
advert’s HTML from this URL when [`contenturlFull`](/documentation/PSReader/PSEPage/contenturlFull) is missing.