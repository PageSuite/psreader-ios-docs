<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSAppConfig/accountGUID",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader11PSAppConfigC11accountGUIDSSSgvp"
  },
  "title" : "accountGUID"
}
-->

# accountGUID

The GUID of the account the configuration belongs to, or `nil` when
the configuration doesn’t name one.

```
var accountGUID: String? { get }
```

## Discussion

Use it to create services that need an account, such as
[`FeedEditionService`](/documentation/PSReader/FeedEditionService), from a configuration you loaded by shortcode.