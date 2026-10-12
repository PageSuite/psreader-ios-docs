<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SettingsConfiguration/isDownloadWhileReadingToggleEnabled",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader21SettingsConfigurationV35isDownloadWhileReadingToggleEnabledSbvp"
  },
  "title" : "isDownloadWhileReadingToggleEnabled"
}
-->

# isDownloadWhileReadingToggleEnabled

Determines whether the download while reading option appears in the settings menu.

```
var isDownloadWhileReadingToggleEnabled: Bool
```

## Discussion

When set to `false`, the option is hidden from the settings menu. The
first-run download prompt can still record the user’s choice unless
[`isDownloadWhileReadingPreferenceAlertEnabled`](/documentation/PSReader/SettingsConfiguration/isDownloadWhileReadingPreferenceAlertEnabled) is also `false`.