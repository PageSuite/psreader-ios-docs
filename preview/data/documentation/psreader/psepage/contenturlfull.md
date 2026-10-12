<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPage/contenturlFull",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEPage(py)contenturlFull"
  },
  "title" : "contenturlFull"
}
-->

# contenturlFull

A URL for the page’s HTML, as sent by the backend.

```
@objc var contenturlFull: String?
```

## Discussion

For HTML advert pages, the built-in advert rendering fetches the
advert’s HTML from this URL, falling back to [`contenturlOriginal`](/documentation/PSReader/PSEPage/contenturlOriginal).