<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEArticle/datecreated",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEArticle(py)datecreated"
  },
  "title" : "datecreated"
}
-->

# datecreated

When the article was created, as a date string from the backend.

```
@objc var datecreated: String?
```

## Discussion

The reader expects an ISO 8601 UTC timestamp with milliseconds, such
as `2026-09-01T06:00:00.000Z`.