<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPublished/editionDateString",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEPublished(py)editionDateString"
  },
  "title" : "editionDateString"
}
-->

# editionDateString

The edition date as display text, for example
“Tuesday September 1 2026”.

```
@objc var editionDateString: String?
```

## Discussion

The backend can send this text itself. Otherwise
[`FeedEditionService`](/documentation/PSReader/FeedEditionService) formats [`editionDate`](/documentation/PSReader/PSEPublished/editionDate) as weekday, month, day
and year in its [`timeZone`](/documentation/PSReader/FeedEditionService/timeZone). `nil` when neither is
available. For your own formatting, start from [`editionDate`](/documentation/PSReader/PSEPublished/editionDate).