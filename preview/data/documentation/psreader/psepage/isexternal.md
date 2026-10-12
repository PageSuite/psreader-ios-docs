<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPage/isExternal",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader7PSEPageC10isExternalSbvp"
  },
  "title" : "isExternal"
}
-->

# isExternal

Whether the page renders externally hosted web content (its
[`external`](/documentation/PSReader/PSEPage/external) flag is set, or its [`type`](/documentation/PSReader/PSEPage/type) is `webview`).

```
var isExternal: Bool { get }
```