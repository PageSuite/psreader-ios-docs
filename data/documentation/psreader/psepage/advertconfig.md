<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPage/advertConfig",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader7PSEPageC12advertConfigSDySSypGSgvp"
  },
  "title" : "advertConfig"
}
-->

# advertConfig

For third-party advert pages, the advert’s configuration as
published, or `nil` when the page has none.

```
var advertConfig: [String : Any]?
```

## Discussion

Its keys depend on [`advertProvider`](/documentation/PSReader/PSEPage/advertProvider); [`thirdPartyAdvertConfig`](/documentation/PSReader/PSEPage/thirdPartyAdvertConfig)
reads the ad unit, sizes and targeting whatever the provider. Google
Ad Manager and Freestar pages have no built-in rendering: request
the ad yourself from that configuration.