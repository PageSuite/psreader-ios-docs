<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/LocalizationManager/localizedString(for:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19LocalizationManagerC15localizedString3forSSAA09LocalizedE3KeyO_tF"
  },
  "title" : "localizedString(for:)"
}
-->

# localizedString(for:)

Returns a localized version of the string identified by the given key.

```
func localizedString(for key: LocalizedStringKey) -> String
```

## Parameters

`key`

The `LocalizedStringKey` for the string.

## Discussion

The base implementation of this method uses `NSLocalizedString` with
a default value for each key. The default values can be found in the
`LocalizedStringKey` documentation.