<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSAppConfig",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader11PSAppConfigC"
  },
  "title" : "PSAppConfig"
}
-->

# PSAppConfig

The application configuration authored in the PageSuite portal, decoded
from the remote configuration payload.

```
class PSAppConfig
```

## Overview

Treat it as an opaque carrier: the SDK consumes it where it is asked for
— for example
[`open(edition:openingPage:application:)`](/documentation/PSReader/PSEditionReaderViewController/open(edition:openingPage:application:))
reads the settings for in-article adverts, third-party advert loaders
and article widgets from it.
The nested section types mirror the portal’s JSON schema and are not a
documented API; their shape follows the portal, not this SDK’s release
cycle.

To load one from a shortcode, use [`AppConfigService`](/documentation/PSReader/AppConfigService);
[Identifiers](/documentation/PSReader/Identifiers) explains the shortcode and the account GUID it
carries.

## Topics

### Loading a Configuration

[`AppConfigService`](/documentation/PSReader/AppConfigService)

Loads the app configuration published in the PageSuite portal for a
shortcode.

[`AppConfigServiceError`](/documentation/PSReader/AppConfigServiceError)

Errors thrown by [`AppConfigService`](/documentation/PSReader/AppConfigService).

### Account

[`accountGUID`](/documentation/PSReader/PSAppConfig/accountGUID)

The GUID of the account the configuration belongs to, or `nil` when
the configuration doesn’t name one.

