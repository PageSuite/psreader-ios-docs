<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SettingsMenuContext/dismissSettings(animated:completion:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19SettingsMenuContextC07dismissB08animated10completionySb_yycSgtF"
  },
  "title" : "dismissSettings(animated:completion:)"
}
-->

# dismissSettings(animated:completion:)

Closes the settings menu, leaving the reader open.

```
@MainActor func dismissSettings(animated: Bool = true, completion: (() -> Void)? = nil)
```

## Parameters

`animated`

Whether to animate the dismissal. Defaults to `true`.

`completion`

Called after the menu closes.