<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSLegacyBridgedEdition/pageSource",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22PSLegacyBridgedEditionC10pageSourceAA013PSEPageSpreadF0_pSgvp"
  },
  "title" : "pageSource"
}
-->

# pageSource

This edition itself, which reports each spread’s state while it
prepares the spread’s page files, so the reader can show loading and
retry states.

```
var pageSource: (any PSEPageSpreadSource)? { get }
```