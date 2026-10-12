<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPage/effectiveScreenshotURL",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader7PSEPageC22effectiveScreenshotURLSSSgvp"
  },
  "title" : "effectiveScreenshotURL"
}
-->

# effectiveScreenshotURL

The best screenshot URL for the page: [`screenshoturl`](/documentation/PSReader/PSEPage/screenshoturl) when set,
else derived from a PDF page’s content URL, else `nil`.

```
var effectiveScreenshotURL: String? { get }
```