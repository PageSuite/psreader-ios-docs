<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionReaderViewController/scrollCollapseController",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29PSEditionReaderViewControllerC014scrollCollapseE0AA09PSEScrollgE0CSgvp"
  },
  "title" : "scrollCollapseController"
}
-->

# scrollCollapseController

Collapses and reveals host chrome in response to the reader’s
scrolling. Attach one and register your chrome animations on it; the
reader feeds it scroll activity from every page.

```
@MainActor var scrollCollapseController: PSEScrollCollapseController? { get set }
```