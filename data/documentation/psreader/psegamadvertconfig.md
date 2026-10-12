<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEGAMAdvertConfig",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEGAMAdvertConfig"
  },
  "title" : "PSEGAMAdvertConfig"
}
-->

# PSEGAMAdvertConfig

Google Ad Manager native advert configuration.

```
@objc class PSEGAMAdvertConfig
```

## Topics

### Creating a Configuration

[`init(dictionary:)`](/documentation/PSReader/PSEGAMAdvertConfig/init(dictionary:))

Creates a configuration from a Google Ad Manager advert config.

### Requesting the Ad

[`adZone`](/documentation/PSReader/PSEGAMAdvertConfig/adZone)

The ad zone to request, from the config’s `adzone` value.

[`adSection`](/documentation/PSReader/PSEGAMAdvertConfig/adSection)

The ad section to target, from the config’s `adsection` value.

[`sizes`](/documentation/PSReader/PSEGAMAdvertConfig/sizes)

The ad sizes the slot accepts, as `[width, height]` pairs, from the
config’s `sizes` value.

[`isTesting`](/documentation/PSReader/PSEGAMAdvertConfig/isTesting)

Whether the config marks the advert as a test advert, from its
`isTesting` value; `false` when the config doesn’t say.

