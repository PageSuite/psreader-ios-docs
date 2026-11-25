<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEEdition/supportedPageTypes",
  "metadataVersion" : "0.1.0",
  "role" : "Type Property",
  "symbol" : {
    "kind" : "Type Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader10PSEEditionC18supportedPageTypesShySSGvpZ"
  },
  "title" : "supportedPageTypes"
}
-->

# supportedPageTypes

The page types the reader can render. A page of any other type is
left out of the spreads, so a type this SDK predates pages past
cleanly instead of rendering as a broken web page. [`pages`](/documentation/PSReader/PSEEdition/pages) keeps
every page as published.

```
static let supportedPageTypes: Set<String>
```