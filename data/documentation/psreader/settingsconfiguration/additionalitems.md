<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SettingsConfiguration/additionalItems",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader21SettingsConfigurationV15additionalItemsSayAA0B8MenuItemVGvp"
  },
  "title" : "additionalItems"
}
-->

# additionalItems

Rows added below the built-in settings, in order. Empty by default.

```
var additionalItems: [SettingsMenuItem]
```

## Discussion

Each reader has its own settings configuration, so to show the same
rows everywhere, set up one [`ReaderConfiguration`](/documentation/PSReader/ReaderConfiguration) and assign it to
the archive, bookmarks and downloads configurations.

The legacy replica reader doesn’t show additional items.

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/SettingsMenuItem``