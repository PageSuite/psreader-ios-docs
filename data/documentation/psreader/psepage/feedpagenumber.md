<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPage/feedPageNumber",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEPage(py)feedPageNumber"
  },
  "title" : "feedPageNumber"
}
-->

# feedPageNumber

The page number exactly as the edition’s data published it. The data
numbers advert pages as if they were printed pages, shifting every
subsequent page — `pageNumber` is normalized to the printed folio at
edition load (`PSEEdition.normalizePageNumbers`), and this preserves
the raw value for anything that must use the published numbering.
0 until normalization has run.

```
@objc var feedPageNumber: Int
```