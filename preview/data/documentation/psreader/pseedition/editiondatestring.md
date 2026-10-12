<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEEdition/editionDateString",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEEdition(py)editionDateString"
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

The backend can send this text itself. Otherwise the SDK formats
[`editionDate`](/documentation/PSReader/PSEEdition/editionDate) as weekday, month, day and year in UTC. `nil` when
neither is available. For your own formatting, start from
[`editionDate`](/documentation/PSReader/PSEEdition/editionDate).