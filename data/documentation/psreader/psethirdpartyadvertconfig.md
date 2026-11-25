<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEThirdPartyAdvertConfig",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEThirdPartyAdvertConfig"
  },
  "title" : "PSEThirdPartyAdvertConfig"
}
-->

# PSEThirdPartyAdvertConfig

The provider-agnostic view of a third-party advert page’s configuration.

```
@objc class PSEThirdPartyAdvertConfig
```

## Overview

Every provider publishes the same essentials under its own key names:
the ad unit to request, the creative sizes, and key-value targeting.
This view reads them whatever the provider, so a delegate can serve a
Freestar page, or a provider only your app knows, from one type.
Provider-specific keys stay available in [`raw`](/documentation/PSReader/PSEThirdPartyAdvertConfig/raw).