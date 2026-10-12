<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/FeedEditionService/init(accountGUID:timeZone:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18FeedEditionServiceV11accountGUID8timeZoneACSS_10Foundation04TimeH0Vtcfc"
  },
  "title" : "init(accountGUID:timeZone:)"
}
-->

# init(accountGUID:timeZone:)

Creates an edition service for an account.

```
init(accountGUID: String, timeZone: TimeZone = .current)
```

## Parameters

`accountGUID`

The account the service’s requests are scoped to.

`timeZone`

The time zone for formatting edition date strings the
backend leaves out. Defaults to the device’s time zone.