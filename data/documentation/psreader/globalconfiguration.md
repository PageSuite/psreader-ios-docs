<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/GlobalConfiguration",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19GlobalConfigurationV"
  },
  "title" : "GlobalConfiguration"
}
-->

# GlobalConfiguration

A configuration object that provides global settings and delegates for
customizing the SDK’s behavior and appearance.

```
struct GlobalConfiguration
```

## Overview

Use this struct to configure default behaviors, theming, and delegate-based
customization points across the SDK. This configuration allows you to centrally
manage aspects like branding, asset customization, sharing behavior,
advertising, paywalls, and media playback functionality.

Setting a primary font, secondary font, and brand color will provide a base
theme which can be further customized as desired. The primary font is used
for labels such as titles, headlines and publication names. The secondary font
is used for the remaining UI elements. The brand color is used as an accent color.

By default the SDK interprets timestamps in the system timezone. Provide an
explicit timezone to keep this consistent across all locales.

Provide an instance of this configuration when initializing other SDK components.

## Usage

```swift
let globalConfig = GlobalConfiguration(
    apiKey: "API_KEY",
    accountGUID: "ACCOUNT_GUID",
    primaryFont: UIFont(name: "Georgia", size: 12)!,
    secondaryFont: UIFont(name: "Helvetica", size: 12)!,
    brandColor: .systemBlue
)
```

## Configuration Inheritance

`GlobalConfiguration` sits at the top of the configuration hierarchy:
component configurations created with `init(globalConfig:)` start from its
fonts, colors, and delegates. See [Configuring the Prebuilt UI](/documentation/PSReader/Configuring-the-Prebuilt-UI).

## Delegates

Optional delegates enable specific SDK features. All delegates are `nil` by
default except [`shareDelegate`](/documentation/PSReader/GlobalConfiguration/shareDelegate) and [`assetDelegate`](/documentation/PSReader/GlobalConfiguration/assetDelegate) which have built-in
defaults:

|Delegate                                                                                      |Feature                                       |Default                                                                                        |
|----------------------------------------------------------------------------------------------|----------------------------------------------|-----------------------------------------------------------------------------------------------|
|``doc://com.pagesuite.PSReader/documentation/PSReader/GlobalConfiguration/shareDelegate``     |Content sharing                               |``doc://com.pagesuite.PSReader/documentation/PSReader/ShareProvider`` with `.onlyArticleLink()`|
|``doc://com.pagesuite.PSReader/documentation/PSReader/GlobalConfiguration/assetDelegate``     |Custom icons and logos                        |``doc://com.pagesuite.PSReader/documentation/PSReader/DefaultAssetProvider``                   |
|``doc://com.pagesuite.PSReader/documentation/PSReader/GlobalConfiguration/audioDelegate``     |Text-to-speech                                |`nil` (disabled)                                                                               |
|``doc://com.pagesuite.PSReader/documentation/PSReader/GlobalConfiguration/paywallDelegate``   |Paywall screens                               |`nil` (no paywalls)                                                                            |
|``doc://com.pagesuite.PSReader/documentation/PSReader/GlobalConfiguration/advertDelegate``    |Advertisement banners & full-page advert pages|`nil` (no banners; advert pages use built-in rendering)                                        |
|``doc://com.pagesuite.PSReader/documentation/PSReader/GlobalConfiguration/mediaDelegate``     |Video playback                                |`nil` (no video)                                                                               |
|``doc://com.pagesuite.PSReader/documentation/PSReader/GlobalConfiguration/navigationDelegate``|Reader lifecycle events                       |`nil`                                                                                          |
|``doc://com.pagesuite.PSReader/documentation/PSReader/GlobalConfiguration/commentingDelegate``|Comment buttons and counts                    |`nil` (no commenting)                                                                          |

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Getting-Started>

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Theming>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/CarouselViewController``

## Topics

### Creating a Configuration

[`init(apiKey:accountGUID:primaryFont:secondaryFont:brandColor:liquidGlassPolicy:timeZone:dateFormatter:shareDelegate:assetDelegate:audioDelegate:paywallDelegate:advertDelegate:mediaDelegate:navigationDelegate:commentingDelegate:remoteConfig:)`](/documentation/PSReader/GlobalConfiguration/init(apiKey:accountGUID:primaryFont:secondaryFont:brandColor:liquidGlassPolicy:timeZone:dateFormatter:shareDelegate:assetDelegate:audioDelegate:paywallDelegate:advertDelegate:mediaDelegate:navigationDelegate:commentingDelegate:remoteConfig:))

Initializes a new global configuration object with provided customization options.

### Credentials

[`apiKey`](/documentation/PSReader/GlobalConfiguration/apiKey)

The API key used by the SDK to communicate with backend services.

[`accountGUID`](/documentation/PSReader/GlobalConfiguration/accountGUID)

The globally unique identifier representing your SDK account or publication.

### Appearance

[`primaryFont`](/documentation/PSReader/GlobalConfiguration/primaryFont)

The primary font used throughout the SDK’s UI. This is used when emphasis is desired.

[`secondaryFont`](/documentation/PSReader/GlobalConfiguration/secondaryFont)

The secondary font used throughout the SDK’s UI. This is used for general UI labels.

[`brandColor`](/documentation/PSReader/GlobalConfiguration/brandColor)

The primary brand / accent color used throughout the SDK’s interface.

[`liquidGlassPolicy`](/documentation/PSReader/GlobalConfiguration/liquidGlassPolicy)

Default Liquid Glass policy used throughout the SDK’s UI.

### Dates

[`timeZone`](/documentation/PSReader/GlobalConfiguration/timeZone)

Time zone used when parsing edition strings into `Date` objects.

[`dateFormatter`](/documentation/PSReader/GlobalConfiguration/dateFormatter)

Default `EditionDateFormatter` used for displaying edition dates across the SDK.

### Delegates

[`shareDelegate`](/documentation/PSReader/GlobalConfiguration/shareDelegate)

Delegate that decides which pages can be shared and what the share sheet offers.

[`assetDelegate`](/documentation/PSReader/GlobalConfiguration/assetDelegate)

Delegate responsible for providing custom images and assets.

[`audioDelegate`](/documentation/PSReader/GlobalConfiguration/audioDelegate)

Delegate responsible for providing audio features. Off (`nil`) by default.

[`paywallDelegate`](/documentation/PSReader/GlobalConfiguration/paywallDelegate)

Optional delegate used for handling paywall interactions within the SDK. Without it, paywalls are not displayed.

[`advertDelegate`](/documentation/PSReader/GlobalConfiguration/advertDelegate)

Optional delegate that supplies advert banners and can replace the
rendering of advert pages.

[`mediaDelegate`](/documentation/PSReader/GlobalConfiguration/mediaDelegate)

Optional delegate for enabling video and media playback. No playback functionality is provided by default.

[`commentingDelegate`](/documentation/PSReader/GlobalConfiguration/commentingDelegate)

Optional delegate for enabling commenting functionality within the reader.

[`navigationDelegate`](/documentation/PSReader/GlobalConfiguration/navigationDelegate)

Optional delegate to customize navigation actions triggered by the SDK.

### App Configuration

[`remoteConfig`](/documentation/PSReader/GlobalConfiguration/remoteConfig)

The app configuration from the PageSuite portal, which some reader
features read their settings from.

