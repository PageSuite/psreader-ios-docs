<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPage/external",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEPage(py)external"
  },
  "title" : "external"
}
-->

# external

Whether the backend flags the page as externally hosted web content,
which the reader loads from [`contenturl`](/documentation/PSReader/PSEPage/contenturl).

```
@objc var external: Bool
```

## Discussion

Check [`isExternal`](/documentation/PSReader/PSEPage/isExternal) instead to also cover `webview` pages.