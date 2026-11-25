<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ReaderOnboardingConfiguration/isEnabled",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29ReaderOnboardingConfigurationV9isEnabledSbvp"
  },
  "title" : "isEnabled"
}
-->

# isEnabled

Whether the walkthrough runs the first time the reader opens.

```
var isEnabled: Bool
```

## Discussion

Defaults to `true`. Set it to `false` to never show the walkthrough,
which also removes its row from the settings menu.