<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ReaderOnboardingConfiguration/StepText",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29ReaderOnboardingConfigurationV8StepTextV"
  },
  "title" : "ReaderOnboardingConfiguration.StepText"
}
-->

# ReaderOnboardingConfiguration.StepText

The title and body of one tooltip in the walkthrough.

```
struct StepText
```

## Overview

Leave a value `nil` to use the SDK’s default text for that step,
documented on [`LocalizedStringKey`](/documentation/PSReader/LocalizedStringKey).

## Topics

### Creating Step Text

[`init(title:body:)`](/documentation/PSReader/ReaderOnboardingConfiguration/StepText/init(title:body:))

Creates the text for one step.

### Text

[`title`](/documentation/PSReader/ReaderOnboardingConfiguration/StepText/title)

The tooltip’s title, or `nil` for the default.

[`body`](/documentation/PSReader/ReaderOnboardingConfiguration/StepText/body)

The tooltip’s body text, or `nil` for the default.

