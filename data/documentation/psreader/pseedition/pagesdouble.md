<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEEdition/pagesDouble",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader10PSEEditionC11pagesDoubleSayAA13PSEPageSpreadOGvp"
  },
  "title" : "pagesDouble"
}
-->

# pagesDouble

The spreads the reader pages between in double-page mode, without
the pages [`applyPageFilter(_:)`](/documentation/PSReader/PSEEdition/applyPageFilter(_:)) rules out. Assigning sets the
spreads as built; reading applies the filter.

```
var pagesDouble: [PSEPageSpread] { get set }
```