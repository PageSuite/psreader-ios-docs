<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ReaderOnboardingConfiguration",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29ReaderOnboardingConfigurationV"
  },
  "title" : "ReaderOnboardingConfiguration"
}
-->

# ReaderOnboardingConfiguration

Configuration object for the reader’s onboarding walkthrough.

```
struct ReaderOnboardingConfiguration
```

## Overview

The prebuilt reader walks the user through its controls with a sequence
of tooltips, one per control on screen, left to right across the
navigation bar: Contents, Listen, Share, Bookmark, then Settings, and
last an article’s comment bar. Each tooltip names the control, explains
what it does, and offers a Next button and a close button. It runs
twice per device: once the first time the reader opens on a page, for
the edition view, and once the first time an article is on screen, for
the article view’s controls. Once each has appeared, it doesn’t appear
again.

Every string has a default, documented on [`LocalizedStringKey`](/documentation/PSReader/LocalizedStringKey), which
the user’s `Localizable` strings can translate. Set a string here to
replace the default outright, for example with wording from your
server. Buttons the reader isn’t showing are skipped.

```swift
var readerConfig = ReaderConfiguration(globalConfig: globalConfig)
readerConfig.onboarding.eyebrow = "WELCOME TO THE E-EDITION"
readerConfig.onboarding.bookmark.title = "Save it for later"
readerConfig.onboarding.doneButtonTitle = "Start reading"
```

To turn the walkthrough off, set [`isEnabled`](/documentation/PSReader/ReaderOnboardingConfiguration/isEnabled) to `false`.

To customize the reader screen, see [Customizing the Reader Screen](/documentation/PSReader/Customizing-the-Reader-Screen).

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/ReaderConfiguration/onboarding``

## Topics

### Creating a Configuration

[`init(globalConfig:)`](/documentation/PSReader/ReaderOnboardingConfiguration/init(globalConfig:))

Initializes a new onboarding configuration, inheriting defaults from
the provided global configuration.

### Behavior

[`isEnabled`](/documentation/PSReader/ReaderOnboardingConfiguration/isEnabled)

Whether the walkthrough runs the first time the reader opens.

[`isSettingsMenuItemEnabled`](/documentation/PSReader/ReaderOnboardingConfiguration/isSettingsMenuItemEnabled)

Whether the reader’s settings menu offers a row that plays the
walkthrough again.

### Text

[`eyebrow`](/documentation/PSReader/ReaderOnboardingConfiguration/eyebrow)

The short label above every tooltip’s title, or `nil` for the default.

[`contents`](/documentation/PSReader/ReaderOnboardingConfiguration/contents)

The text of the tooltip that points at the Contents button.

[`listen`](/documentation/PSReader/ReaderOnboardingConfiguration/listen)

The text of the tooltip that points at the Listen button.

[`share`](/documentation/PSReader/ReaderOnboardingConfiguration/share)

The text of the tooltip that points at the Share button.

[`bookmark`](/documentation/PSReader/ReaderOnboardingConfiguration/bookmark)

The text of the tooltip that points at the Bookmark button.

[`settings`](/documentation/PSReader/ReaderOnboardingConfiguration/settings)

The text of the tooltip that points at the Settings button.

[`comments`](/documentation/PSReader/ReaderOnboardingConfiguration/comments)

The text of the tooltip that points at the article’s comment bar.

[`nextButtonTitle`](/documentation/PSReader/ReaderOnboardingConfiguration/nextButtonTitle)

The title of the button that moves to the next tooltip, or `nil` for
the default.

[`doneButtonTitle`](/documentation/PSReader/ReaderOnboardingConfiguration/doneButtonTitle)

The title of the last tooltip’s button, which finishes the
walkthrough, or `nil` for the default.

[`ReaderOnboardingConfiguration.StepText`](/documentation/PSReader/ReaderOnboardingConfiguration/StepText)

The title and body of one tooltip in the walkthrough.

### Appearance

[`backgroundColor`](/documentation/PSReader/ReaderOnboardingConfiguration/backgroundColor)

The background color of each tooltip, including its arrow.

[`borderColor`](/documentation/PSReader/ReaderOnboardingConfiguration/borderColor)

The color of the thin line around each tooltip, including its arrow.

[`eyebrowLabel`](/documentation/PSReader/ReaderOnboardingConfiguration/eyebrowLabel)

Appearance of the short label above the title.

[`titleLabel`](/documentation/PSReader/ReaderOnboardingConfiguration/titleLabel)

Appearance of the title.

[`bodyLabel`](/documentation/PSReader/ReaderOnboardingConfiguration/bodyLabel)

Appearance of the body text.

[`buttonLabel`](/documentation/PSReader/ReaderOnboardingConfiguration/buttonLabel)

Appearance of the Next and Done button’s title.

[`buttonBackgroundColor`](/documentation/PSReader/ReaderOnboardingConfiguration/buttonBackgroundColor)

The background color of the Next and Done button.

[`progressIndicatorColor`](/documentation/PSReader/ReaderOnboardingConfiguration/progressIndicatorColor)

The color of the progress dot for the current step.

[`progressIndicatorInactiveColor`](/documentation/PSReader/ReaderOnboardingConfiguration/progressIndicatorInactiveColor)

The color of the progress dots for the other steps.

[`closeButtonColor`](/documentation/PSReader/ReaderOnboardingConfiguration/closeButtonColor)

The tint color of the close button.

[`preferredWidth`](/documentation/PSReader/ReaderOnboardingConfiguration/preferredWidth)

The width of each tooltip, in points.

