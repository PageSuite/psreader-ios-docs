<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPage/hostDisplayName",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEPage(py)hostDisplayName"
  },
  "title" : "hostDisplayName"
}
-->

# hostDisplayName

The `displayName` of the classic PDF page hosting this article-level page,
resolved at edition load (`PSEEdition.resolveHostDisplayNames`). Article
pages carry no friendly name of their own and inherit their host’s.

```
@objc var hostDisplayName: String?
```