<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/FeedEditionService/timeZone",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18FeedEditionServiceV8timeZone10Foundation04TimeF0Vvp"
  },
  "title" : "timeZone"
}
-->

# timeZone

The time zone the service formats edition date strings in.

```
let timeZone: TimeZone
```

## Discussion

The backend groups the catalog into dates; this time zone doesn’t
change that grouping. It only formats each edition’s
`editionDateString` from its edition date when the backend doesn’t
send a string of its own.