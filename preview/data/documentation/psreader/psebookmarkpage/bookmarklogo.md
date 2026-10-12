<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEBookmarkPage/bookmarkLogo",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEBookmarkPage(py)bookmarkLogo"
  },
  "title" : "bookmarkLogo"
}
-->

# bookmarkLogo

The publication’s header logo for the edition’s date, as set in the
app configuration.

```
@objc var bookmarkLogo: String?
```

## Discussion

Set only when an `application` configuration was passed while
bookmarking the page, so it’s `nil` for pages migrated from the
legacy SDK.