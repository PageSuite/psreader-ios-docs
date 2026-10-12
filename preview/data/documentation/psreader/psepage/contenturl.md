<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPage/contenturl",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEPage(py)contenturl"
  },
  "title" : "contenturl"
}
-->

# contenturl

The page’s main content: the PDF file for PDF pages, the HTML template
the reader fills in for templated pages, or the web address for
external pages (see [`isExternal`](/documentation/PSReader/PSEPage/isExternal)).

```
@objc var contenturl: String?
```

## Discussion

A PDF page’s reference is relative to the edition’s storage, so
resolve it through the source’s [`resourceManager`](/documentation/PSReader/PSEEditionSource/resourceManager).