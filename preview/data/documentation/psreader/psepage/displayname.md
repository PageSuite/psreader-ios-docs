<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPage/displayName",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEPage(py)displayName"
  },
  "title" : "displayName"
}
-->

# displayName

The publisher’s friendly page label (“A1”, “B12”…) exactly as the
edition’s data published it. Optional and opaque: it is never parsed or reformatted,
and whole editions or individual pages may lack it.

```
@objc var displayName: String?
```