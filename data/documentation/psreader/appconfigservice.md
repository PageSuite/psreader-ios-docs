<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AppConfigService",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader16AppConfigServiceV"
  },
  "title" : "AppConfigService"
}
-->

# AppConfigService

Loads the app configuration published in the PageSuite portal for a
shortcode.

```
struct AppConfigService
```

## Overview

The configuration is the one dynamic archives load. Pass it wherever the
SDK takes a [`PSAppConfig`](/documentation/PSReader/PSAppConfig), such as
[`open(edition:openingPage:application:)`](/documentation/PSReader/PSEditionReaderViewController/open(edition:openingPage:application:))
or [`remoteConfig`](/documentation/PSReader/GlobalConfiguration/remoteConfig), and read the account it belongs
to from [`accountGUID`](/documentation/PSReader/PSAppConfig/accountGUID):

```swift
let config = try await AppConfigService().configuration(forShortcode: "SHORTCODE")
guard let accountGUID = config.accountGUID else { return }
let service = FeedEditionService(accountGUID: accountGUID)
```

## Topics

### Creating a Service

[`init()`](/documentation/PSReader/AppConfigService/init())

Creates an app configuration service.

### Fetching a Configuration

[`configuration(forShortcode:)`](/documentation/PSReader/AppConfigService/configuration(forShortcode:))

Returns the configuration published for a shortcode.

