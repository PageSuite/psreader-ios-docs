<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SettingsConfiguration",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader21SettingsConfigurationV"
  },
  "title" : "SettingsConfiguration"
}
-->

# SettingsConfiguration

Configuration object used to customize the reader’s settings menu.

```
struct SettingsConfiguration
```

## Overview

The settings menu allows users to adjust their reading preferences, including
viewing modes for PDF content, double-page spreads, and download behaviors.

Customize this configuration to define the default settings presented to the
user, enable or disable specific options, and align the settings menu visually
with your application’s design.

To change the menu’s options, see [Customizing the Reader Screen](/documentation/PSReader/Customizing-the-Reader-Screen);
to add a row of your own, see [Adding Your Own Rows](/documentation/PSReader/Customizing-the-Reader-Screen#Adding-Your-Own-Rows).

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/ReaderConfiguration``

## Topics

### Creating a Configuration

[`init(globalConfig:)`](/documentation/PSReader/SettingsConfiguration/init(globalConfig:))

Initializes a new settings configuration using defaults provided by the global SDK configuration.

### Appearance

[`titleLabel`](/documentation/PSReader/SettingsConfiguration/titleLabel)

Appearance configuration for the title label of the settings menu.

### Reader Settings

[`pdfLayoutModeDefault`](/documentation/PSReader/SettingsConfiguration/pdfLayoutModeDefault)

The default layout mode used when displaying PDF editions.

[`isDoublePageEnabled`](/documentation/PSReader/SettingsConfiguration/isDoublePageEnabled)

Indicates whether the double-page viewing mode is enabled, allowing two
PDF pages to be displayed side-by-side.

[`isShowContentBrowserOnFirstLoadEnabled`](/documentation/PSReader/SettingsConfiguration/isShowContentBrowserOnFirstLoadEnabled)

Determines whether the show content browser on first load option appears in the settings menu.

[`showContentBrowserOnFirstLoadDefault`](/documentation/PSReader/SettingsConfiguration/showContentBrowserOnFirstLoadDefault)

Indicates whether the content browser should show automatically on first load by default.

### Data Settings

[`isDownloadWhileReadingToggleEnabled`](/documentation/PSReader/SettingsConfiguration/isDownloadWhileReadingToggleEnabled)

Determines whether the download while reading option appears in the settings menu.

[`downloadWhileReadingDefault`](/documentation/PSReader/SettingsConfiguration/downloadWhileReadingDefault)

Indicates whether editions should download content automatically in the background while users read.

[`isDownloadWhileReadingPreferenceAlertEnabled`](/documentation/PSReader/SettingsConfiguration/isDownloadWhileReadingPreferenceAlertEnabled)

Indicates whether the SDK should prompt users about their download while
reading preference the first time they open the reader.

[`isAllowCelluarDownloadEnabled`](/documentation/PSReader/SettingsConfiguration/isAllowCelluarDownloadEnabled)

Determines whether the allow cellular download option appears in the settings menu.

[`isClearEditionDataEnabled`](/documentation/PSReader/SettingsConfiguration/isClearEditionDataEnabled)

Determines whether the clear edition data option appears in the data settings menu.

[`isAutoDeleteEditionsEnabled`](/documentation/PSReader/SettingsConfiguration/isAutoDeleteEditionsEnabled)

Determines whether the auto delete editions option appears in the data settings menu.

### Your Own Rows

[`additionalItems`](/documentation/PSReader/SettingsConfiguration/additionalItems)

Rows added below the built-in settings, in order. Empty by default.

