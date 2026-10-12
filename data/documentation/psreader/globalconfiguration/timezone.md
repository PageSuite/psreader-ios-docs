<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/GlobalConfiguration/timeZone",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19GlobalConfigurationV8timeZone10Foundation04TimeE0Vvp"
  },
  "title" : "timeZone"
}
-->

# timeZone

Time zone used when parsing edition strings into `Date` objects.

```
var timeZone: TimeZone
```

## Discussion

By default the SDK interprets timestamps in the system timezone. Provide an
explicit timezone to keep this consistent across all locales.

> Tip: Set this to an explicit timezone (e.g., `TimeZone(identifier: "Europe/London")`)
> to ensure edition dates display consistently regardless of the user’s locale.