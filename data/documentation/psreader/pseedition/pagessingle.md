<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEEdition/pagesSingle",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader10PSEEditionC11pagesSingleSayAA13PSEPageSpreadOGvp"
  },
  "title" : "pagesSingle"
}
-->

# pagesSingle

The spreads the reader pages between in single-page mode, without
the pages [`applyPageFilter(_:)`](/documentation/PSReader/PSEEdition/applyPageFilter(_:)) rules out. Assigning sets the
spreads as built; reading applies the filter.

```
var pagesSingle: [PSEPageSpread] { get set }
```